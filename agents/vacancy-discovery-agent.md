# Agent: Vacancy Discovery Agent

## Purpose

Find open vacancies — at discovered employers or independently — and
record them as structured vacancy artifacts.

## Responsibilities

- Search for open vacancies matching the candidate's preference criteria
  across the role types identified by
  [role-discovery-agent](role-discovery-agent.md) — not only the single
  title the candidate first named.
- Record each discovered vacancy using the
  [vacancy template](../templates/vacancy.md) via the
  [vacancy-analysis](../skills/vacancy-analysis.md) skill, including a
  verbatim snapshot of the original job description saved alongside the
  summary.
- Link each vacancy to its employer artifact, creating a new employer
  candidate artifact if the vacancy's employer isn't already tracked
  (handing off to [company-discovery-agent](company-discovery-agent.md)
  conventions for that artifact).
- Check for duplicate vacancy postings using the deduplication skill.

## Inputs

- The candidate profile and stated preferences.
- The candidate role types identified by
  [role-discovery-agent](role-discovery-agent.md), which set the range of
  roles — including adjacent ones — to search for, rather than only the
  single title the candidate first named.
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
- Every vacancy has a verbatim posting snapshot, so the original job
  description survives the listing expiring or being edited.

## Failure Modes

- Paraphrasing requirements in a way that changes their meaning or
  strictness.
- Missing an obvious duplicate because of superficial differences (e.g.,
  same posting found on two job boards).
- Recording a vacancy without linking it to an employer artifact.
- Recording only the structured summary and losing the original posting
  text once the listing goes offline.

## Open Questions

- How to handle vacancies with no identifiable employer (e.g., anonymized
  postings) — currently: record with employer marked "unknown" and flag
  for the candidate.

## Future Improvements

- Add conventions for marking vacancies as expired/stale once a deadline
  has clearly passed.
