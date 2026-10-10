# Improvements

A record of concrete changes made to this playbook (agents, skills,
rules, templates) in response to one or more entries in
[journal/observations.md](observations.md). This is the audit trail of
how the process itself has evolved.

## How to add an entry

Append a new entry at the top, using this structure:

```markdown
## <date> — <short title>

Triggered by: <link/reference to the observation(s) that prompted this>
Change made: <what was edited, and where — file(s) and section(s)>
Reasoning: <why this change addresses the observation>
Expected effect: <what should be different going forward>
```

## Entries

## 2026-09-29 — Named commit checkpoints for interview practice

Triggered by: the candidate noticing only one mock interview session
was committed. Four sessions (2026-09-27, three on 2026-09-29) and
changes to the practice profile, study topics, and question bank sat
uncommitted in the candidate repo; the one committed session was
committed during a playbook development session, not by the practice
track.
Change made: Commit steps at the end of the interview dialog (step 5)
and an uncommitted-files check before planning (step 0) in
[skills/mock-interviewing.md](../skills/mock-interviewing.md); a
commit step in "Closing the session" in
[skills/practice-tracking.md](../skills/practice-tracking.md); practice
checkpoints and "commit at the checkpoint, not at session end" in
[rules/general.md](../rules/general.md), "Commit cadence".
Reasoning: The commit rule tied checkpoints to vacancies and
submissions, which practice sessions never reach, and its fallback
("commit before the session ends") never fires when a dialog ends with
the agent asking a question and the candidate leaving.
Expected effect: Every practice session is committed when the
interview ends and again when it is closed out; leftovers are caught
before the next session is planned.

## 2026-09-29 — Mock interviews only ask questions from the question bank

Triggered by: a standing rule from the candidate: always take questions
from the bank; if new questions are needed, add them to the bank first.
Change made: Planning and interview steps in
[skills/mock-interviewing.md](../skills/mock-interviewing.md) (bank-only
main questions, follow-ups scoped to the current bank question);
responsibilities and failure modes in
[agents/interviewer-agent.md](../agents/interviewer-agent.md) and
[agents/interview-question-agent.md](../agents/interview-question-agent.md);
a new trigger in
[skills/interview-question-design.md](../skills/interview-question-design.md);
the Plan table in
[templates/mock-interview-session.md](../templates/mock-interview-session.md);
step 1 of the practice track in [docs/workflow.md](../docs/workflow.md).
Reasoning: The evaluator scores against the bank's key points and the
practice profile tracks questions by bank ID; a question asked outside
the bank can be neither scored fairly nor tracked for re-asks.
Expected effect: Every asked question has an ID, key points, and a
place in question history; the bank grows from real practice needs.

## 2026-09-29 — Gated mock interview close-out on an actual practice profile update

Triggered by: [observations.md](observations.md), "2026-09-29 — Mock
interview results never reached the practice profile."
Change made: Added a hand-off step after the corrections debrief in
[skills/interview-evaluation.md](../skills/interview-evaluation.md) and
matching output/failure modes in
[agents/interview-evaluation-agent.md](../agents/interview-evaluation-agent.md);
made the interview-progress-agent the sole owner of the `recorded in
practice profile` status, set only after the profile's change note
cites the session
([agents/interview-progress-agent.md](../agents/interview-progress-agent.md),
[skills/practice-tracking.md](../skills/practice-tracking.md), "Closing
the session",
[templates/mock-interview-session.md](../templates/mock-interview-session.md));
added a pre-planning check (step 0) and a question-history check to
[skills/mock-interviewing.md](../skills/mock-interviewing.md), plus a
per-exchange write checkpoint for the transcript; reinforced the
sequence in [agents/orchestrator.md](../agents/orchestrator.md) and
[docs/workflow.md](../docs/workflow.md), "Parallel track: interview
practice."
Reasoning: The failure was not a missing rule but a missing hand-off
and an unverified status: the debrief ended the conversation, a status
claimed work that wasn't done, and the next session trusted it.
Expected effect: Every evaluated session is folded into the profile
before the next one is planned; a stale profile is caught at planning
time instead of producing repeated questions; an interrupted session
keeps its transcript up to the interruption.

## 2026-09-28 — Saved the original job description as a verbatim posting snapshot

Triggered by: the candidate asking whether vacancy artifacts keep the
original job description. They did not: the vacancy summary held links
and a structured extraction only, so once a listing expired or was
edited, the full posting text was gone — even though it is what CV and
cover-letter tailoring, interview prep, and "did the requirements
change after I applied?" checks need.
Change made: Added a "Posting Snapshot" template to
[templates/vacancy.md](../templates/vacancy.md) (verbatim text, capture
time, source URL, capture method, language, completeness, supersedes
link) and a "Posting snapshot" line in its Links block; added the
snapshot as an expected output and quality criterion in
[skills/vacancy-analysis.md](../skills/vacancy-analysis.md), with a
new dated snapshot on every posting change; added it to the
responsibilities, success criteria and failure modes of
[agents/vacancy-discovery-agent.md](../agents/vacancy-discovery-agent.md);
added `vacancies/postings/<vacancy-name>-<date>.md` to
[work/README.md](../work/README.md)'s suggested layout. Kept in a
separate file rather than inline so summaries stay short to scan.
Existing vacancy artifacts were not backfilled.
Reasoning: the same "nothing important lives only somewhere
ephemeral" principle behind every artifact here — a live web page is
as ephemeral as a chat transcript. Snapshots are never edited, which
also preserves the exact version the candidate applied against.
Expected effect: every newly recorded vacancy keeps its original text,
so later work that depends on the posting still has it after the
listing goes offline.

## 2026-09-25 — Added a "Study Topics" list to the interview practice track

Triggered by: the candidate asking, mid-session, to note "Bloom
filters" as a topic to explore later (surfaced tangentially while
explaining the correct answer to a deduplication question), then
asking for a genuine structured place for such notes rather than an
ad hoc line in work/jakub-charabet/TODO.txt — a plain personal scratch
list not meant to hold this kind of thing — plus a request that the
context each topic surfaced in be captured, not just its name.
Change made: Added
[templates/study-topics.md](../templates/study-topics.md) (one running
list per candidate: topic, first-surfaced date, context — the specific
question/session/exchange it came from — why it matters, and status);
added it to [docs/glossary.md](../docs/glossary.md) and to
[work/README.md](../work/README.md)'s suggested directory layout,
alongside the practice profile; added a step to the "Parallel track:
interview practice" section of
[docs/workflow.md](../docs/workflow.md) so capturing a tangential topic
is a standing part of the loop, not something remembered only when
asked; and added matching quality-criteria lines to
[skills/mock-interviewing.md](../skills/mock-interviewing.md) and
[skills/interview-evaluation.md](../skills/interview-evaluation.md),
since a tangential topic can surface during the interview itself, the
evaluation, or a corrections debrief. Created
work/jakub-charabet/interviews/practice/study-topics.md with the Bloom
filter entry. Also cleaned up the earlier ad hoc line in
work/jakub-charabet/TODO.txt (removed — it had also lost its line
break on append, a good example of why an unstructured scratch file
isn't the right home for this).
Reasoning: matches the same "nothing important lives only in
conversation" principle behind every other artifact in this repo — a
topic worth studying later is exactly the kind of thing that gets lost
if it only exists as a line in a chat transcript, and a plain-text
scratch file with no structure doesn't preserve *why* something was
flagged, which is the part that makes it useful months later.
Expected effect: future sessions capture tangential study topics with
real context automatically, in a place that scales past a couple of
ad hoc lines, without the candidate having to ask each time.

## 2026-09-25 — Added a "Corrections Debrief" step to the interview practice track

Triggered by: the candidate's direct request, during a mock interview
session, for a detailed breakdown of every error and inconsistency in
an answer (not just what the Evaluation's "key points missed" field
captured), with the correct answer given in plain language — and his
observation that this should be a standard part of every session
rather than something he has to remember to ask for.
Change made: Added a "Corrections Debrief" section to
[templates/mock-interview-session.md](../templates/mock-interview-session.md);
a "Corrections Debrief" procedure to
[skills/interview-evaluation.md](../skills/interview-evaluation.md)
describing when to offer it (always, in one line, right after
presenting the Evaluation), what it must cover (every error, not just
the first found; a plain-language correct answer per
[rules/outputs.md](../rules/outputs.md)'s existing "Language and tone"
rule; any question bank gap surfaced); a matching Responsibilities/
Outputs update to
[agents/interview-evaluation-agent.md](../agents/interview-evaluation-agent.md);
and a one-line addition to the "Evaluate" step in
[docs/workflow.md](../docs/workflow.md) so it isn't missed by an agent
following the workflow doc alone.
Reasoning: The Evaluation section's existing "key points missed" and "a
strong answer would add" fields are written for scoring, not for
studying from — they're terse and assume the reader already knows the
correct answer. A candidate actually improving between sessions needs
the specific errors named plainly and the correct answer spelled out,
not just a score. Making the offer standard (rather than only available
if asked) prevents it from being skipped in a future session run by an
agent that wasn't part of this conversation.
Expected effect: Every future evaluated session ends with an explicit,
one-line offer of a corrections debrief; when taken up, the result is
recorded in the session artifact itself (not left only in conversation)
and question-bank gaps it surfaces get folded back into the bank.

## 2026-09-25 — Added an interview practice track: four agents, four skills, three templates

Triggered by: [journal/observations.md](observations.md), 2026-09-25 —
no process for practicing interviews once a vacancy reaches the
interview stage.
Change made:
- New agents:
  [interview-question-agent](../agents/interview-question-agent.md),
  [interviewer-agent](../agents/interviewer-agent.md),
  [interview-evaluation-agent](../agents/interview-evaluation-agent.md),
  [interview-progress-agent](../agents/interview-progress-agent.md).
- New skills:
  [interview-question-design](../skills/interview-question-design.md),
  [mock-interviewing](../skills/mock-interviewing.md),
  [interview-evaluation](../skills/interview-evaluation.md),
  [practice-tracking](../skills/practice-tracking.md).
- New templates:
  [question-bank](../templates/question-bank.md),
  [mock-interview-session](../templates/mock-interview-session.md),
  [practice-profile](../templates/practice-profile.md).
- [docs/workflow.md](../docs/workflow.md): added "Parallel track:
  interview practice."
- [docs/glossary.md](../docs/glossary.md): added Question Bank, Mock
  Interview Session, Practice Profile.
- [work/README.md](../work/README.md): added the
  `interviews/practice/` layout.
- [agents/orchestrator.md](../agents/orchestrator.md): offer the
  practice track at the interview stage; don't leave sessions
  unevaluated.
- [README.md](../README.md): added the practice track to "How to Use
  the Playbook."
Reasoning: Interview practice needs the same discipline as the rest of
the process: artifacts instead of conversation, single-responsibility
agents, and honest judgments. See
[journal/decision-log.md](decision-log.md), 2026-09-25, for why the
interviewer and evaluator are separate.
Expected effect: The candidate can rehearse for a real interview
against questions drawn from the vacancy and prep notes, get a direct
evidence-backed assessment, and see progress across sessions, with the
next session targeting their weakest topics.

## 2026-09-08 — Turned seven external job-search prompt tips into playbook enhancements, three new skills, and a new agent

Triggered by: [journal/observations.md](observations.md), 2026-09-08 — a
maintainer-provided set of seven external job-search prompt tips, mapped
against existing agents and skills, surfaced four implicit-craft gaps and
three missing capabilities.
Change made:
- [skills/cv-tailoring.md](../skills/cv-tailoring.md): added two Style
  Conventions — "Bullet construction" (lead with a strong action verb, one
  idea, state the outcome, keep to ~two lines; strength from fact +
  outcome, not adjectives — a phrasing rule that never licenses a new
  fact) and "ATS-parseable content and terminology" (literal section
  headings; expand an acronym once alongside it; align the CV's wording to
  the *posting's* term for a skill the candidate genuinely holds, while a
  keyword they lack stays a surfaced gap, not inserted). Extended the
  Limitations formatting note to distinguish in-scope ATS *content/
  terminology* from render-time ATS *visual layout*, preserving the
  existing scope boundary.
- [skills/matching.md](../skills/matching.md): added a keyword/terminology
  gap check to Expected Outputs and a matching Quality Criterion — split
  the vacancy's named requirements into (a) held-and-surfaced, (b)
  held-but-worded-differently (for honest alignment by cv-tailoring), and
  (c) genuinely absent (recorded as opposing factors/unknowns, never
  inserted). This gives the honest half of "match the job description" a
  procedure while keeping the dishonest half out, and keeps the two
  strictly distinct.
- [skills/application-writing.md](../skills/application-writing.md): added
  a "Human voice — avoid an AI-written tell" Style Convention naming the
  concrete machine-generated hallmarks to cut (hollow superlatives,
  throat-clearing openers, boilerplate connectives) and grounding
  confidence in a stated fact + outcome, cross-referencing
  rules/outputs.md's "Language and tone."
- New [skills/role-discovery.md](../skills/role-discovery.md) + new
  [agents/role-discovery-agent.md](../agents/role-discovery-agent.md): a
  new upstream capability that generates the *role types* (including
  adjacent/transferable ones) a candidate is qualified for from the
  profile alone, ranked with honest, explicitly-hedged demand/response
  estimates and visible constraint-driven exclusions. It feeds both
  discovery agents. Wired as an input and a broadened responsibility into
  [agents/company-discovery-agent.md](../agents/company-discovery-agent.md)
  and
  [agents/vacancy-discovery-agent.md](../agents/vacancy-discovery-agent.md)
  so discovery searches across role types, not just the one title first
  named.
- New [skills/outreach-messaging.md](../skills/outreach-messaging.md):
  concise, person-directed recruiter/contact outreach and follow-up
  messages (hook-led, reply-seeking, not favor-asking; specific and human;
  factual; recipient's language). Owned by
  [agents/application-agent.md](../agents/application-agent.md) (Purpose,
  a responsibility, and Skills Used extended), which drafts them for the
  candidate to send — never sending itself.
- New [skills/search-strategy.md](../skills/search-strategy.md): advisory
  synthesis over the pipeline — application volume/cadence, customization
  tiering (choosing the staged pipeline vs. the bulk sweep per
  opportunity), and follow-up timing, all as adjustable suggestions.
  Owned by [agents/reporting-agent.md](../agents/reporting-agent.md)
  (Purpose, a responsibility, and Skills Used extended).
- [docs/workflow.md](../docs/workflow.md): inserted "Explore fitting role
  types" as new stage 3 (renumbering the rest, diagram included) between
  building the profile and discovering employers; noted the matching-stage
  keyword/terminology gap check; noted the tailoring stage now produces
  action-verb/ATS-parseable, honestly-aligned content; folded outreach
  drafting into the application-guidance stage and search-strategy into the
  reporting stage.
Reasoning: The tips were a useful external checklist against a playbook
that had grown around producing and submitting materials for postings a
candidate already knew to search for. The genuinely-covered tips still
pointed at craft the playbook left to each agent's discretion, so writing
them down as conventions closes silent-default gaps the same way the
2026-07-15 house-style round did. The three missing capabilities were real
holes at the three edges the pipeline never reached — upstream (what to
search for), sideways (messaging a person, not a posting), and meta (how
to pace the search). Each was built to the playbook's own standards: no
candidate/profession/technology specifics (per
[docs/operating-principles.md](../docs/operating-principles.md)), every
new judgment kept honest (hedged estimates with stated basis; terminology
alignment that can't become a claim of a missing skill; nothing sent on
the candidate's behalf), and role-discovery given its own agent per the
single-responsibility principle rather than overloading an existing one.
Expected effect: A search can start from "what roles fit me?" and widen
beyond a single title; tailored CVs default to tight, action-led,
ATS-parseable bullets with honest keyword alignment; matching makes the
held-vs-absent keyword split explicit; cover letters and outreach read as
human and specific; and the candidate can get concrete, honest guidance on
how much to apply, where to spend tailoring effort, and when to follow up —
none of it at the cost of the factual-accuracy and human-approval
guarantees.

## 2026-08-28 — Added a Language selection rule so messages to a person take the recipient's language, not English by default

Triggered by: [journal/observations.md](observations.md), 2026-08-28 —
"Draft messages to people defaulted to English, ignoring the recipient's
(and candidate's) language." A candidate report that outreach drafts to a
Polish-speaking recipient came back in English despite the candidate being
a native Polish speaker.
Change made:
- [rules/outputs.md](../rules/outputs.md): added a "Language selection"
  subsection under "Language and tone" that names two cases with different
  signals — (a) materials bound to a posting or form keep the existing
  posting/form-language rule; (b) a message addressed to a specific person
  is written in *that person's* language, inferred from concrete evidence
  (the language they wrote in, then location/nationality/employer country;
  a name alone is not evidence), then cross-checked against the candidate
  profile's Languages so the recipient's language is used when the
  candidate is proficient (native/advanced) and English is only a
  fallback, stated when used. Contacting a native speaker of a language
  the candidate also commands, in English, is called out as a defect.
- [skills/application-writing.md](../skills/application-writing.md): added
  a "Message to a named person" Style Convention alongside the existing
  "Vacancy language" bullet, pointing at the new rule, so the
  person-directed case is visible at the point where prose-to-a-person is
  drafted (the skill already disclaims sending on the candidate's behalf).
Reasoning: The existing language rules all keyed off the posting or the
form UI, which is correct for a CV, cover letter, application answers, or
form fields — but a message to an actual person has a different natural
signal (the recipient), and no rule or skill covered it, so drafting
defaulted to English. The fix lives at the rules level because
person-directed messages are cross-cutting and not owned by a single
skill. The rule stays candidate-agnostic (it references the profile's
Languages generically rather than hardcoding Polish/Russian), per the
playbook/candidate-data separation.
Expected effect: Future outreach drafts to a named person are written in
the recipient's language when the candidate can write it (e.g. Polish to a
Polish contact, given the candidate's native Polish), with English used
only as an explicit shared-language fallback and the agent asking when the
language or proficiency is genuinely unclear — instead of silently
defaulting to English.

## 2026-08-12 — Clarified the verify step's granularity and made the per-candidate notes the home for tool-driving/efficiency detail

Triggered by: [journal/observations.md](observations.md), 2026-08-12 —
"A bulk run's time went mostly to per-field tool round trips; the verify
rule risked being read as per-field." A performance report on a 10-form
bulk run, with a maintainer request to speed up the sweep without
sacrificing accuracy.
Change made:
- [skills/bulk-application-fill.md](../skills/bulk-application-fill.md):
  step 12 now states the verification is **one confirmation of the
  finished form's state** (read the assembled form back once before
  hand-off), not a re-check after every field — and notes a structured
  read-back is both faster and a truer check than a per-field visual
  pass. The "Known Form Quirks" section was broadened to "Known Form
  Quirks and Tool-Driving Notes": it now explicitly houses *how the tools
  are driven for speed* (batching, faster/more-reliable reads, transfer
  method) alongside widget quirks, all recorded per-candidate under
  `work/<candidate>/`, with an explicit reminder that efficiency never
  overrides the step-12 guarantee. Per Operating Principle 2, no tool
  names were added to the shared skill.
- [work/jakub-charabet/job-board-notes.md](../work/jakub-charabet/job-board-notes.md)
  (candidate repo, committed separately): added a "Driving the tools
  efficiently" section (batch independent field-fills/reads into one
  call; prefer structured reads over screenshots, reserving a full
  screenshot for the final confirmation; transfer via the file tools
  per-file, not a shell base64 blob) and two ATS-interaction facts
  (native `<select>` needs a set-value call, not coordinate clicks —
  correcting the stale "no quirks" note on DCG; a React-controlled-input
  platform needs screenshot-before-click + triple-click-select-all).
Reasoning: The speed lived almost entirely in tool mechanics, which
Principle 2 keeps out of the playbook, so the substantive fixes go to the
candidate's notes where such detail already lives. The only playbook-
level defect was step 12's silence on granularity, which invited an
expensive per-field reading of a rule that only requires the finished
state be confirmed once. Fixing the wording captures the speed win at the
process level without weakening the guarantee.
Expected effect: A future bulk run has the tool-driving shortcuts and ATS
quirks on record instead of rediscovering them, and reads step 12 as a
single final confirmation — cutting the per-field screenshot cost that
dominated this run — while re-grounding and verify-before-report stay
fully intact.

## 2026-08-12 — Captured the application-form URL as a first-class field and the strongest dedup key

Triggered by: [journal/observations.md](observations.md), 2026-08-12 —
"Vacancy artifacts recorded only the listing URL, discarding the
application-form URL — the strongest dedup key." A single free-text
`Source:` field captured only the discovery listing; the resolved Apply
target (often a different ATS domain, and sometimes a thin-redirect
listing's only stable identifier) was seen during the bulk sweep and
thrown away.
Change made:
- [templates/vacancy.md](../templates/vacancy.md): replaced the single
  `Source:` header line with a structured **Links** block — listing URL,
  application-form URL (the resolved Apply target when it differs, noted
  as the primary dedup key and the identifier to record when a listing is
  a thin redirect), and an optional employer canonical posting.
- [skills/bulk-application-fill.md](../skills/bulk-application-fill.md):
  step 2 now records the resolved application-form URL in the Links
  block; step 1's dedup check calls out the form URL as the strongest key
  and says to re-check against it once resolved.
- [skills/deduplication.md](../skills/deduplication.md): added "Same
  application-form URL" as the first (strongest) matching heuristic —
  same form URL ⇒ same requisition, no fuzzy comparison — above the
  existing locator/employer/name-variance cases.
- [docs/workflow.md](../docs/workflow.md): the alternate path's triage
  step 2 now notes its dedup check is an initial listing-level pass and
  the form-URL key isn't known until Apply is resolved; step 3 records
  the form URL in the Links block and re-runs the dedup check against it.
Reasoning: The application-form URL is the one identifier that settles
requisition identity deterministically, and it's exactly what the bulk
sweep already surfaces when it resolves the Apply target — but nothing
captured it, so the dedup work landed earlier the same day was left
matching on softer signals. This completes that work: give the URL a
home in the artifact, capture it at the step that already resolves it,
and make it the top dedup key. The check is deliberately two-stage
(listing-level at triage, form-URL once Apply resolves) because the form
URL isn't knowable until the Apply flow is opened.
Expected effect: Every bulk-sweep vacancy records both its listing and
its application-form URL; duplicates that share a form URL but differ in
listing/board/title are caught deterministically; and a thin-redirect
listing that exposes only the final form link still has a stable
identifier on file.

## 2026-08-12 — Made the live pre-filled form a protected, verified deliverable — its tab must stay open, and the fill must be confirmed before it's reported

Triggered by: [journal/observations.md](observations.md), 2026-08-12 —
"Agent reported forms pre-filled after closing their tabs; the pre-fill
was gone and the claim was false." The agent closed three form tabs
after saving their records and reported the postings ready; the
pre-filled forms were unrecoverable and the claim was untrue.
Change made: [skills/bulk-application-fill.md](../skills/bulk-application-fill.md):
- Expected Outputs: the "form left mid-review" bullet now says a
  **live, still-open** tab, and spells out that the form is a separate
  deliverable from the vacancy artifact — the artifact records *what*
  was filled, but the pre-filled form exists only while its tab is open,
  cannot be rebuilt from the artifact, and is destroyed by closing the
  tab.
- Step 11 (checkpoint): added that the record is **not** a substitute
  for the live form, that a pre-filled form's tab must never be closed,
  that checkpointing the record is not permission to close it, and that
  "move on" means opening the next posting in a new tab — not closing the
  filled ones.
- New step 12: "Verify in the browser before reporting a posting
  pre-filled" — never claim a form was filled unless the live browser
  was just checked (fields hold the values, tab still open); a saved
  record is not evidence; report against browser state, not the
  artifact; a false "it's pre-filled" is worse than an honest "I
  couldn't."
- Quality Criteria: added that every pre-filled form is still open in
  its own live tab at hand-off (no tab closed after filling; the
  artifact is never a stand-in), and that a posting is reported
  pre-filled only after the live form is confirmed filled and open.
Reasoning: The 2026-08-12 checkpoint fix correctly made the on-disk
artifact the durable record of *progress*, but its framing ("a browser
tab is not a record") was over-generalized into "the record is the
deliverable, so the tab can go." A pre-filled form is unreconstructable
browser-only state, so the record and the live form are two distinct,
both-required deliverables — and the skill never said so, nor required
the fill to be verified before it was reported. Naming the live form as
protected and adding a browser-state verification step closes both the
lost-work and the false-report failure at once.
Expected effect: A bulk sweep leaves every pre-filled form open in its
own tab for the candidate, never closes a filled tab on the strength of
a saved record, and only reports a posting pre-filled after confirming
the live form actually holds the values — so "I pre-filled them" can no
longer be true on disk and false in the browser.

## 2026-08-12 — Attached deduplication to the bulk sweep and gave it a concrete matching heuristic

Triggered by: [journal/observations.md](observations.md), 2026-08-12 —
"Deduplication was effectively absent from the bulk sweep, and its one
inline check was mis-scoped." The sweep bypasses the discovery agents
that are the only callers of the deduplication skill, the skill an
operator follows during the sweep never mentioned dedup, the dedup skill
didn't know the sweep existed, and the one inline check conflated
"employer already tracked" with "requisition already tracked."
Change made:
- [skills/bulk-application-fill.md](../skills/bulk-application-fill.md):
  added a new Procedure step 1, "Deduplicate before creating anything
  for this posting" — run the deduplication skill against existing
  vacancy artifacts, matched on the *requisition* (not just the
  employer), *before* the form is opened or the checkpoint stub (now
  step 11) is written; renumbered the rest. Added the existing artifact
  set to Required Inputs and a "no duplicate because of a different
  URL/slug/similar-offers link" Quality Criterion. This also fixes an
  ordering risk introduced by the 2026-08-12 checkpoint change (stub
  written "the moment a posting is triaged"): dedup now gates that write
  so the sweep can't mint duplicate stubs.
- [docs/workflow.md](../docs/workflow.md): split the alternate path's
  triage step 2 into two explicit, separate checks — "is this exact
  requisition already tracked?" (via the deduplication skill, before
  creating anything including the step-5 stub) and "is this employer
  already tracked?" — instead of the single conflated sentence.
- [skills/deduplication.md](../skills/deduplication.md): added the bulk
  sweep to "When to Invoke" (per posting, before any artifact/stub,
  noting the sweep bypasses the agents that normally call this skill);
  added a "Matching heuristics" section promoting the now-observed
  patterns (same requisition/different locator; same employer/different
  opening; employer name-variance normalization) out of "Future
  Improvements," which was still deferring heuristics as unobserved.
Reasoning: Dedup was one of the responsibilities the discovery agents
carried, and the bulk sweep was documented as a path that skips those
agents (2026-08-11) without re-attaching dedup to the sweep's own skill
and steps — so it survived only as one mis-scoped inline sentence that
its own text admitted "has recurred and been missed before." Making the
check an explicit first per-posting step, teaching the dedup skill about
the sweep, and writing down the concrete pattern closes the gap the same
way the checkpoint and 1-click fixes did: move the rule out of implicit
practice into the shared, checked documents.
Expected effect: A bulk sweep runs an explicit requisition-level dedup
check on each posting before creating any artifact for it, so the same
posting reached via a different URL, slug, or "similar offers" link
updates the existing artifact instead of spawning a duplicate — and the
check no longer depends on remembering a single sentence buried in a
triage step.

## 2026-08-12 — Required a per-posting durability checkpoint in the bulk sweep so a lost browser can't erase progress

Triggered by: [journal/observations.md](observations.md), 2026-08-11 —
"A bulk sweep lost its browser tabs and, with them, all in-session
progress." Per-posting artifact writes were being deferred toward the
end of the sweep, so the browser tabs were the only record of which
postings had been found and how far each had gotten; losing the tabs
lost all of it.
Change made:
- [skills/bulk-application-fill.md](../skills/bulk-application-fill.md):
  replaced the old "Move on without waiting for 'next'" procedure step
  with "Checkpoint each posting to disk before moving on" — the on-disk
  vacancy artifact is the single source of truth for a posting's
  existence and progress, written as each posting is triaged/pre-filled
  (at minimum a stub with URL, employer, `Status: draft`) and updated in
  place, before the next tab is opened; auto-proceed now follows that
  checkpoint. Added a matching Quality Criterion (every posting touched
  has an on-disk artifact before the next is opened; tabs are never the
  sole record). The step explicitly distinguishes this durability
  checkpoint (persist the file) from git "Commit cadence" (batched per
  unit of work) — the disk write, not the commit, is what survives a
  browser crash.
- [docs/workflow.md](../docs/workflow.md): the alternate path's "Record
  as draft" step now says "as you go, to disk" and requires the stub-
  then-update-in-place write before moving on; "Auto-proceed" now only
  advances once the current posting is checkpointed to disk, so a lost
  session costs at most the posting in hand.
Reasoning: The workflow and skill already produced a per-posting
artifact but never fixed *when* it had to be written relative to
advancing, so batching (correct for git commits) leaked into the disk
write and left the browser as the only durable-feeling record — which it
isn't. Naming the checkpoint and separating it from commit cadence
closes that gap without contradicting the existing commit-batching rule.
Expected effect: A browser tab loss mid-sweep costs at most the single
posting in hand; everything earlier is already on disk and the sweep can
be rebuilt from the vacancy artifacts rather than restarted.

## 2026-08-11 — Documented the bulk job-board sweep as an alternate path, and promoted its field-level rules into a skill

Triggered by: [journal/observations.md](observations.md), 2026-08-11 —
the candidate's recurring bulk-sweep workflow (direct browsing,
lightweight fit judgment, real-form pre-fill via a browser session) had
never been written into the playbook, and its field-level rules lived
only in per-session memory, one of which (1-click Apply handling) had
gone stale by the time it was written down.
Change made: [docs/workflow.md](../docs/workflow.md) gained an
"Alternate path: bulk job-board sweep" section describing the loop
end-to-end (trigger → direct browse → lightweight triage → determine
real form vs. 1-click → pre-fill or set aside → record as draft →
auto-proceed → candidate submits/process records → reconcile at the
end of a sweep), framed explicitly as trading the staged pipeline's
evaluation/matching rigor for speed, and noting a vacancy handled this
way can still graduate into the staged pipeline later. New
[skills/bulk-application-fill.md](../skills/bulk-application-fill.md)
captures the field-level rules this path depends on: always fill a
LinkedIn field, match the form's own UI language, ground per-skill form
answers in the candidate profile (with an explicit non-claim rather
than an invented figure for unconfirmed skills), leave complex
multi-field forms for the candidate, fold "why this fits" framing into
the CV Summary when there's no cover-letter field, never touch consent
checkboxes or the submit control, and — the corrected rule — never
click a genuine 1-click Apply button on the candidate's behalf; set it
aside instead. Board- and ATS-specific detail (which platforms this
candidate's search touches, and quirks specific to each — e.g. a
Greenhouse react-select click-not-type behavior, Traffit's widely
varying form scope) was deliberately kept out of the shared skill and
recorded instead in
[work/jakub-charabet/job-board-notes.md](../work/jakub-charabet/job-board-notes.md),
per the candidate's request to separate general rules from site- or
candidate-specific detail — the skill only notes that such detail
exists and where to find it.
Reasoning: This mirrors the exact lesson already recorded for the
clickable-CV-links fix below (2026-07-17): a rule that only lives in
private, cross-session memory isn't durable the way a playbook
document is, and the fact that the 1-click Apply rule had drifted from
the candidate's actual current preference by the time this session
tried to document it is direct evidence of that gap doing damage in
practice, not just a theoretical risk.
Expected effect: A future session running a bulk job-board sweep — with
or without this specific memory intact — has a documented path to
follow and a single shared place for its field-level rules, so the
1-click-handling mistake (and similar staleness) shouldn't recur
silently.

## 2026-07-17 — Required working-tree/HEAD parity after a manual git-plumbing commit

Triggered by: [journal/observations.md](observations.md),
2026-07-17 — the "safe-commit" git-plumbing workaround (`hash-object`/
`write-tree`/`commit-tree`/ref-move, adopted to route around this
mount's `unlink()` failures) silently desynced the working tree from
git HEAD across five files: the plumbing pattern only writes git's
object database and the ref pointer, never the checked-out file, so
later reads saw stale content while `git show HEAD:<path>` showed the
new content. The pattern's own verification masked it by diffing HEAD
against the same temp file used to build the blob.
Change made: [rules/general.md](../rules/general.md)'s "Tooling note:
bash vs. direct file tools" section gained a paragraph covering the
manual-plumbing commit case: after building such a commit, copy the
exact blob content over the real working-tree file, and verify parity
with `diff <(git show HEAD:<path>) <path>` against the actual file —
never the temp file, which always passes even when the real file is
stale.
Reasoning: The existing "Tooling note" already covered content
diverging between the shell's view and what's actually true, but its
wording ("reads a file, transforms it, and writes it back") assumed a
workaround that writes to the file; the plumbing pattern never writes
to the file at all, only to git's object database, so it fell outside
the rule's plain reading. Naming the pattern explicitly closes that
gap.
Expected effect: A manual-plumbing commit is followed by a
working-tree copy-back and a real-file parity check, so the working
tree can't silently drift from HEAD after a commit built this way, and
the verification step can no longer pass on a stale file.

## 2026-07-17 — Formalized "clickable contact links" into skills/cv-tailoring.md (had recurred)

Triggered by: a direct candidate question in an execution session ("We
forgot to make links clickable. Is it a rule?"), asked after the
Upvanta CV's contact block was rendered with GitHub/LinkedIn as plain
text. This exact feedback was already given once before (2026-07-15,
Xebia Azure CV) but was only ever captured as a private cross-session
memory note ("worth folding into skills/cv-tailoring.md's Style
Conventions next time that file is touched") — never actually written
into the playbook itself, so it recurred the next time a fresh CV was
drafted.
Change made: [skills/cv-tailoring.md](../skills/cv-tailoring.md)'s
existing "Contact line" Style Convention gained a sentence: render
GitHub/LinkedIn/portfolio URLs as clickable markdown links, not bare
text.
Reasoning: A rule that only lives in an agent's private memory isn't
durable across sessions or agents the way a playbook rule is — this is
the same structural lesson as the "outcome" gap earlier today (an
instruction given once needs to land in a shared, checked artifact, not
just be remembered informally).
Expected effect: Future tailored CVs render contact URLs as clickable
links by default; this specific feedback shouldn't need to be given a
third time.

## 2026-07-17 — Added "State the outcome" rule and refined language ordering in skills/cv-tailoring.md

Triggered by: a direct candidate request in an execution session while
reviewing the Upvanta Polish CV ("The typical task - I want the
outcome to be always present... Put English above Russian"). Reviewing
the request also surfaced a real gap: the print-job-visibility
outcome (increased postcard output) had been added to the Megapolis IT
tailored CV by the candidate's own hand-edit, but was never actually
propagated into candidate-profile.md — so it was missing from the
source of truth, not just under-used.
Change made: [skills/cv-tailoring.md](../skills/cv-tailoring.md)'s
Style Conventions gained a "State the outcome, not just the task"
bullet (check candidate-profile.md for a recorded outcome whenever an
achievement/task is included; some outcomes have more than one
recorded framing — pick the one that fits the vacancy). The existing
"Language order" bullet was refined: below the target-market language,
rank English (the candidate's actual professional working language)
above other native languages not tied to the target market. Also
backfilled candidate-profile.md's Manufacturing project entry with the
missing outcome (postcard output / general "factory productivity"
framing) — see the corresponding commit in work/jakub-charabet.
Reasoning: An outcome that only lives in one tailored CV's hand-edit
isn't durable — the next tailored CV for a different vacancy has no
way to find it. Making outcome-inclusion a standing check against
candidate-profile.md (not tailored-CV memory) closes that gap
structurally, not just for this one instance.
Expected effect: Future tailored CVs state outcomes by default and
pull them from candidate-profile.md; language ordering for non-target-
market native languages defaults to professional-usage ranking instead
of a flat native-language tier.

## 2026-07-17 — Added a "Technical achievements/typical tasks and scale" rule to skills/cv-tailoring.md

Triggered by: a direct candidate request in an execution session ("I
want to always include technical achievements/typical tasks and scale
unless stated otherwise"), after this content had previously only been
added to a tailored CV on request (Megapolis IT, following the
candidate's complaint that Work Experience entries were "too brief").
Change made: [skills/cv-tailoring.md](../skills/cv-tailoring.md)'s
Style Conventions gained a "Technical achievements/typical tasks and
scale" bullet: include each project's documented technical
achievement(s)/typical task(s) and scale/load figures by default,
respecting whichever label candidate-profile.md already uses for each
(achievement vs. typical task — don't relabel), omitting only on
explicit candidate instruction for a given vacancy.
Reasoning: What had been a one-off enrichment for a single vacancy
(Megapolis IT) is now the candidate's stated general preference — every
future tailored CV should be full by default, not thin unless asked.
Expected effect: New tailored CVs (and re-tailored existing ones,
starting with Upvanta) include achievements/tasks and scale figures
without the candidate needing to ask each time.

## 2026-07-17 — Added a "Vacancy language" rule to skills/cv-tailoring.md and skills/application-writing.md

Triggered by: a direct candidate request in an execution session
("Respect the vacancy language. Is it a rule already?"), asked while
reviewing the Upvanta vacancy (a Polish posting). It wasn't yet a
rule — the one existing precedent (the Megapolis IT tailored CV,
drafted in Russian, 2026-07-17) was done per one-off explicit
instruction, not a standing default.
Change made: both [skills/cv-tailoring.md](../skills/cv-tailoring.md)
and [skills/application-writing.md](../skills/application-writing.md)
gained a "Vacancy language" Style Convention: draft the tailored CV,
cover letter, and application question responses in the vacancy
posting's own language by default, not English; ask the candidate if
the posting is bilingual or the target language is unclear.
Reasoning: The candidate had already applied this once via explicit
instruction (Megapolis IT); asking whether it was already a standing
rule signals they expect it to apply by default going forward, not to
be re-requested per vacancy.
Expected effect: Future tailored CVs/cover letters for non-English
postings (e.g., Upvanta and other Poland-based Polish-language
postings) are drafted in that language automatically.

## 2026-07-17 — Added a "Presenting artifacts for candidate review" rule to rules/outputs.md

Triggered by: a direct candidate request in an execution session
("Always give a link to the vacancy alongside CV and other artifacts.
Make it a rule") plus the [journal/observations.md](observations.md)
2026-07-15 entry ("Candidate started a one-by-one submission review
pass; wants links included by default...") that had already flagged
this exact gap and predicted it would need formalizing later.
Change made: [rules/outputs.md](../rules/outputs.md)'s "Linking"
section gained a "Presenting artifacts for candidate review"
subsection: whenever a tailored CV, cover letter, application package,
or other artifact is presented for review/decision, always include a
link to the vacancy artifact, and where available the employer
artifact and original posting URL — by default, not only when asked.
Reasoning: The existing "Linking" section only covered link formatting
*within* written artifacts, not what must accompany a chat presentation
of those artifacts. The candidate had already had to ask for this once
per the 2026-07-15 observation; asking a second time later in the
search made clear it should be a standing default, not a one-off
request.
Expected effect: Every future artifact presentation (CV, cover letter,
application package) includes the vacancy link automatically, without
the candidate needing to ask.

## 2026-07-17 — Added a "Draft format and PDF rendering" rule to rules/general.md

Triggered by: a direct maintainer request in a development session (not
a prior observation) — after two tailored-CV PDFs were generated
automatically as part of drafting, the candidate asked for markdown
artifacts they can hand-edit instead, with PDF rendering deferred until
after they approve the .md content, and asked for this to become a
standing rule.
Change made: [rules/general.md](../rules/general.md) gained a "Draft
format and PDF rendering" section, placed directly after "Human review
before anything external" (before "Traceability"). It states that
tailored CVs/cover letters are drafted and reviewed as markdown, that a
PDF should only be rendered once the candidate has approved the
underlying .md content, and that further edits after a PDF exists
should go through the .md source and a re-render, never a hand-edit of
the PDF itself.
Reasoning: The PDF-rendering step (tools/render_cv_pdf.py) had grown
into this candidate's workflow ad hoc, with no rule governing when it
should run — the default in practice had become "render immediately
after drafting," which conflicts with "Human review before anything
external": a PDF is harder to review/edit than markdown, so generating
one before approval works against the review step rather than
supporting it.
Expected effect: Future tailored CV/cover letter work shares the .md
draft first and only produces a PDF once the candidate confirms it's
ready, avoiding wasted renders and keeping the editable source, not a
PDF, as the thing under active review.

## 2026-07-17 — Added a "Commit cadence" rule to rules/general.md

Triggered by: a direct maintainer request in a development session (not
a prior observation) — the candidate found per-artifact commits during
execution sessions too slow and asked for commits to be batched, at
minimum to once per coherent unit of work (e.g., once a vacancy is
wrapped up), with an actual submission always triggering a commit
regardless of other batching.
Change made: [rules/general.md](../rules/general.md) gained a "Commit
cadence" section, placed directly after "Version control and history"
(before "Tooling note: bash vs. direct file tools"). It sharpens the
existing "natural checkpoints" language: the checkpoint is a coherent
unit of work, not each individual edit; an actual submission is always
its own checkpoint; and an early-ending unit of work (e.g., a vacancy
found already filled before tailoring starts) can still be folded into
one commit rather than committed separately. It's explicit that this
changes commit frequency, not whether commits happen.
Reasoning: "Version control and history" already named natural
checkpoints as the commit trigger, but didn't say how large a
checkpoint should be, so the default in practice had drifted to
committing after nearly every artifact edit — correct per the letter
of the existing rule, but slower than the candidate wanted and not
what "natural checkpoint" was meant to convey.
Expected effect: Execution sessions commit noticeably less often —
around once per vacancy/unit of work, plus always on confirmed
submission — without losing the underlying history-preservation intent
of the original rule.

## 2026-07-15 — Made /input the mandatory first stop for facts surfaced mid-session

Triggered by: [journal/observations.md](observations.md), 2026-07-15 —
"A new candidate fact was about to be patched directly into the
profile, bypassing /input."
Change made: [rules/factual-accuracy.md](../rules/factual-accuracy.md)
— added a "New facts surfaced mid-session" section requiring any
candidate statement, however it arises, to be recorded in /input
(typically input/notes.md) before the candidate profile is updated
from it, with the profile update citing the input entry as its source.
Reasoning: The existing rule already named /input as the sole entry
point for candidate facts, but only described the dedicated
profile-building flow — it didn't say what to do when a fact surfaces
organically during unrelated work (tailoring, application review,
etc.), which is exactly when the shortcut of editing the profile
directly is most tempting.
Expected effect: Every candidate fact has a durable record in /input,
independent of the conversation that produced it, regardless of which
task was underway when the candidate mentioned it.

## 2026-07-15 — Genericized candidate- and profession-specific examples out of the reusable playbook

Triggered by: a direct maintainer request (not a prior observation) to
double-check that the playbook — the reusable process, as distinct from
the journal's historical record — contains nothing candidate- or
profession-specific. This also enforces the existing rule in
[docs/operating-principles.md](../docs/operating-principles.md) that the
playbook should not name specific implementation technologies, frameworks,
languages, or (by extension) employers, job boards, or candidates.
Change made:
- [rules/general.md](../rules/general.md): in "Version control and
  history," replaced the `work/jakub-charabet/.git` example with the
  generic `work/<candidate>/` pattern. In "Source liveness," removed named
  job boards and companies (justjoin.it, Teamtailor, hh.ru with Cyrillic
  UI strings, Lever, Luxoft/SuccessFactors, JobLeads, Onwelo) and
  restated the two non-JS-fetch failure modes and the confirmed-live
  signal catalog as platform-agnostic descriptions, pointing to
  [journal/observations.md](observations.md) for the concrete instances.
- [rules/outputs.md](../rules/outputs.md): replaced the `t-bank.md` and
  `hh.ru/vacancy/...` example links with neutral placeholders
  (`acme-corp.md`, `example.com/jobs/...`).
- [skills/cv-tailoring.md](../skills/cv-tailoring.md): generalized the
  contact-line example (dropped GitHub), the language-order example
  (dropped Poland/Polish/Russian), the "solid full-stack developer"
  framing (now "role-agnostic"), and the skills-list example (dropped
  AI-assisted development tools).
Reasoning: Concrete names had accumulated as illustrative examples during
this candidate's IT/region-specific search. They made the rules clearer in
the moment but coupled the reusable playbook to one candidate, one
profession, and one region — the opposite of what the playbook is for, and
a direct violation of operating-principles.md. The underlying lessons were
preserved; only the specifics were removed, with the historical instances
still available in the journal.
Expected effect: The playbook reads as reusable for any candidate,
profession, and region, while the journal retains the specific incidents
that motivated each rule.

## 2026-07-15 — Added a "Recording actual submissions" step, closing the gap after stage 8

Triggered by: [journal/observations.md](observations.md) — "No playbook
step existed for recording an actual submission" (2026-07-15) — the
candidate applied to the Xebia Blazor vacancy directly and reported
back the actual financial expectations stated, the final cover-letter
text (one small edit from the draft), and the actual CV file used, with
nowhere defined in the playbook to file them.
Change made:
- [rules/general.md](../rules/general.md): added a "Recording actual
  submissions" section (after "Source liveness") describing what to do
  when the candidate reports an actual submission — create/update the
  application package to `submitted`, capture the materials actually
  sent (noting any differences from the last draft), record actual
  answers to application questions, and update the vacancy's status to
  `applied`.
- [docs/workflow.md](../docs/workflow.md): extended stage 8's
  description to cover this.
- [agents/application-agent.md](../agents/application-agent.md): added
  a matching responsibility.
- [templates/application.md](../templates/application.md): added
  fields for the actual file submitted, differences from the drafting
  version, actual (not just draft) question answers, and a "date
  submitted" / "attachments actually sent" pair under Submission Notes;
  noted in the template's header comment that it also covers the
  post-submission state, not just pre-submission drafting.
Reasoning: The vacancy template's Status enum already included
`applied` and the application-package template's Status enum already
included `submitted`, so the design anticipated this state — but no
rule or agent responsibility ever drove anything to actually reach it,
since submission itself intentionally happens outside this process
(no agent submits on the candidate's behalf). Without an explicit step,
each real submission would otherwise need this same ad hoc handling
worked out from scratch.
Expected effect: Future reported submissions get filed consistently —
application package created or updated to `submitted`, actual sent
materials preserved distinctly from the drafting history, and the
vacancy status kept in sync — without needing to re-derive where things
belong each time.

## 2026-07-15 — Added a "Version control and history" rule separating execution commits from playbook commits

Triggered by: a direct design decision in a development session (not a
prior observation) — the maintainer wants agents running the process to
commit their changes under `work/<candidate>/` and `input/` so each
candidate's history is preserved, while changes to the playbook itself are
committed only in development sessions.
Change made: [rules/general.md](../rules/general.md) gained a "Version
control and history" section (placed after "Artifact discipline"). It
names the nested-repo layout (playbook repo excludes `work/` and `input/`;
one repo per candidate at `work/<candidate>/`; one repo at `input/`),
defines execution vs. development sessions, and states which repo each
commits to — execution agents commit candidate artifacts to that
directory's own repo and never to the playbook repo; playbook changes go
to the playbook repo with a matching improvements entry. It also covers
the mixed-session case (keep separate commits per repo, surface playbook
changes for review) and the ambiguous case (ask rather than guess).
Reasoning: The infrastructure already existed (`input/.git` and
`work/jakub-charabet/.git` were initialized and committed, and `.gitignore`
excludes both directories), but no rule instructed executing agents to
commit their outputs or warned them off committing the playbook — so the
intended history-keeping behavior would not actually happen. Agents act on
written rules, not on intent recorded only in a conversation.
Expected effect: Execution runs leave a per-candidate commit history of
work product without polluting the shared playbook repo, and playbook
edits stay confined to development sessions.

## 2026-07-14 — Added URL-rot distinction and per-platform confirmed-live signal catalog to the "Source liveness" rule

Triggered by: [journal/observations.md](observations.md) — "Full
JS-rendered re-check of 10 'unconfirmed' vacancies: 9 confirmed live, 1
blocked by a rotted secondary-source URL" (2026-07-14). A full re-check
batch surfaced two gaps in the existing rule once the Claude in Chrome
tool was actually available: it didn't say what to do when a
secondary-sourced vacancy's saved URL 404s (distinct from the listing
itself expiring), and it didn't help an agent recognize what a
genuinely confirmed-live page looks like across different platforms.
Change made: [rules/general.md](../rules/general.md)'s "Source
liveness" section gained two new bullets: (1) a dead URL on a
secondary-sourced vacancy should be recorded as "re-check inconclusive"
rather than `expired`, since URL rot and listing expiry are different
findings; (2) a short catalog of platform-specific confirmed-live
signals (justjoin.it's live countdown, hh.ru's viewer count / absent
archived banner, Lever's persistent Apply button, working ATS
application forms) to help future checks recognize genuine liveness
rather than expecting one universal signal.
Reasoning: Both gaps were concrete, not hypothetical — Onwelo hit the
URL-rot case directly, and the other 9 checks each surfaced a
differently-shaped "live" signal that a future agent might otherwise
second-guess or misread.
Expected effect: Future liveness re-checks correctly separate "source
URL is stale" from "listing is closed," and agents doing a JS-rendered
check know what a positive result actually looks like on common
platforms in this search.

## 2026-07-14 — Generalized the "Source liveness" rule beyond justjoin.it: no non-JS signal proves liveness on any job board

Triggered by: [journal/observations.md](observations.md) — "The non-JS-
fetch liveness problem is general, not justjoin.it-specific, and the
browser fallback wasn't available" (2026-07-14) — a second candidate-
caught false positive (Paysend, on a different platform than the
first).
Change made: [rules/general.md](../rules/general.md)'s "Source
liveness" section now names two independently observed failure modes
(cached countdown text on justjoin.it; client-side-injected closed
state on Teamtailor) and states the rule generally: a page loading
normally, showing an "Apply" button, or showing a future date is never
sufficient evidence of current liveness, on any platform — only a
JS-rendering check or the candidate's direct confirmation counts as
"live," while a past date remains valid evidence of expiry regardless
of platform.
Reasoning: The first fix (this same day, see the entry below) was
scoped to justjoin.it's specific countdown-caching bug. A second,
differently-shaped false positive on a completely different platform
within the same session showed the narrower framing missed the general
principle: client-side JavaScript can hide a closed/expired state from
any non-JS fetch, regardless of whether that board displays a
countdown at all.
Expected effect: Future liveness checks default to "unconfirmed"
unless independently rendered or candidate-confirmed, regardless of
which job board is involved — this session's pipeline-overview.md and
all affected vacancy artifacts were updated accordingly as the first
application of this tightened rule.

## 2026-07-14 — Tightened the "Source liveness" rule: a non-JS page fetch can prove expiry but not liveness

Triggered by: [journal/observations.md](observations.md) — "A 'live'
liveness check was wrong: non-JS page fetches can't be trusted on
justjoin.it" (2026-07-14) — the candidate caught a vacancy marked
"re-verified live" that was actually expired.
Change made: [rules/general.md](../rules/general.md)'s "Source
liveness" section now explicitly states that a non-JS page fetch is
not sufficient evidence of current liveness (a job board can serve a
cached snapshot with a stale "days left" countdown), while a past date
in that same countdown remains valid evidence of expiry regardless of
caching. Agents should prefer a JS-rendering check or direct candidate
confirmation before recording a listing as "live," and otherwise
record it as unconfirmed rather than live.
Reasoning: The asymmetry matters — a stale snapshot can only make a
listing look *more* alive than it really is (an old "days left" from
before closure), never less, so past-date conclusions stay valid while
future-date conclusions don't.
Expected effect: Future "live" claims either come from a real
JS-rendered check, candidate confirmation, or are explicitly labeled
as unconfirmed — this specific false-positive pattern shouldn't recur
silently.

## 2026-07-14 — Added write-verification, bash-tooling, and source-liveness rules to rules/general.md; added timestamps and an Availability Checks section to templates/vacancy.md

Triggered by: [journal/observations.md](observations.md) — "decision-log.md
and 15 vacancy artifacts were silently truncated a second time"
(2026-07-14), and the candidate's direct report that 2-3 of the
top-ranked vacancies turned out to be expired when checked manually.
Change made:
- [rules/general.md](../rules/general.md): extended "Artifact
  discipline" to require time-of-day on time-sensitive facts and a
  post-write verification step; added a new "Tooling note: bash vs.
  direct file tools" section documenting the confirmed bash-mount
  staleness issue and instructing agents to prefer direct file tools
  for read-modify-write work; added a new "Source liveness" section
  requiring a dated, timed re-check of external listings whenever a
  vacancy artifact is touched again for substantive work, with status
  updated to `expired` (not deleted) when a listing is found dead.
- [templates/vacancy.md](../templates/vacancy.md): added `expired` to
  the Status enum, added time-of-day to "Last updated" and "Date
  discovered," and added a new "Availability Checks" section for
  logging each re-check.
Reasoning: Two independent problems surfaced together: (1) artifacts
were silently reverting to stale content, traced to a bash/direct-tool
filesystem mismatch; (2) vacancy artifacts only recorded a discovery
date, so there was no structural prompt to re-verify a listing was
still live before relying on it later in the process, and no place to
record that a listing had gone stale between discovery and use.
Expected effect: Future artifact writes get verified immediately
rather than discovered broken stages later; bulk or repeated edits to
this project's files go through the direct file tools; and vacancy
artifacts carry a visible, timestamped history of liveness checks so
"is this still open?" doesn't have to be re-derived from memory.

## 2026-07-14 — Added a "Linking" rule to rules/outputs.md

Triggered by: [journal/observations.md](observations.md) — "Internal/
external references were plain text, not links, by default"
(2026-07-14), and the candidate's direct request to make all internal
and external references clickable.
Change made: Added a "Linking" section to
[rules/outputs.md](../rules/outputs.md) instructing agents to render
internal cross-references and external URLs as markdown links at the
point of writing, with one example of each form.
Reasoning: Roughly 60 artifacts across this candidate's working
directory had accumulated plain-text path/URL references because no
rule addressed link formatting; fixing it after the fact required a
manual pass across every file. Making linking a standing expectation
prevents the same gap from recurring for future candidates or later
artifacts in this one.
Expected effect: New artifacts produced by any agent should link
internal and external references from the start, without needing a
candidate to ask for a cleanup pass.

## 2026-10-01 — Made interview recording silent

Triggered by: [journal/observations.md](observations.md) — "Interviewer
narrated its record-keeping to the candidate" (2026-10-01).
Change made: Added a "Recording is silent" paragraph to step 4 of
[skills/mock-interviewing.md](../skills/mock-interviewing.md) and a
matching failure mode to
[agents/interviewer-agent.md](../agents/interviewer-agent.md).
Reasoning: Recording as you go is required so an interrupted session
loses nothing, but announcing each write turns the interviewer back
into an assistant mid-interview.
Expected effect: Interview turns contain only the question, probe, or
follow-up; file writes still happen after every exchange.

## 2026-10-01 — Fixed question scopes and coverage-based scoring

Triggered by: [journal/observations.md](observations.md) — "Mock
interview scores weren't comparable between sessions" (2026-10-01), and
the candidate's request that each question's scope be defined.
Change made:
- [skills/interview-question-design.md](../skills/interview-question-design.md)
  and [templates/question-bank.md](../templates/question-bank.md): every
  question has a fixed scope — numbered scored key points, one to three
  required follow-ups (each with its own key points), optional "out of
  scope," and a scope version raised on any change.
- [skills/mock-interviewing.md](../skills/mock-interviewing.md) and
  [agents/interviewer-agent.md](../agents/interviewer-agent.md): ask the
  main question and every required follow-up as written; at most two
  neutral probes per question that never steer toward a key point; no
  follow-ups outside the scope; difficulty adapts between sessions only.
- [skills/interview-evaluation.md](../skills/interview-evaluation.md):
  mark each key point covered / partial / missed / wrong, score from
  coverage (under 25% → 1 … 100% → 5), with caps for wrong key points
  and hints; anything outside the scope is noted, not scored.
- [skills/practice-tracking.md](../skills/practice-tracking.md): question
  history records the scope version, and scores are only compared
  within the same version.
- [templates/mock-interview-session.md](../templates/mock-interview-session.md):
  plan carries the scope version, transcript tags `[F1]` / `[probe]`,
  evaluation has a per-key-point table and coverage.
- The candidate's bank was converted to scope version 1 (all 47
  questions) and past scores in the practice profile marked version 0.
Reasoning: The candidate wants results that compare between sessions.
A fixed scope plus mechanical scoring from key-point coverage means a
score change reflects the answer, not what the interviewer chose to
ask that day.
Expected effect: Re-asks of a question test the same thing; scores and
trends per question are comparable within a scope version. Trade-off:
less improvisation, so a vague answer is challenged only within two
neutral probes.

## 2026-10-01 — Spaced re-asks by score and a default session mix

Triggered by: [journal/observations.md](observations.md) — "No rule for
repeating questions scored 3, or for mixing due and new questions"
(2026-10-01), and the candidate's approval of both changes.
Change made:
- [skills/practice-tracking.md](../skills/practice-tracking.md): a
  question is due again 2 sessions after a 1–2, 4 after a 3, 8 after a
  4, and never after a 5; a due question that isn't asked keeps its
  due session and becomes overdue. Sessions default to half due
  questions (rounded up) and half new; when too many are due, most
  overdue then lowest score go first and the rest carry over.
- [skills/mock-interviewing.md](../skills/mock-interviewing.md): planning
  order follows that mix.
- [templates/practice-profile.md](../templates/practice-profile.md):
  "Session mix" line in Next Session Focus; question history records
  scope version, session number, and the session a question is due.
- The candidate's practice profile was recomputed under the new rule.
Reasoning: Scores of 3 mean the depth isn't there yet, so they need a
retest; a fixed mix keeps new material flowing even after a weak
session, and an overdue-first queue stops due questions slipping
indefinitely.
Expected effect: Every question below 5 comes back on a predictable
schedule, and each session's plan states its due/new split.

## 2026-10-01 — Coverage window for the question bank

Triggered by: [journal/observations.md](observations.md) — "Nothing
guaranteed every bank question gets asked" (2026-10-01), and the
candidate's choice of 4 sessions at 8 questions each.
Change made:
- [skills/practice-tracking.md](../skills/practice-tracking.md):
  "Coverage window" — every active bank question is asked within 4
  sessions of being added (sessions 6–9 for the current backlog); the
  session mix sets new slots to keep that pace (at least half the
  session, at least 3 slots left for due questions), offers a longer
  session if the pace can't be met, and runs shorter sessions once the
  bank is exhausted. "Choosing new questions" puts never-asked topics
  first and uses the closest difficulty level instead of skipping a
  topic.
- [skills/mock-interviewing.md](../skills/mock-interviewing.md):
  planning order and difficulty fallback updated to match.
- [templates/practice-profile.md](../templates/practice-profile.md):
  "Coverage" line in Next Session Focus.
- The candidate's practice profile: coverage plan for sessions 6–9 and
  the missing Estimation topic row.
Reasoning: The candidate wants the whole bank covered in a reasonable
time; a fixed window makes that a scheduled outcome rather than
something that depends on how each focus is written.
Expected effect: All 47 questions asked by session 9. Trade-off: due
re-asks get only 3 slots per session during the window, so a backlog
builds up and is cleared in the sessions after it.

## 2026-10-02 — Follow-ups keep their scope but adapt their wording

Triggered by: [observations.md](observations.md), "2026-10-02 —
Fixed follow-ups felt rigid and abstract."
Change made: The interview step in
[skills/mock-interviewing.md](../skills/mock-interviewing.md) now
fixes what each follow-up tests, not its words. The interviewer
bridges into a follow-up from the candidate's answer, narrows a partly
covered follow-up (`[F2 narrowed]`), falls back to a hypothetical when
a follow-up's premise doesn't hold, asks probes that name what the
candidate said, gives a small concrete setup when asking for an
example, and answers questions about the process in role. Matching
responsibilities and failure modes are in
[agents/interviewer-agent.md](../agents/interviewer-agent.md). Each
follow-up gets a `Tests:` line, plus concreteness, no-overlap, and
hypothetical-fallback criteria, in
[skills/interview-question-design.md](../skills/interview-question-design.md)
and [templates/question-bank.md](../templates/question-bank.md).
Rewording without changing what a follow-up tests no longer raises
the scope version
([agents/interview-question-agent.md](../agents/interview-question-agent.md)).
The `[F2 narrowed]` marker is added in
[templates/mock-interview-session.md](../templates/mock-interview-session.md).
Reasoning: Scores stay comparable because they come from key-point
coverage, not from the exact words of the follow-up. Fixing the words
added nothing to comparability and made the interviewer sound
scripted.
Expected effect: Follow-ups read as a reaction to the answer. Nothing
already answered gets asked again, and every probe is specific enough
to answer. Scores are still compared at the same scope version.

## 2026-10-08 — Probes are conditional, not a quota

Triggered by: [observations.md](observations.md), "2026-10-08 —
Every question seemed to get exactly three follow-ups."
Change made: In [skills/mock-interviewing.md](../skills/mock-interviewing.md),
neutral probes are now used only when an answer is vague, skips over
something the candidate raised, or makes a claim worth testing. Zero
probes is the normal case, and two is a limit, not a target. A new
"Moving on" step sends the interviewer to the next main question once
the scope is covered. The quality criteria require a reason for every
probe and an exchange count that varies with the answers.
[agents/interviewer-agent.md](../agents/interviewer-agent.md) matches
this and adds "filling a quota" as a failure mode.
Reasoning: Scores come from the required follow-ups and key points,
and those don't change. Probes only get the candidate to expand, so
probing a complete answer adds turns without adding signal.
Expected effect: Questions get different numbers of exchanges: a
strong answer moves on quickly, and a vague one gets probed. No scope
version changes.

## 2026-10-09 — Key points score the idea, not the API name

Triggered by: [observations.md](observations.md), "2026-10-09 —
Evaluation read as a test of exact method names."
Change made: [skills/interview-evaluation.md](../skills/interview-evaluation.md)
gets a "Mark the idea, not the name" rule. A correct mechanism without
the name, or with a near-miss name, is covered. A name with no
mechanism is at most partial. An invented API that changes the design
is judged as a wrong claim. Name slips go to a new per-answer "Names to
learn" line that doesn't affect the score. Top priorities rank design
gaps above name recall.
[templates/mock-interview-session.md](../templates/mock-interview-session.md)
adds the "Names to learn" line, and
[agents/interview-evaluation-agent.md](../agents/interview-evaluation-agent.md)
adds marking down a correct mechanism for a missing name as a failure
mode. [skills/interview-question-design.md](../skills/interview-question-design.md)
asks for key points to state the idea first, with the name in brackets.
Reasoning: Real technical interviews reward understanding and treat a
half-remembered name as a lookup. Scoring names made practice scores
both stricter than a real interview and misleading about what to study.
Expected effect: Scores reflect what an interviewer would credit, names
remain on the study list, and priorities point at real gaps. No bank
scope versions change: key points still test the same ideas, but they
are read differently. Scores from sessions evaluated before this date
were marked under the older reading.
