# Template: Vacancy Summary

> Structural template only — no real postings. Illustrative examples must
> be clearly labeled per [examples/README.md](../examples/README.md).

```markdown
# Vacancy — <role title> at <employer name>

Status: candidate | matched | rejected | applied | expired
Last updated: <date and time>
Date posted (if known):
Date discovered (date and time):

## Links

- Listing URL: <where this vacancy was found — the job-board or careers
  page the posting was discovered on>
- Application-form URL: <the actual target the "Apply" button resolves
  to, when it differs from the listing — often a separate ATS domain
  (an applicant-tracking form, a company site). Record it even if the
  listing is just a thin redirect that exposes only this link. This is
  the **primary deduplication key**: two listings that resolve to the
  same application-form URL are the same requisition (see
  [skills/deduplication.md](../skills/deduplication.md)). Leave blank
  only for a genuine 1-click widget with no distinct form URL, and say
  so.>
- Employer canonical posting (if different): <the same role on the
  employer's own careers site, when the vacancy was discovered via an
  aggregator or board instead>

## Role Summary

- Title:
- Employer:
- Location / remote policy:
- Seniority level (as stated in posting):
- Reporting line (if stated):

## Requirements (as stated in posting)

- Must-have:
- Nice-to-have:
- Ambiguous/unclear requirements: <flag rather than interpret silently>

## Compensation & Logistics (as stated, if available)

- Salary range:
- Contract type:
- Application deadline:
- Application method:

## Notes

- <anything relevant not covered above>

## Linked Employer

- <reference to the corresponding employer artifact>

## Match Status

- <reference to the match decision produced by the matching-agent, once
  available>

## Availability Checks

- <date and time> — <live | expired | removed>, <how checked, e.g.
  "re-fetched listing URL, deadline shown as 21.07.2026">
- <append a new line each time this vacancy is re-checked; see
  rules/general.md's "Source liveness" section>
```
