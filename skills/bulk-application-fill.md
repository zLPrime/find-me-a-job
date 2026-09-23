# Skill: Bulk Application Fill

## Purpose

Pre-fill real application forms directly in a live browser session for
a batch of job-board listings, so the candidate can review and submit
each one themselves with minimal friction. This is the field-level
companion to [docs/workflow.md](../docs/workflow.md)'s "Alternate path:
bulk job-board sweep" — that document describes the stage-by-stage
loop; this skill describes how to actually handle a given form once
you're in it.

## When to Invoke

- The candidate is directing a bulk sweep of a job board's listings
  (see the workflow's alternate path) rather than moving a single
  vacancy through the staged pipeline.
- A specific vacancy's real application form needs to be pre-filled,
  regardless of how it was discovered.

## Required Inputs

- The candidate profile — the only source for any claim entered into a
  form field.
- A live, JavaScript-rendering browser session (a non-JS fetch cannot
  reliably tell a real form from a closed listing or a 1-click widget —
  see rules/general.md's "Source liveness").
- The existing set of vacancy (and employer) artifacts under
  `work/<candidate>/`, to check each posting against before creating a
  new artifact — see step 1 and the [deduplication](deduplication.md)
  skill.
- The vacancy artifact, if one already exists, for context on prior
  fields/values used at this employer.

## Expected Outputs

- A vacancy artifact with `Status: draft (pre-filled, awaiting
  candidate review — not submitted)`, documenting exactly what was
  filled, what was left blank and why, and any open questions.
- A form left mid-review in a **live, still-open** browser tab: fields
  filled, consent checkboxes and the submit button untouched. This is a
  separate deliverable from the vacancy artifact, not a duplicate of it:
  the artifact records *what* was filled, but the candidate reviews and
  submits the actual open form. A pre-filled form exists only as long as
  its tab stays open — it cannot be rebuilt from the artifact, so closing
  the tab discards the pre-fill entirely and re-filling means starting
  from scratch.

## Procedure

1. **Deduplicate before creating anything for this posting.** Before
   opening the form, building an artifact, or writing the checkpoint
   stub (step 11), check whether this requisition is already tracked —
   run the [deduplication](deduplication.md) skill against the existing
   vacancy artifacts under `work/<candidate>/`. Match on the
   *requisition*, not just the employer: the same posting recurs under a
   different board URL, slug, or hash, or resurfaces through a job
   board's "similar offers" carousel, and has been missed here before.
   The strongest key is the **application-form URL** (the resolved Apply
   target, captured at step 2): two listings that lead to the same form
   URL are the same requisition, even when their listing URLs differ, so
   check it against the Links block of existing artifacts as soon as
   you've resolved it. If it's already tracked, update that artifact in
   place rather than creating a second one; if it's a genuinely distinct
   opening at an already-tracked employer, keep both, clearly
   distinguished. Doing
   this first is what keeps the per-posting checkpoint (step 11) from
   minting duplicate stubs — and because each posting is now checkpointed
   to disk before the next is triaged, the set you match against is
   complete and current, including postings found earlier in this same
   sweep.
2. **Check the form before building any other artifact — and record its
   URL.** Open the live Apply flow first — a "1-click Apply" label on the
   job-board listing page is not reliable evidence of what actually
   happens; some 1-click-labeled listings open a full external form, and
   some full-looking listings are genuinely one click. Capture the
   resolved **application-form URL** (the real target the Apply button
   lands on, commonly a different ATS domain than the listing) in the
   artifact's Links block — it's often the only stable identifier when
   the listing is a thin redirect, and it feeds the step-1 dedup check.
   Only start building a CV, decision-log entry, or employer file after
   confirming what kind of form this actually is.
3. **If it's a genuine 1-click widget: do not click it.** Set it aside
   as an open, candidate-actionable item instead (e.g. "1-click Apply
   available, not yet clicked — candidate to submit"). Unlike a
   pre-filled form, clicking a 1-click button *is* the submission, with
   no review step — that final click belongs to the candidate, even on
   a fast-track listing. Only click through if the candidate explicitly
   asks.
4. **If it's a real form, fill the standard fields directly:** name,
   email, phone, and — whenever a LinkedIn or similar profile-link
   field is present — the candidate's LinkedIn URL, even if the field
   is optional or not asked about. Attempt the CV upload; if the upload
   tool is broken or fails, say so plainly on the vacancy artifact
   ("CV upload NOT completed") rather than leaving it ambiguous.
5. **Match the form's own UI language**, not the job posting's
   language and not English by default. Check every field and label,
   not just free-text ones — a form can be in a different language than
   the posting that linked to it.
6. **Ground every free-text or per-skill answer strictly in the
   candidate profile.** For forms with individual per-technology
   fields (e.g. "years of experience with X"), check each technology
   against the profile before entering a number. Where the profile
   doesn't confirm a technology, enter an honest non-claim (e.g. "0")
   rather than a plausible-sounding invented figure — same rule as
   [rules/factual-accuracy.md](../rules/factual-accuracy.md) applied at
   form-field granularity.
7. **Leave genuinely complex forms for the candidate.** If a form has
   many UI elements requiring judgment calls only the candidate can
   make (financial expectations, availability specifics, an
   open-ended "why this role" essay), fill what's confidently
   groundable and leave the rest with the actual values the candidate
   would need, rather than guessing on their behalf.
8. **Fold vacancy-specific framing into the CV when there's no
   cover-letter field.** If the form has no dedicated cover-letter or
   "why this role" field, work any vacancy-specific "why this fits"
   framing into the CV's Summary section instead of dropping it.
9. **Never touch consent or submission.** GDPR/privacy checkboxes and
   the final submit button (Wyślij, Submit application, Apply, etc.)
   are always left untouched — see rules/general.md's "Human review
   before anything external." Pre-filling every other field is not an
   exception to this.
10. **Record the actual submission, not just the draft.** When the
    candidate reports a form sent — especially with a correction, like a
    revised rate — log the new fact to `input/notes.md` first (see
    rules/general.md's "Recording actual submissions"), then update the
    vacancy status and the actual values sent.
11. **Checkpoint each posting to disk before moving on.** A browser tab
    is not a record. Treat the on-disk vacancy artifact as the single
    source of truth for a posting's existence and progress, and write it
    *as* each posting is triaged and pre-filled — not batched up for the
    end of the sweep. A discovered posting gets its artifact (at minimum
    a stub with its URL, employer, and `Status: draft`) before the next
    tab is opened, and that artifact is updated in place as the pre-fill
    proceeds, so a lost browser session costs at most the one posting in
    hand rather than the whole sweep. This is a durability checkpoint —
    persisting the file with the direct file tools — and is distinct from
    git commit cadence, which stays batched per unit of work (see
    rules/general.md's "Commit cadence"); the disk write, not the commit,
    is what survives a browser crash. But the record is **not** a
    substitute for the live form: it captures *what* was filled, while
    the pre-filled form itself — the thing the candidate actually
    submits — survives only as an open tab and cannot be rebuilt from the
    artifact. So never close a pre-filled form's tab; leaving it open is
    the deliverable, and having checkpointed the record is not permission
    to close it. Once a posting is checkpointed, move on by opening the
    next posting in a new tab (or setting it aside per step 3) — not by
    closing the filled ones — rather than pausing for confirmation;
    surface a running list and flag anything needing a decision inline.
12. **Verify in the browser before reporting a posting pre-filled.**
    Don't state that a form was filled — to the candidate or on the
    artifact — unless you've just confirmed, in the live browser, that
    the fields actually hold the values and the tab is still open. A
    saved record is not evidence the form is ready: it is easy to write
    `Status: draft (pre-filled…)` while the real form was closed, reset,
    or never committed its values (see "Known Form Quirks" — some widgets
    don't register a typed value). Report against the actual browser
    state, not against what the artifact claims — a false "it's
    pre-filled" is worse than an honest "I couldn't fill it," because the
    candidate acts on it without checking. This verification is **one
    confirmation of the finished form's state** — read the assembled form
    back once, before hand-off — not a re-check after every individual
    field; confirming the whole form at the end is enough, and reading it
    back as structured field data is both faster and a truer check than
    a per-field visual pass.

## Known Form Quirks and Tool-Driving Notes

Custom form widgets vary in how they actually commit a value — for
example, some dropdown-style components don't register a selection
just from typed text and need the rendered option clicked directly, or
a form's real extent only becomes clear after scrolling to its end.
The same is true of *how the tools are driven* for speed — which
operations can be batched, which reads are faster or more reliable than
others, and how results are transferred back. Both kinds of detail are
properties of the specific ATS, platform, or tool surface a given run
happens to use, not of this process, so they're recorded per-candidate
under `work/<candidate>/` (see [work/README.md](../work/README.md)) as
they're discovered, rather than catalogued here — this skill stays
applicable to any board, platform, or toolset. Check that candidate's
notes before assuming a form behaves, or a tool performs, like the last
one; working efficiently (batching independent steps, avoiding redundant
verification passes) is expected, but never at the cost of the
verify-before-report guarantee in step 12.

## Quality Criteria

- Every field value traces to the candidate profile or to the
  candidate's own stated correction — never invented.
- The form's own language is used throughout, not assumed from the
  posting.
- Consent checkboxes and the submit control are untouched on every
  form this skill produces.
- The vacancy artifact accurately reflects what was and wasn't filled,
  so a later session (or the candidate, reviewing days later) doesn't
  need to re-open the form to know its state.
- Every posting touched has an on-disk artifact written before the next
  one is opened, so a lost browser session never erases progress that
  can't be recovered from disk — the tabs are never the sole record of
  what was found or how far it got.
- No posting gets a second artifact because it was reached through a
  different URL, slug, or "similar offers" link — each requisition is
  checked against the existing artifacts (step 1) before anything is
  created for it.
- Every pre-filled form is still open in its own live tab at hand-off —
  no form tab is closed after filling, and the saved artifact is never
  treated as a stand-in for the live form the candidate has to submit.
- A posting is reported as pre-filled only after the live form is
  confirmed filled and open in the browser, never inferred from the
  existence of a saved `draft (pre-filled…)` artifact.

## Limitations

- This skill never submits an application or clicks a 1-click Apply
  button on the candidate's behalf.
- It does not perform the staged pipeline's formal employer evaluation
  or match scoring — fit judgments made here are direct and
  lightweight, not decision-log-grade.

## Future Improvements

- If the same platform-specific quirk turns up independently in
  multiple candidates' `work/<candidate>/` notes, that's a signal it's
  actually general (a property of the ATS, not the candidate) and
  worth promoting into this skill's "Known Form Quirks" section instead
  of staying duplicated per-candidate.
