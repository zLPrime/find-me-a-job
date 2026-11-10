# Template: Elicitation Session

> Structural template only. One artifact per session. The
> [elicitation-agent](../agents/elicitation-agent.md) writes everything
> here and sets status up to `awaiting mapping`; only the
> [concept-mapping-agent](../agents/concept-mapping-agent.md) sets
> `mapped`, after the concept mapping's change note cites this session.

```markdown
# Elicitation — <topic> — <project> — <date>

Status: planned | in progress | awaiting mapping | mapped | abandoned
Last updated: <date and time>
Internal only: practice material, never sent to anyone.
Topic map: <link>
Project: <project name as the candidate profile states it, and the part
  covered in this session, if not the whole project>
Language: <language>

## Plan

Prepared by: elicitation-agent

| # | Concept ID | Weight | Status before | Why selected |
|---|---|---|---|---|
| 1 | <C-nn> | <weight> | unexplored / partial | <high unexplored / sent back by mapping / partial> |

## Transcript

Prepared by: elicitation-agent

### 1. <C-nn> — <concept>

**Interviewer:** `[P2]` <prompt as actually asked>

**Candidate:** <answer in the candidate's own words>

**Interviewer:** `[specifics]` <follow-up naming what the candidate
said>

**Candidate:** <answer>

<`[also touches C-nn]` — evidence for another concept, noted, not
chased.>

## Coverage

Prepared by: elicitation-agent

| Concept ID | Concept | Status | Where (transcript section) |
|---|---|---|---|
| <C-nn> | <concept> | unexplored / covered / partial / absent (<why it never came up>) / contradicted | <#> |

## Facts Recorded

- <one line per fact> — input/notes.md, entry of <date>

## Study Topics Surfaced

- <topic, with context — recorded in study-topics.md, or "none">
```
