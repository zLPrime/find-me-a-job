# Skill: Deduplication

## Purpose

Detect and resolve duplicate or near-duplicate artifacts — the same
employer discovered twice, the same vacancy found through two sources,
overlapping match decisions — so the candidate never sees redundant or
inconsistent versions of the same thing.

## When to Invoke

- After employer or vacancy discovery, before evaluation or matching
  proceeds, to catch duplicates early.
- Whenever an agent suspects an artifact it's about to create may already
  exist in a different form (e.g., different source, slightly different
  name spelling).

## Required Inputs

- The candidate (or nearly-candidate) artifact being checked.
- The existing set of employer and/or vacancy artifacts to check against.

## Expected Outputs

- A determination: new artifact, or duplicate of an existing one.
- If a duplicate: a merged artifact preserving all distinct information
  from both, with sources for each retained piece of information, and a
  note of what was merged and when.
- If a near-duplicate with genuine differences (e.g., same employer, two
  different open vacancies): both are kept, clearly distinguished.

## Quality Criteria

- Merges never silently drop information — if two sources disagree on a
  detail, the disagreement is flagged rather than one version being
  discarded.
- Matching is based on substantive identity (same employer/role), not
  superficial similarity (e.g., different employers with similar names
  are not merged).
- Every merge is traceable: it should be possible to see what the
  artifact looked like before and after.

## Limitations

- This skill reduces redundant/conflicting artifacts; it does not
  evaluate quality or fit — that remains the job of
  [employer-analysis](employer-analysis.md),
  [vacancy-analysis](vacancy-analysis.md), and [matching](matching.md).
- Ambiguous cases (possible but not certain duplicates) should be flagged
  as open questions rather than merged or split by default guess.

## Future Improvements

- Define concrete matching heuristics (name normalization, domain
  matching for employers, role+employer+date proximity for vacancies)
  once real-world duplicate patterns are observed.
- Consider a periodic sweep skill invocation rather than only
  point-in-time checks at discovery.
