# Skill: Employer Analysis

## Purpose

Assess a candidate employer against criteria relevant to this candidate —
stability, culture, compensation signals, reputation, and any stated
red-flag concerns — and record the assessment on the employer artifact.

## When to Invoke

- After an employer has been discovered (or supplied directly by the
  candidate) and needs evaluation before vacancies there are pursued.
- When new information about a previously evaluated employer emerges and
  the existing evaluation needs revisiting (see
  [rules/decision-making.md](../rules/decision-making.md)).

## Required Inputs

- The employer artifact ([templates/employer.md](../templates/employer.md))
  in candidate or evaluated status.
- The candidate's stated preferences and constraints from their profile
  (e.g., industries to avoid, values that matter to them).

## Expected Outputs

- An updated employer artifact with evaluation findings: stability,
  culture, compensation, reputation indicators, and red flags.
- An explicit confidence level and supporting reasoning for the overall
  assessment.
- Open questions where evidence is thin or conflicting.

## Quality Criteria

- Findings are grounded in identifiable evidence (stated in the artifact),
  not vague impressions.
- Both supporting and opposing signals are recorded — a one-sided
  evaluation is incomplete.
- Confidence level reflects the actual strength and volume of evidence
  available, not a default.
- Candidate-stated preferences (e.g., "avoid heavy travel") are checked
  against findings explicitly, not left implicit.

## Limitations

- This skill assesses employers using available information; it cannot
  verify claims made by an employer about itself, and should flag
  self-reported claims as such.
- It does not decide whether the candidate should apply — that synthesis
  with the candidate's own fit happens in [matching](matching.md).

## Future Improvements

- Define a standard set of evaluation dimensions so employer artifacts
  are comparable to each other at a glance.
- Add guidance for weighting recency of evidence (e.g., old reviews vs.
  recent ones) once patterns emerge from real use.
