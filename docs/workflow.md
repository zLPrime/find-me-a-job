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
3. Discover employers
        ↓
4. Discover vacancies
        ↓
5. Evaluate employers
        ↓
6. Match opportunities
        ↓
7. Prepare tailored materials
        ↓
8. Prepare application guidance
        ↓
9. Generate reports
        ↓
10. Collect observations
        ↓
11. Improve the playbook
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

### 3. Discover employers

The [company-discovery-agent](../agents/company-discovery-agent.md)
identifies employers that plausibly fit the candidate's profile and
stated preferences, producing candidate employer entries using the
[employer template](../templates/employer.md).

### 4. Discover vacancies

The [vacancy-discovery-agent](../agents/vacancy-discovery-agent.md) finds
open vacancies, either at discovered employers or independently, and
records them with the [vacancy template](../templates/vacancy.md).

### 5. Evaluate employers

The [employer-evaluation-agent](../agents/employer-evaluation-agent.md)
assesses discovered (or candidate-supplied) employers against criteria
that matter to this candidate — using the
[employer-analysis](../skills/employer-analysis.md) skill — and records
findings and open questions on the employer artifact.

### 6. Match opportunities

The [matching-agent](../agents/matching-agent.md) compares the candidate
profile against evaluated employers and vacancies using the
[matching](../skills/matching.md) skill, producing ranked, reasoned match
decisions recorded in the [decision log](../templates/decision-log.md).

### 7. Prepare tailored materials

The [tailoring-agent](../agents/tailoring-agent.md) produces a tailored
CV and supporting materials for a specific matched vacancy using the
[cv-tailoring](../skills/cv-tailoring.md) skill — strictly from facts
already present in the candidate profile.

### 8. Prepare application guidance

The [application-agent](../agents/application-agent.md) assembles the
full [application package](../templates/application.md) (cover letter,
answers to application questions, submission notes) using the
[application-writing](../skills/application-writing.md) skill, and
routes it for candidate approval before anything is considered ready to
send.

### 9. Generate reports

The [reporting-agent](../agents/reporting-agent.md) summarizes progress,
pipeline status, and outcomes for the candidate using the
[report-generation](../skills/report-generation.md) skill, producing a
[report](../templates/report.md).

### 10. Collect observations

Any agent, at any stage, may record an observation — a gap, a surprising
result, a candidate correction — in [journal/observations.md](../journal/observations.md).

### 11. Improve the playbook

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
