# Template: Question Bank

> Structural template only — no real questions for a real target.
> Illustrative examples must be clearly labeled per
> [examples/README.md](../examples/README.md).

```markdown
# Question Bank — <target: role title at employer, or role type> (<seniority>)

Status: active | retired
Last updated: <date>
Prepared by: interview-question-agent
Internal only: practice material, never sent to anyone.
Target: <link to the vacancy artifact, or the role type>
Linked prep notes: <links to interview prep notes, if any>
Interview language: <language the real interview is held in>
Change note: <what was added or retired in this version, and why>

## Difficulty scale

1 — fundamentals; 2 — working knowledge; 3 — solid practitioner;
4 — senior: trade-offs, internals, failure modes;
5 — expert: design under competing constraints, deep internals.

## Question scope

Each question's scope is fixed so its scores compare across sessions:
the main question, its required follow-ups, and the key points (K1, K2,
…) scored against them. Key points are numbered across the main
question and its follow-ups. What each follow-up tests is fixed; its
wording adapts to the conversation. Any change to what the question or
its follow-ups test, or to the key points, raises the scope version; see
[skills/interview-question-design.md](../skills/interview-question-design.md),
"Question scope."

## Topics

| Topic | Source | Weight |
|---|---|---|
| <topic> | <vacancy requirement / profile fact / prep-note signal / standard coverage> | high / medium / low |

## Questions

### <Topic>

#### <ID, e.g. Q-001> — <short title>

- Difficulty: <1–5>
- Type: conceptual | experience-based | scenario | design discussion
- Scope version: <n> (<date>: <what changed>)
- Question: <as the interviewer would ask it>
- Key points (scored):
  - K1: <specific, checkable point>
- Required follow-ups (always covered; wording adapts, what they test
  doesn't):
  - F1: <default wording, concrete: a situation, symptom, or number to
    reason about — trade-offs, failure modes, scale, alternatives>
    - Tests: <one line: what this follow-up checks>
    - K<n>: <key point this follow-up tests>
- Out of scope: <optional — nearby topics this question does not test>
- Grounded in: <profile fact, for experience-based questions only>
- Status: active | retired (<reason>)

## Open Questions

- <anything uncertain about the target's interview format or focus>
```
