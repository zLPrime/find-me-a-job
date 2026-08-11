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
- The vacancy artifact, if one already exists, for context on prior
  fields/values used at this employer.

## Expected Outputs

- A vacancy artifact with `Status: draft (pre-filled, awaiting
  candidate review — not submitted)`, documenting exactly what was
  filled, what was left blank and why, and any open questions.
- A form left mid-review in the browser: fields filled, consent
  checkboxes and the submit button untouched.

## Procedure

1. **Check the form before building any other artifact.** Open the
   live Apply flow first — a "1-click Apply" label on the job-board
   listing page is not reliable evidence of what actually happens; some
   1-click-labeled listings open a full external form, and some
   full-looking listings are genuinely one click. Only start building a
   CV, decision-log entry, or employer file after confirming what kind
   of form this actually is.
2. **If it's a genuine 1-click widget: do not click it.** Set it aside
   as an open, candidate-actionable item instead (e.g. "1-click Apply
   available, not yet clicked — candidate to submit"). Unlike a
   pre-filled form, clicking a 1-click button *is* the submission, with
   no review step — that final click belongs to the candidate, even on
   a fast-track listing. Only click through if the candidate explicitly
   asks.
3. **If it's a real form, fill the standard fields directly:** name,
   email, phone, and — whenever a LinkedIn or similar profile-link
   field is present — the candidate's LinkedIn URL, even if the field
   is optional or not asked about. Attempt the CV upload; if the upload
   tool is broken or fails, say so plainly on the vacancy artifact
   ("CV upload NOT completed") rather than leaving it ambiguous.
4. **Match the form's own UI language**, not the job posting's
   language and not English by default. Check every field and label,
   not just free-text ones — a form can be in a different language than
   the posting that linked to it.
5. **Ground every free-text or per-skill answer strictly in the
   candidate profile.** For forms with individual per-technology
   fields (e.g. "years of experience with X"), check each technology
   against the profile before entering a number. Where the profile
   doesn't confirm a technology, enter an honest non-claim (e.g. "0")
   rather than a plausible-sounding invented figure — same rule as
   [rules/factual-accuracy.md](../rules/factual-accuracy.md) applied at
   form-field granularity.
6. **Leave genuinely complex forms for the candidate.** If a form has
   many UI elements requiring judgment calls only the candidate can
   make (financial expectations, availability specifics, an
   open-ended "why this role" essay), fill what's confidently
   groundable and leave the rest with the actual values the candidate
   would need, rather than guessing on their behalf.
7. **Fold vacancy-specific framing into the CV when there's no
   cover-letter field.** If the form has no dedicated cover-letter or
   "why this role" field, work any vacancy-specific "why this fits"
   framing into the CV's Summary section instead of dropping it.
8. **Never touch consent or submission.** GDPR/privacy checkboxes and
   the final submit button (Wyślij, Submit application, Apply, etc.)
   are always left untouched — see rules/general.md's "Human review
   before anything external." Pre-filling every other field is not an
   exception to this.
9. **Record the actual submission, not just the draft.** When the
   candidate reports a form sent — especially with a correction, like a
   revised rate — log the new fact to `input/notes.md` first (see
   rules/general.md's "Recording actual submissions"), then update the
   vacancy status and the actual values sent.
10. **Move on without waiting for "next."** Once a vacancy is fully
    pre-filled (or set aside, per step 2), proceed to the next one in
    the batch automatically rather than pausing for confirmation —
    surface a running list and flag anything needing a decision inline.

## Known Form Quirks

Custom form widgets vary in how they actually commit a value — for
example, some dropdown-style components don't register a selection
just from typed text and need the rendered option clicked directly, or
a form's real extent only becomes clear after scrolling to its end.
These behaviors are properties of the specific ATS or platform a given
employer happens to use, not of this process, so they're recorded
per-candidate under `work/<candidate>/` (see
[work/README.md](../work/README.md)) as they're discovered, rather
than catalogued here — this skill stays applicable to any board or
platform. Check that candidate's notes before assuming a form behaves
like the last one.

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
