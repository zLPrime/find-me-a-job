# Skill: Vacancy Analysis

## Purpose

Extract and structure the substance of a job posting — requirements,
seniority, logistics, compensation if stated — into a clear
[vacancy summary](../templates/vacancy.md), flagging anything ambiguous
rather than resolving it silently.

## When to Invoke

- Whenever a new vacancy is discovered or supplied by the candidate and
  needs to be recorded before matching.
- When a previously recorded vacancy posting changes (e.g., requirements
  edited, deadline updated) and the artifact needs refreshing.

## Required Inputs

- The raw vacancy posting (source text, link, or candidate-supplied
  description).
- The linked employer artifact, if one exists.

## Expected Outputs

- A vacancy artifact following
  [templates/vacancy.md](../templates/vacancy.md), separating
  must-have from nice-to-have requirements as stated in the posting.
- Explicit flags on any requirement or logistic detail that is vague,
  contradictory, or missing from the posting.

## Quality Criteria

- Requirements are transcribed faithfully, not paraphrased in a way that
  changes their strictness (e.g., turning a "required" into a "preferred").
- Ambiguous seniority or scope is flagged rather than assumed.
- Compensation and logistics fields are left blank and marked "not
  stated" rather than estimated, unless the candidate wants estimation —
  in which case it must be clearly labeled as an estimate, not a posted
  fact.

## Limitations

- This skill only structures what a posting says; it does not judge fit
  (see [matching](matching.md)) or evaluate the employer (see
  [employer-analysis](employer-analysis.md)).
- It cannot resolve postings that are themselves internally
  contradictory — those are flagged as open questions.

## Future Improvements

- Add guidance for handling postings aggregated from multiple sources
  with slightly different details for the same role.
- Consider a convention for expiring vacancies that are no longer
  reachable (e.g., link dead, deadline passed).
