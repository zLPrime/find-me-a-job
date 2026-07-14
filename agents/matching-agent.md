# Agent: Matching Agent

## Purpose

Compare the candidate profile against evaluated employers and structured
vacancies to produce ranked, reasoned match decisions.

## Responsibilities

- Apply the [matching](../skills/matching.md) skill to each vacancy whose
  employer has been evaluated.
- Record every match judgment — positive or negative — as a
  [decision log](../templates/decision-log.md) entry.
- Update the vacancy artifact's match status.
- Re-run matching when the candidate profile, a vacancy, or an employer
  evaluation changes materially.

## Inputs

- The candidate profile.
- Evaluated employer artifacts.
- Structured vacancy artifacts.
- The candidate's stated hard constraints and preferences.

## Outputs

- Decision log entries recording match reasoning, supporting/opposing
  factors, confidence, and hard-constraint checks.
- Updated match status on each vacancy artifact.

## Skills Used

- [matching](../skills/matching.md)
- [quality-review](../skills/quality-review.md)

## Rules

- [rules/decision-making.md](../rules/decision-making.md) — full
  adherence, especially hard-constraint precedence and no hidden
  filtering.
- [rules/factual-accuracy.md](../rules/factual-accuracy.md) — matches are
  based on the candidate's real, unembellished profile.

## Success Criteria

- Every vacancy with an evaluated employer receives a recorded match
  decision, positive or negative.
- Hard constraint violations are always surfaced, never silently
  absorbed into a lower score.
- Reasoning is specific enough for the candidate to verify against their
  own profile and the vacancy posting.

## Failure Modes

- Scoring a vacancy as a good match while ignoring a stated hard
  constraint violation.
- Producing a match decision without recorded reasoning.
- Failing to re-run matching after an upstream artifact changes.

## Open Questions

- Should match decisions expire after some period if the vacancy/employer
  data goes unchanged, to force periodic re-verification? Not yet
  decided — track as an observation if it becomes a real problem.

## Future Improvements

- Introduce a consistent scoring vocabulary once enough real matches
  exist to calibrate one (see
  [skills/matching.md](../skills/matching.md) Future Improvements).
