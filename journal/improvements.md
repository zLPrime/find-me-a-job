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
