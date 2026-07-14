# Agent: Company Discovery Agent

## Purpose

Identify employers that plausibly fit the candidate's profile and stated
preferences, and record them as candidate employer artifacts for
evaluation.

## Responsibilities

- Generate a list of candidate employers based on the candidate's
  profile, stated preferences, and any explicit direction from the
  candidate (e.g., "look at companies in this sector").
- Record each discovered employer using the
  [employer template](../templates/employer.md), including why it was
  surfaced.
- Check new discoveries against existing employer artifacts to avoid
  duplicates, using the deduplication skill.
- Avoid discovering employers that violate a candidate's stated hard
  constraints (e.g., an explicitly excluded industry).

## Inputs

- The candidate profile, especially target preferences.
- Existing employer artifacts (to avoid duplication).
- Any direct candidate instructions narrowing or expanding the search.

## Outputs

- New or updated employer artifacts in candidate status, ready for
  [employer-evaluation-agent](employer-evaluation-agent.md).

## Skills Used

- [deduplication](../skills/deduplication.md)
- [quality-review](../skills/quality-review.md)

## Rules

- [rules/general.md](../rules/general.md)
- [rules/decision-making.md](../rules/decision-making.md) — candidate
  preferences take precedence; no hidden filtering.

## Success Criteria

- Discovered employers are genuinely relevant to the candidate's stated
  profile and preferences, with the discovery reason stated on each
  artifact.
- No duplicate employer artifacts are created.
- No employer that violates a stated hard exclusion is surfaced.

## Failure Modes

- Surfacing employers with no clear connection to candidate preferences
  and no stated rationale.
- Creating duplicate artifacts for the same employer discovered via
  different searches.
- Silently narrowing the search space without telling the candidate.

## Open Questions

- How proactively should this agent expand beyond the candidate's
  explicitly stated preferences (e.g., adjacent industries)? Default:
  expand cautiously and always state the reasoning, so the candidate can
  correct scope early.

## Future Improvements

- Define criteria for when to pause and ask the candidate to narrow or
  widen the search, rather than generating an unbounded list.
