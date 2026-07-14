# Agent: Vacancy Discovery Agent

## Purpose

Find open vacancies — at discovered employers or independently — and
record them as structured vacancy artifacts.

## Responsibilities

- Search for open vacancies matching the candidate's stated role and
  preference criteria.
- Record each discovered vacancy using the
  [vacancy template](../templates/vacancy.md) via the
  [vacancy-analysis](../skills/vacancy-analysis.md) skill.
- Link each vacancy to its employer artifact, creating a new employer
  candidate artifact if the vacancy's employer isn't already tracked
  (handing off to [company-discovery-agent](company-discovery-agent.md)
  conventions for that artifact).
- Check for duplicate vacancy postings using the deduplication skill.

## Inputs

- The candidate profile and stated preferences.
- Existing employer artifacts.
- Existing vacancy artifacts (to avoid duplication).

## Outputs

- New or updated vacancy artifacts in candidate status, ready for
  [matching](matching-agent.md) once the linked employer is evaluated.

## Skills Used

- [vacancy-analysis](../skills/vacancy-analysis.md)
- [deduplication](../skills/deduplication.md)
- [quality-review](../skills/quality-review.md)

## Rules

- [rules/general.md](../rules/general.md)
- [rules/decision-making.md](../rules/decision-making.md)

## Success Criteria

- Vacancy artifacts faithfully and completely transcribe posting
  requirements and logistics, with ambiguities flagged rather than
  resolved by guessing.
- No duplicate vacancy artifacts for the same posting.
- Every vacancy is linked to an employer artifact.

## Failure Modes

- Paraphrasing requirements in a way that changes their meaning or
  strictness.
- Missing an obvious duplicate because of superficial differences (e.g.,
  same posting found on two job boards).
- Recording a vacancy without linking it to an employer artifact.

## Open Questions

- How to handle vacancies with no identifiable employer (e.g., anonymized
  postings) — currently: record with employer marked "unknown" and flag
  for the candidate.

## Future Improvements

- Add conventions for marking vacancies as expired/stale once a deadline
  has clearly passed.
