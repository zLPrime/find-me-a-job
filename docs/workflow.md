# Workflow

This document describes the job search process at a business level: what
happens, in roughly what order, and which agents and artifacts are
involved at each stage. It is a map of the process, not a rigid pipeline —
stages can repeat, run out of order, or loop back as new information
arrives.

## Stages

```text
1. Receive candidate materials
        ↓
2. Build candidate profile
        ↓
3. Explore fitting role types
        ↓
4. Discover employers
        ↓
5. Discover vacancies
        ↓
6. Evaluate employers
        ↓
7. Match opportunities
        ↓
8. Prepare tailored materials
        ↓
9. Prepare application guidance
        ↓
10. Generate reports
        ↓
11. Collect observations
        ↓
12. Improve the playbook
```

### 1. Receive candidate materials

The candidate supplies source materials (CV, LinkedIn export, notes,
target preferences) into [/input](../input). This is the only entry point
for factual candidate information. See [rules/factual-accuracy.md](../rules/factual-accuracy.md).

### 2. Build candidate profile

The [profile-agent](../agents/profile-agent.md) uses the
[profile-analysis](../skills/profile-analysis.md) skill to turn raw
materials into a structured [candidate profile](../templates/candidate-profile.md).
This profile becomes the reference point for every later stage.

### 3. Explore fitting role types

The [role-discovery-agent](../agents/role-discovery-agent.md) uses the
[role-discovery](../skills/role-discovery.md) skill to identify the *types
of role* the candidate is genuinely qualified for — including adjacent or
transferable ones they may be overlooking — ranked with honest,
explicitly-hedged demand/response estimates. This widens what the next two
stages search for, so discovery isn't limited to the single title the
candidate first named. It runs on the candidate profile alone; no specific
employer or posting is involved yet.

### 4. Discover employers

The [company-discovery-agent](../agents/company-discovery-agent.md)
identifies employers that plausibly fit the candidate's profile, stated
preferences, and the role types from the previous stage, producing
candidate employer entries using the
[employer template](../templates/employer.md).

### 5. Discover vacancies

The [vacancy-discovery-agent](../agents/vacancy-discovery-agent.md) finds
open vacancies — across those same role types — either at discovered
employers or independently, and records them with the
[vacancy template](../templates/vacancy.md).

### 6. Evaluate employers

The [employer-evaluation-agent](../agents/employer-evaluation-agent.md)
assesses discovered (or candidate-supplied) employers against criteria
that matter to this candidate — using the
[employer-analysis](../skills/employer-analysis.md) skill — and records
findings and open questions on the employer artifact.

### 7. Match opportunities

The [matching-agent](../agents/matching-agent.md) compares the candidate
profile against evaluated employers and vacancies using the
[matching](../skills/matching.md) skill, producing ranked, reasoned match
decisions recorded in the [decision log](../templates/decision-log.md).
Matching also runs a keyword/terminology gap check, separating skills the
candidate genuinely holds but the CV words differently (for honest
alignment in the next stage) from keywords the candidate simply lacks
(recorded as gaps, never papered over).

### 8. Prepare tailored materials

The [tailoring-agent](../agents/tailoring-agent.md) produces a tailored
CV and supporting materials for a specific matched vacancy using the
[cv-tailoring](../skills/cv-tailoring.md) skill — strictly from facts
already present in the candidate profile, with action-verb, results-first,
ATS-parseable content and honest terminology alignment to the posting.

### 9. Prepare application guidance

The [application-agent](../agents/application-agent.md) assembles the
full [application package](../templates/application.md) (cover letter,
answers to application questions, submission notes) using the
[application-writing](../skills/application-writing.md) skill, and
routes it for candidate approval before anything is considered ready to
send. The same agent also drafts the person-directed messages that go
alongside an application — a recruiter/contact outreach note or a
follow-up — using the
[outreach-messaging](../skills/outreach-messaging.md) skill, for the
candidate to review and send themselves.

Once the candidate reports they've actually submitted — whether
through this package or by applying directly with a standalone tailored
CV and cover letter — the application package is created (if it doesn't
exist yet) or updated to `submitted` status, recording the materials
actually sent and the vacancy's status updated to `applied`. See
rules/general.md's "Recording actual submissions."

### 10. Generate reports

The [reporting-agent](../agents/reporting-agent.md) summarizes progress,
pipeline status, and outcomes for the candidate using the
[report-generation](../skills/report-generation.md) skill, producing a
[report](../templates/report.md). When the candidate wants direction on how
to run the search rather than just where it stands, the same agent uses the
[search-strategy](../skills/search-strategy.md) skill to recommend
application volume/cadence, how to tier tailoring effort across
opportunities (including when to use the bulk sweep below versus the full
staged pipeline), and follow-up timing — all as adjustable suggestions, not
targets.

### 11. Collect observations

Any agent, at any stage, may record an observation — a gap, a surprising
result, a candidate correction — in [journal/observations.md](../journal/observations.md).

### 12. Improve the playbook

Observations are periodically reviewed and, where warranted, turned into
concrete edits to agents, skills, rules, or templates, tracked in
[journal/improvements.md](../journal/improvements.md).

## This is not a strict pipeline

In practice:

- Employer discovery and vacancy discovery often interleave or run in
  either order.
- New information (e.g., a candidate rules out an industry) can send the
  process back to profile or discovery stages.
- Evaluation and matching may run multiple times as new vacancies appear.
- Reporting can happen at any point the candidate wants a status update,
  not only at the end.

The [orchestrator](../agents/orchestrator.md) is responsible for
sequencing real work across these stages and deciding when to loop back,
but it does so by invoking the specialized agents above — it does not
perform their work itself.

## Alternate path: bulk job-board sweep

Alongside the staged pipeline above, the candidate frequently drives a
second, lighter-weight path directly: a bulk sweep of a job board's
listing pages, filtered and sorted however the candidate specifies.
This path intentionally trades the pipeline's evaluation/matching rigor
and decision-log traceability for speed across a high volume of
postings in one sitting. It reuses the same [vacancy
template](../templates/vacancy.md) and status vocabulary as the staged
pipeline, so a vacancy handled this way can still graduate into the
staged pipeline later — e.g., if it needs a genuinely tailored CV, or a
formal employer evaluation before the candidate commits further. See
[skills/bulk-application-fill.md](../skills/bulk-application-fill.md)
for the field-level and form-handling rules this path follows, and
`work/<candidate>/` for any board- or ATS-specific notes accumulated
while using it (see [work/README.md](../work/README.md)) — this
document and the skill stay general on purpose; which job boards or
application platforms a given candidate's search actually touches is
candidate-specific detail, not playbook content.

0. **Trigger.** The candidate initiates directly ("browse X job board,
   category Y, remote, sorted newest") rather than the orchestrator
   sequencing through company-discovery-agent or vacancy-discovery-agent.
1. **Direct browse.** A live, JavaScript-rendering browser session
   (Claude in Chrome) works through postings in the batch directly,
   rather than routing through vacancy-discovery-agent's more formal
   capture. See [rules/general.md](../rules/general.md)'s "Source
   liveness" section — a non-JS fetch is never sufficient here.
2. **Lightweight triage per posting.** For each listing, first run two
   distinct checks — don't conflate them:
   - *Is this exact requisition already tracked?* The same posting
     recurs under a different board URL, slug, or hash, or resurfaces
     through a job board's "similar offers" carousel — this has been
     missed before. Check the posting against existing vacancy artifacts
     via the [deduplication](../skills/deduplication.md) skill *before*
     creating anything (including the checkpoint stub in step 5); if it's
     already tracked, update that artifact instead of opening a second
     one. This is an initial check on the listing; the strongest key —
     the application-form URL — only becomes known once Apply is resolved
     (step 3), so re-run the check against it then.
   - *Is this employer already tracked?* A distinct opening at an
     already-tracked employer is kept as its own vacancy, clearly
     distinguished from the employer's other requisitions — same
     employer is not the same posting.

   Then judge fit directly against the [candidate
   profile](../templates/candidate-profile.md) — skipping
   employer-evaluation-agent and matching-agent's formal scoring. Hard
   blockers (a residency requirement, an unusual on-call commitment, an
   unconfirmed skill gate) are flagged inline on the vacancy artifact
   rather than escalated through decision-log formality.
3. **Determine the real application path — and record the form URL.**
   Click Apply and confirm whether it opens a real external application
   form (hosted by whatever ATS or company site the employer uses) or a
   genuine 1-click widget — record this explicitly on the artifact, since
   it has been misjudged in both directions before. Capture the resolved
   application-form URL in the artifact's Links block (see
   [templates/vacancy.md](../templates/vacancy.md)); it's often the only
   stable identifier when the listing is a thin redirect. Now that it's
   known, re-run the requisition dedup check (step 2) against it — the
   form URL is the strongest key, so a match here catches a duplicate the
   listing-level check missed.
   - **Real form:** proceed to pre-fill (next step).
   - **Genuine 1-click widget:** do not click it. A true 1-click flow
     submits instantly with no review step, unlike a pre-filled form
     the candidate can still check before pressing submit — so there's
     no safe "pre-fill now, let the candidate confirm later" for a
     1-click posting. Set it aside as an open, candidate-actionable
     item (e.g. "1-click Apply available, not yet clicked") and move on.
     Only click through if the candidate explicitly asks.
4. **Pre-fill, don't submit.** For real forms: fill directly via browser
   tools — name/email/phone/LinkedIn/CV upload attempt, plus
   form-specific free text (financial expectations, availability,
   per-skill experience) — grounded strictly in the candidate profile,
   matching the form's own UI language. Complex multi-field forms, or
   fields needing the candidate's own judgment call, are left for them.
   GDPR/consent checkboxes and the final submit button are always left
   untouched, per "Human review before anything external" in
   [rules/general.md](../rules/general.md).
5. **Record as draft — as you go, to disk.** The vacancy artifact gets
   `Status: draft (pre-filled, awaiting candidate review — not
   submitted)`, documenting what was filled, what was deliberately left
   blank and why, and any open questions for the candidate to weigh.
   Write it *as each posting is handled*, before moving to the next — a
   browser tab is never the sole record of a posting's existence or
   state. A posting gets at least a stub artifact (URL, employer,
   `Status: draft`) the moment it's triaged, updated in place as the
   pre-fill proceeds, so a lost browser session can be rebuilt from disk
   rather than starting over.
6. **Auto-proceed.** Move to the next posting in the batch without
   waiting for an explicit "next" — surface a running list of drafts and
   flag decisions inline rather than blocking on confirmation. Only
   advance once the current posting is checkpointed to disk (step 5), so
   a lost browser session costs at most the posting in hand, not the
   whole sweep.
7. **Candidate submits, the process records.** When the candidate
   reports a posting sent — sometimes with a correction, like a revised
   rate — log any new fact to `input/notes.md` first (see
   rules/general.md's "Recording actual submissions" and the profile
   stage above), then update the vacancy status to `applied (submitted
   by candidate, <date>)` with the actual values sent, and commit to the
   candidate's own repo at that checkpoint per "Commit cadence."
8. **Reconcile at the end of a sweep.** Cross-check open tabs or
   discovered postings against tracked vacancy files to catch anything
   found but not yet actioned (including 1-click listings set aside at
   step 3), and report what's fully wrapped up versus still open.
