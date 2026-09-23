# Skill: Matching

## Purpose

Compare the candidate profile against an evaluated employer and vacancy
to produce a reasoned, evidence-based judgment of fit — recorded as a
[decision log](../templates/decision-log.md) entry.

## When to Invoke

- Whenever a vacancy has been structured
  ([vacancy-analysis](vacancy-analysis.md)) and its employer evaluated
  ([employer-analysis](employer-analysis.md)), and needs a fit judgment.
- When the candidate profile or a vacancy/employer artifact changes in a
  way that could affect a previously made match decision.

## Required Inputs

- The current candidate profile.
- The vacancy artifact (requirements, logistics).
- The employer artifact (evaluation findings).
- The candidate's stated preferences and hard constraints.

## Expected Outputs

- A decision log entry recording the match judgment, with supporting
  factors, opposing factors, unknowns, and an explicit confidence level,
  per [rules/decision-making.md](../rules/decision-making.md).
- An updated match status on the vacancy artifact.
- A keyword/terminology gap check against the vacancy's named
  requirements, splitting them three ways: (a) skills/keywords the
  candidate genuinely has and the CV already surfaces; (b) skills the
  candidate genuinely has but the profile expresses in different words
  than the posting — flagged for honest terminology alignment by
  [cv-tailoring](cv-tailoring.md), so a real match isn't lost to
  vocabulary; and (c) keywords the candidate does not genuinely have —
  recorded as opposing factors or unknowns, never as something to insert
  into the CV to "match the keyword." This makes the honest half of
  keyword-matching (align wording for skills truly held) explicit while
  keeping the dishonest half (claim a skill to hit a keyword) out.

## Quality Criteria

- The judgment weighs both the candidate's actual (not embellished)
  qualifications and the employer's evaluated characteristics.
- Hard candidate constraints (e.g., location, industries to avoid) are
  treated as filters, not just as one factor among many — a violation of
  a hard constraint should be surfaced clearly, not buried in a score.
- Reasoning is specific enough that a candidate could sanity-check it
  against their own profile and the vacancy posting.
- Rejections are just as well-reasoned and recorded as positive matches —
  a rejected vacancy still gets a decision log entry explaining why.
- The keyword/terminology gap check never blurs the line between "the
  candidate has this but the CV words it differently" (fixable by honest
  alignment) and "the candidate doesn't have this" (a real gap): the two
  are always kept distinct, so terminology alignment can never be misread
  as license to claim a missing skill.

## Limitations

- This skill produces a judgment, not a guarantee; the candidate makes
  the final call on whether to pursue any match.
- It cannot account for factors the candidate hasn't disclosed (e.g.,
  unstated preferences); such gaps should surface as open questions
  rather than silently skew the result.

## Future Improvements

- Define a consistent scoring vocabulary (e.g., strong/possible/weak
  match) once enough real matches have been produced to calibrate it.
- Add guidance for batch-ranking multiple matched vacancies against each
  other for the candidate's benefit.
