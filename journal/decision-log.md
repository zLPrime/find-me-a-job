# Decision Log (Process-Level)

A chronological log of consequential decisions made **about the playbook
itself** — design choices, tradeoffs, and the reasoning behind them. This
is distinct from per-candidate decision log entries (matches, employer
evaluations), which live alongside the relevant artifacts in
[/work](../work) and follow the structure in
[templates/decision-log.md](../templates/decision-log.md).

## How to add an entry

Append a new entry at the top, using the structure from
[templates/decision-log.md](../templates/decision-log.md), adapted to a
process/design decision rather than a candidate-facing one:

```markdown
## <date> — <short title>

Decision: <what was decided about the repository/process structure>
Alternatives considered: <other options and why they were set aside>
Reasoning: <why this option was chosen>
Revisit trigger: <what would prompt reconsidering this decision>
```

## Entries

## 2026-09-25 — Interview practice as a parallel track with a separate interviewer and evaluator

Decision: Add interview practice as a parallel track (not a numbered
pipeline stage) with four agents: question building, interviewing,
evaluation, and progress tracking. The interviewer never grades; the
evaluator works from the recorded transcript alone. Practice memory
lives in a practice profile kept separate from the candidate profile.
Alternatives considered: A single "mock interviewer" agent that asks,
grades, and remembers (simpler, but an interviewer that also grades
drifts into coaching mid-interview and grades its own conversation
generously); folding practice scores into the candidate profile
(rejected: practice performance is a judgment, not a candidate fact,
and must never leak into matching or tailoring); a numbered stage 10
(rejected: practice runs repeatedly and alongside the pipeline, not
once in sequence).
Reasoning: Keeps each responsibility traceable, per Principle 3 in
[docs/operating-principles.md](../docs/operating-principles.md), and
makes the evaluator's independence structural rather than a matter of
prompt discipline.
Revisit trigger: If evaluating in a separate step proves too slow to
be worth it in practice, or if evaluation scores prove unreliable
without the interviewer's context.

## 2026-07-14 — Initial repository structure and agent boundaries

Decision: Organize the playbook as small, single-responsibility agents
(profile, company discovery, vacancy discovery, employer evaluation,
matching, tailoring, application, reporting) coordinated by a thin
orchestrator, with shared rules and reusable skills rather than
per-agent duplicated instructions.

Alternatives considered: A single comprehensive "job search assistant"
prompt covering the whole process; a stage-based (rather than
responsibility-based) agent split.

Reasoning: A single comprehensive agent tends to blur accountability and
makes it hard to trace why an artifact turned out a certain way.
Responsibility-based agents keep each piece of reasoning traceable to one
place and let skills/rules be improved independently of any one agent.

Revisit trigger: If, in practice, agents frequently need to duplicate
each other's reasoning or hand off so much context that the boundaries
feel arbitrary, reconsider the split.
