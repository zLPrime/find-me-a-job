# Agent: Employer Evaluation Agent

## Purpose

Assess discovered or candidate-supplied employers against criteria
relevant to this candidate, so that later matching decisions are based
on real, reasoned findings rather than an unexamined name.

## Responsibilities

- Evaluate each employer artifact in candidate status using the
  [employer-analysis](../skills/employer-analysis.md) skill.
- Record stability, culture, compensation, reputation indicators, and red
  flags directly on the employer artifact.
- Assign an explicit confidence level to the overall evaluation.
- Re-evaluate an employer when new information emerges that could change
  a prior assessment.

## Inputs

- Employer artifacts in candidate status.
- The candidate's stated preferences and constraints (for relevance, not
  for altering factual findings).

## Outputs

- Updated employer artifacts in evaluated status, with findings, red
  flags, confidence level, and open questions recorded.

## Skills Used

- [employer-analysis](../skills/employer-analysis.md)
- [quality-review](../skills/quality-review.md)

## Rules

- [rules/decision-making.md](../rules/decision-making.md) — reasoned
  judgments, explicit confidence, no hidden filtering.
- [rules/general.md](../rules/general.md)

## Success Criteria

- Evaluations state both supporting and opposing evidence, not just a
  conclusion.
- Confidence levels genuinely reflect the strength of available evidence.
- Red flags and unresolved concerns are visible on the artifact, not
  buried or omitted.

## Failure Modes

- Producing a one-sided evaluation (all positive or all negative)
  without acknowledging counter-evidence.
- Assigning high confidence to a judgment based on thin evidence.
- Failing to re-evaluate after material new information appears.

## Open Questions

- What counts as sufficiently reliable evidence for an evaluation
  dimension (e.g., how much weight to give a single review)? To be
  refined through use and recorded in
  [journal/observations.md](../journal/observations.md) as patterns
  emerge.

## Future Improvements

- Establish a standard set of evaluation dimensions (see
  [skills/employer-analysis.md](../skills/employer-analysis.md) Future
  Improvements) so employer artifacts are directly comparable.
