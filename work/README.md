# Work

This directory holds the real, in-progress and completed artifacts
produced while running the process for an actual candidate: candidate
profiles, employer profiles, vacancy summaries, application packages, and
reports.

## Suggested organization

As the process is used, organize this directory in whatever way keeps
related artifacts easy to find — for example, by candidate (if supporting
more than one) and then by artifact type:

```text
work/
  <candidate-name>/
    candidate-profile.md
    employers/
      <employer-name>.md
    vacancies/
      <vacancy-name>.md
    applications/
      <application-name>.md
    reports/
      <date>.md
```

This structure is a suggestion, not a requirement — adapt it if a clearer
organization emerges, and note the change in
[journal/improvements.md](../journal/improvements.md) if it's a durable
convention worth keeping.

## Rules

- Every artifact here follows the corresponding template in
  [/templates](../templates).
- Every artifact here is real: no fictional or illustrative content
  belongs in this directory — see [/examples](../examples) for that.
- Artifacts carry status and last-updated fields per
  [rules/outputs.md](../rules/outputs.md); superseded versions are kept,
  not deleted, per [rules/general.md](../rules/general.md).
