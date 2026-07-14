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
  modes have been directly observed in the same session: (1) a job
  board (justjoin.it) serving a cached HTML snapshot with a static
  "X days left" countdown baked in at cache time rather than computed
  live; (2) a job board (Teamtailor) whose underlying HTML still
  contains the original posting text and an "Apply now" button for a
  position that a real, JS-rendered browser shows as no longer
  available — the closed state is applied by client-side JavaScript
  after page load, which a non-JS fetch never executes. Both platforms
  looked "live" to a raw fetch while a real browser showed otherwise.
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
  aggregator (JobLeads, a Google search result, etc.) is not the same
  finding as a listing being expired. If the saved URL 404s, that may
  just mean the employer restructured their site or the aggregator's
  link rotted — it says nothing about whether the underlying vacancy
  is still open elsewhere. Record this outcome as "re-check
  inconclusive: source URL no longer resolves" and, where possible,
  search for the vacancy's current URL rather than marking it
  `expired` on URL-rot evidence alone. (Observed on the Onwelo vacancy,
  2026-07-14 — see [journal/observations.md](../journal/observations.md).)
- Once a JS-rendering check is available, a confirmed-live result
  looks different per platform — useful to recognize rather than
  expect one universal signal: justjoin.it shows a live-computed "X
  day left (until DATE)" countdown; hh.ru shows a working
  "Откликнуться" button plus a current viewer count and lacks the "В
  архиве" (archived) banner it shows on closed vacancies; Lever boards
  simply keep serving the posting with an "Apply for this job" button
  (they tend to 404 or redirect once genuinely closed, rather than
  showing a stale-but-present page); ATS application forms (e.g.
  Luxoft/SuccessFactors-style) that fully render and accept input are
  themselves strong evidence, since a closed requisition typically
  can't be applied to at all.

## Escalation

If an agent cannot complete its task because required input is missing,
contradictory, or out of scope, it should:

1. Produce whatever partial artifact is safely possible.
2. Clearly flag what is missing or unresolved.
3. Ask the candidate directly rather than guessing or blocking silently.
