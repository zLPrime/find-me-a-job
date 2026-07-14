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
