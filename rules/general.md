# General Rules

These rules apply to every agent and skill in this repository, in addition
to their own specific instructions. Agent-specific documents should not
restate these rules — they should reference this file.

## Scope of authority

An agent may only produce the outputs listed in its own "Outputs" section.
If completing a task seems to require stepping outside that scope, the
agent should stop and produce an explicit note (an observation or an open
question) instead of quietly expanding its role.

## Human review before anything external

Any artifact that could be seen by someone other than the candidate —
a CV, cover letter, application answer, email, or message to a recruiter
or employer — is a **draft** until the candidate explicitly approves it.

- Draft artifacts must be labeled as drafts.
- No agent submits, sends, or posts a draft on the candidate's behalf.
- Approval is specific to the artifact and version; approving one CV does
  not pre-approve a later revision of it.

## Draft format and PDF rendering

Tailored CVs and cover letters are drafted, reviewed, and edited as
markdown first. A PDF is a production output, not a draft format — it
can't be hand-edited the way a .md file can, so producing one before
the candidate has approved the underlying content pre-empts their
review rather than supporting it.

- Share the .md artifact for candidate review; don't generate a PDF at
  the same time by default.
- Only render a PDF once the candidate has confirmed the .md draft is
  ready to be finalized. Treat rendering as the last production step,
  not an automatic accompaniment to every draft or revision.
- If the candidate requests further changes after a PDF already
  exists, edit the .md and re-render — never hand-edit a PDF directly.

## Traceability

Every artifact should make it possible to answer: *where did this
information come from, and why does it say what it says?*

- Facts about the candidate should be traceable to a specific source
  document or a specific candidate statement.
- Judgments (matches, employer evaluations, rejections) should state the
  reasoning, not just the conclusion.
- Use the [decision log](../templates/decision-log.md) for consequential
  judgments so the reasoning survives beyond the conversation that
  produced it.

## Transparency

Agents communicate what they did and why in plain terms the candidate can
verify. Avoid silently discarding candidate input, silently resolving
ambiguity, or silently narrowing/widening a search — surface these choices
instead.

## Assumptions

When an agent must assume something to proceed (e.g., assuming a
candidate is open to remote roles because they didn't say otherwise),
the assumption must be:

- stated explicitly on the relevant artifact, and
- clearly distinguished from confirmed candidate facts.

Assumptions are never treated as facts in later stages. If a later agent
depends on an assumption, it should confirm it with the candidate rather
than build further conclusions on an unconfirmed guess.

## Uncertainty handling

Where evidence is incomplete or conflicting (e.g., ambiguous employer
reviews, an unclear vacancy requirement), agents state the uncertainty
rather than resolving it by guessing. See
[rules/decision-making.md](../rules/decision-making.md) for how
uncertainty should affect judgments and confidence levels.

## Artifact discipline

- Use the templates in [/templates](../templates) for the corresponding
  artifact type. Do not invent parallel ad hoc formats.
- Every artifact records its status (e.g., draft, under review, approved)
  and the date it was last updated. For time-sensitive facts (e.g., a
  vacancy's availability), record the time of day as well as the date —
  see [templates/vacancy.md](../templates/vacancy.md).
- Superseded artifacts are kept, not deleted, so the history of the
  process remains visible.
- After writing or substantially editing an artifact, verify the write
  landed completely: re-read the file (or otherwise confirm) that it
  ends with its intended closing section, not mid-sentence. This
  process has twice lost content silently mid-session (see
  [journal/observations.md](../journal/observations.md),
  2026-07-14 entries) — treat a truncated-looking ending as a defect to
  fix immediately, not a formatting quirk.
- When writing a long artifact (many entries, several evaluation
  sections), prefer writing it in smaller chunks over one very large
  single write — this reduces how much content is lost if a single
  write is cut short.

## Version control and history

This repository is a **playbook** — the reusable process (agents, skills,
rules, templates, docs, journal). Candidate work product and source
materials do not live in the playbook repo: they are excluded from it
(see [.gitignore](../.gitignore)) and tracked in their **own** independent
git repos, so each candidate's history is preserved without mixing
personal data into the shared playbook. The layout is:

- One repo **per candidate** under `work/<candidate>/`, each with its
  own `.git`.
- One repo for the candidate's source materials at `input/`.

Two kinds of session touch this repository, and they commit to different
places:

- **Execution sessions** run the process for a candidate. An agent that
  creates or updates artifacts under `work/<candidate>/` or `input/`
  commits those changes to *that directory's own repo* — never the
  playbook repo — so the evolution of the candidate's work product is
  preserved. Commit at natural checkpoints (the end of a run, or after a
  coherent unit of work), with a message describing what changed and why.
  This complements Artifact discipline above: superseded artifacts are
  kept in place *and* their history is captured in commits.
- **Development sessions** change the playbook itself (agents, skills,
  rules, templates, docs, or journal entries). Those changes are
  committed to the **playbook repo**, and — when they respond to an
  observation — carry a matching
  [journal/improvements.md](../journal/improvements.md) entry.

An execution agent must not commit to the playbook repo, and a playbook
change must not be committed into a candidate's repo. If a single session
genuinely needs both (e.g., a process gap surfaced mid-run prompts a
playbook fix), keep them as separate commits in their respective repos and
surface the playbook change for human review rather than folding it
silently into the run. If it is unclear which kind of session is underway,
ask the candidate rather than guessing — committing to the wrong repo
mixes exactly the histories this structure exists to keep separate.

## Commit cadence

Committing after every individual edit slows the process down without
adding meaningful history. Execution sessions should batch commits
rather than committing after each artifact touched:

- Commit at the end of a coherent unit of work — typically once a
  vacancy (or other target) is fully wrapped up — rather than after
  each file edited along the way. This sharpens "natural checkpoints"
  from Version control and history above: the checkpoint is the unit
  of work, not the individual edit within it.
- Always commit once the candidate confirms an actual submission (see
  "Recording actual submissions" below) — a submission is itself a
  natural checkpoint regardless of how much batching happened before
  it.
- If a unit of work ends early for an unrelated reason (e.g., a
  vacancy turns out to be already filled before any tailoring starts),
  that correction can still be folded into a single commit rather than
  committed separately.

This changes how *often* commits happen, not whether they happen —
uncommitted work at the end of a run should still be caught and
committed before the session ends.

## Tooling note: bash vs. direct file tools

If an agent has access to both a sandboxed shell and direct file
read/write tools, prefer the direct file tools for anything beyond
read-only inspection of this project's files. The shell's view of this
project's files has been observed to lag behind the direct tools' view
by an unpredictable amount, so a shell script that reads a file,
transforms it, and writes it back can silently overwrite recent
changes with stale content — this is the confirmed cause of at least
one instance of the truncated-artifact problem described above. When
in doubt, read and write through the direct file tools, and treat the
shell as advisory (e.g., for `grep`-style searching) rather than
authoritative.

## Source liveness

For any artifact built from an external listing (a vacancy, primarily),
whenever the artifact is touched again for substantive work — not just
read for reference — re-check that the source listing is still live
before relying on it:

- Record the check as a dated, timed entry (e.g., "Verified live,
  2026-07-14 17:49 CEST" or "Confirmed expired, 2026-07-14 17:49 CEST
  — deadline shown as 16.06.2026").
- If found expired or removed, update the artifact's status to
  `expired` and keep the artifact rather than deleting it (per
  Artifact discipline above) — a candidate may still want the record
  of what was found.
- Do not assume a listing is still live just because it was live when
  discovered; postings can close or expire between discovery and later
  work on the same artifact.
- A non-JavaScript-rendered page fetch is **never sufficient evidence
  of current liveness**, on any job board. Two independent failure
  modes have been directly observed: (1) a board serving a cached HTML
  snapshot with a static "X days left" countdown baked in at cache time
  rather than computed live; (2) a board whose underlying HTML still
  contains the original posting text and an "Apply now" button for a
  position that a real, JS-rendered browser shows as no longer
  available — the closed state is applied by client-side JavaScript
  after page load, which a non-JS fetch never executes. In both cases
  the raw fetch looked "live" while a real browser showed otherwise.
  Treat this as a general property of modern job boards, not a
  quirk of one site.
  - A *past* date found in a fetched page is still trustworthy evidence
    of expiry (the math holds regardless of when the snapshot was
    cached or what client-side state exists).
  - A page loading normally, showing an "Apply" button, or showing a
    future date is **not** trustworthy evidence of current liveness.
  - A "live" conclusion requires either a JavaScript-rendering tool
    (e.g., a Claude in Chrome browser session) or the candidate's own
    direct confirmation. Absent either, record the check as
    "reported [live/loading normally] per non-JS fetch, not
    independently confirmed" — never simply "live."
- A dead URL on a vacancy sourced from a **secondary** job board or
  aggregator (a job aggregator, a search-engine result, etc.) is not the same
  finding as a listing being expired. If the saved URL 404s, that may
  just mean the employer restructured their site or the aggregator's
  link rotted — it says nothing about whether the underlying vacancy
  is still open elsewhere. Record this outcome as "re-check
  inconclusive: source URL no longer resolves" and, where possible,
  search for the vacancy's current URL rather than marking it
  `expired` on URL-rot evidence alone. (A concrete instance is recorded
  in [journal/observations.md](../journal/observations.md), 2026-07-14.)
- Once a JS-rendering check is available, a confirmed-live result
  looks different from board to board — useful to recognize rather
  than expecting one universal signal. Positive signals seen across
  boards include: a live-computed "X days left (until DATE)" countdown;
  a working apply/respond button alongside a current viewer or
  applicant count; the absence of an "archived" or "closed" banner that
  the same board shows on dead listings; and an application form that
  fully renders and accepts input (a closed requisition typically can't
  be applied to at all). Some boards instead stop serving a closed
  posting entirely — 404-ing or redirecting — rather than showing a
  stale-but-present page. (Board-specific examples from past checks are
  recorded in [journal/observations.md](../journal/observations.md).)

## Recording actual submissions

This process routes drafts for candidate approval but does not itself
submit applications (see "Human review before anything external"). When
the candidate reports they've actually applied — whether through a full
[application package](../templates/application.md) this process
assembled, or by applying directly with only a tailored CV and cover
letter as standalone drafts — the actual submission is still recorded,
retroactively if needed:

- Create the application package artifact if one doesn't exist yet (a
  standalone tailored CV + cover letter pair is common for vacancies
  where no application-specific questions were captured — see
  [skills/cv-tailoring.md](../skills/cv-tailoring.md) and
  [skills/application-writing.md](../skills/application-writing.md)),
  or update the existing one.
- Set its status to `submitted` and record the date.
- Capture the *actual* materials sent, not just the last draft — the
  candidate may edit the text before sending. If a final file (e.g. an
  exported PDF) exists, store it alongside the application package
  artifact and reference it; note any differences from the drafting
  version rather than silently overwriting the draft's history.
- Record the actual answers given to any application-specific
  questions (e.g. stated financial expectations), not just draft
  answers.
- Update the corresponding [vacancy artifact](../templates/vacancy.md)'s
  status to `applied`.

This keeps the historical record accurate: what was actually sent can
differ from the last artifact the candidate reviewed here, and losing
that distinction would make the on-file materials misleading if
revisited later (e.g. at an interview, or when tailoring a follow-up
application to the same employer).

## Escalation

If an agent cannot complete its task because required input is missing,
contradictory, or out of scope, it should:

1. Produce whatever partial artifact is safely possible.
2. Clearly flag what is missing or unresolved.
3. Ask the candidate directly rather than guessing or blocking silently.
