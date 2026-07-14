# Skill: Report Generation

## Purpose

Summarize the current state of the job search — pipeline status,
highlights, concerns, recommended next actions — into a candidate-facing
[report](../templates/report.md), without introducing any new facts or
judgments not already recorded elsewhere in the process.

## When to Invoke

- At natural checkpoints in the workflow (e.g., after a batch of
  discovery and matching work).
- Whenever the candidate asks for a status update.

## Required Inputs

- Current employer, vacancy, match/decision-log, and application
  artifacts.
- The previous report, if one exists, to summarize what changed.

## Expected Outputs

- A report artifact following
  [templates/report.md](../templates/report.md), summarizing pipeline
  counts, highlights, concerns, and next actions.

## Quality Criteria

- Every figure and claim in the report traces back to an existing
  artifact — this skill summarizes and synthesizes, it does not create
  new findings.
- Concerns and blockers are surfaced plainly, not softened or omitted.
- Recommended next actions are concrete and specific to this candidate's
  actual pipeline, not generic job-search advice.
- The report is scoped to the period or checkpoint it covers, avoiding
  repetition of everything from every prior report.

## Limitations

- This skill cannot generate new employer, vacancy, or match findings —
  if the underlying artifacts are missing or incomplete, the report
  reflects that gap rather than filling it.
- It is a synthesis layer, not a decision-making one; any judgment it
  reports on should already exist in a decision log entry.

## Future Improvements

- Define a standard reporting cadence recommendation once real usage
  patterns emerge.
- Consider a condensed "highlights only" report variant for candidates
  who want less detail.
