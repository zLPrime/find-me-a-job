# Template: Vacancy Summary

> Structural template only — no real postings. Illustrative examples must
> be clearly labeled per [examples/README.md](../examples/README.md).
>
> A vacancy is recorded as **two files**: the summary below, and a
> verbatim [posting snapshot](#posting-snapshot) of the original job
> description, saved alongside it (see
> [work/README.md](../work/README.md) for the suggested location).
> Postings expire and get edited; the snapshot is what remains when the
> listing URL no longer works.

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
- Posting snapshot: <relative link to the verbatim posting snapshot
  file(s); list every dated snapshot if the posting has been re-captured
  after a change>

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

## Posting Snapshot

The original job description, saved verbatim when the vacancy is first
recorded. Never edit a snapshot after capture: if the posting changes,
save a new dated snapshot next to the old one and link both from the
summary.

```markdown
# Posting snapshot — <role title> at <employer name>

Captured: <date and time>
Source URL: <the exact URL the text was taken from>
Capture method: <e.g. "fetched listing page", "copied from browser",
  "supplied by candidate as pasted text / PDF">
Language: <language of the posting as published>
Completeness: <complete | partial — say what is missing, e.g. "benefits
  section hidden behind login">
Supersedes: <link to the previous snapshot, if this is a re-capture>

---

<the full posting text, verbatim — title, company blurb, responsibilities,
requirements, benefits, logistics, as published. Keep the original
language and wording; do not translate, summarize, reorder or fix
typos. Page chrome (navigation, cookie banners, "similar jobs" lists)
may be dropped. Markdown headings and bullets may be used to mirror
the posting's own structure.>
```
