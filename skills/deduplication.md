# Skill: Deduplication

## Purpose

Detect and resolve duplicate or near-duplicate artifacts — the same
employer discovered twice, the same vacancy found through two sources,
overlapping match decisions — so the candidate never sees redundant or
inconsistent versions of the same thing.

## When to Invoke

- After employer or vacancy discovery, before evaluation or matching
  proceeds, to catch duplicates early.
- During a bulk job-board sweep (see
  [docs/workflow.md](../docs/workflow.md)'s "Alternate path" and
  [skills/bulk-application-fill.md](bulk-application-fill.md)), on **each**
  posting before any artifact — including a checkpoint stub — is created
  for it. The sweep bypasses the discovery agents that normally invoke
  this skill, so the check has to be made explicitly per posting; the
  higher volume and speed make an un-deduplicated posting easy to miss.
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

## Matching heuristics

Match on substantive identity, not the surface form. Known patterns
observed in this process, strongest key first:

- **Same application-form URL.** When two postings resolve to the same
  application-form URL (the target the "Apply" button lands on — see the
  Links block of [templates/vacancy.md](../templates/vacancy.md)), they
  are the same requisition, full stop — no fuzzy comparison needed, even
  if their listing URLs, boards, or titles differ. This is also the
  identifier to rely on when a listing is a thin redirect that exposes
  only the final form link. Check it first when it's available.
- **Same requisition, different locator.** The same posting recurs under
  a different board URL, slug, or hash, or is reached through a job
  board's "similar offers"/"related offers" carousel. A differing URL is
  *not* evidence of a distinct posting — compare employer + role title +
  the substance of the requirements/logistics. This is the pattern that
  has been missed most often in bulk sweeps.
- **Same employer, different opening.** Same employer with a genuinely
  different role (or a clearly separate requisition for the same role) is
  *not* a duplicate — keep both, each as its own vacancy artifact,
  clearly distinguished. "Same employer" alone never establishes a
  duplicate.
- **Name/spelling variance on employers.** Normalize before comparing:
  legal-entity suffixes, regional variants, and punctuation/casing
  differences describe one employer; genuinely different employers with
  similar names are not merged.

When employer + role + requirement substance line up but you're not
certain, flag it as an open question rather than merging or splitting on
a guess (see Limitations).

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

- Extend the "Matching heuristics" section as new duplicate patterns are
  observed (e.g., domain matching for employers, role+employer+date
  proximity for vacancies) beyond the same-requisition/same-employer/
  name-variance cases already captured there.
- Consider a periodic sweep skill invocation rather than only
  point-in-time checks at discovery — a reconciliation pass over all
  artifacts, complementing the per-posting check the bulk sweep already
  does at the end (see [docs/workflow.md](../docs/workflow.md)'s
  "Reconcile at the end of a sweep").
