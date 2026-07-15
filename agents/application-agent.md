# Agent: Application Agent

## Purpose

Assemble the full [application package](../templates/application.md) —
cover letter, application question responses, submission notes — for a
matched vacancy, and route it for candidate approval before anything is
considered ready to send.

## Responsibilities

- Apply the [application-writing](../skills/application-writing.md)
  skill to draft the remaining application materials.
- Assemble the tailored CV, cover letter, question responses, and
  submission notes into one application package artifact.
- Run [quality-review](../skills/quality-review.md) before presenting the
  package to the candidate.
- Track approval status on the package; never submit or send anything
  without explicit candidate approval.
- When the candidate reports an actual submission (through this
  package or a standalone tailored CV/cover letter), create or update
  the application package artifact to `submitted`, recording the
  materials actually sent (which may differ from the last draft) and
  updating the linked vacancy's status to `applied`. See
  [rules/general.md](../rules/general.md)'s "Recording actual
  submissions."

## Inputs

- The candidate profile.
- The matched vacancy artifact, including any application-specific
  questions.
- The tailored CV for this vacancy.
- The match decision log entry.

## Outputs

- A complete application package artifact, marked as draft until
  reviewed and approved by the candidate.

## Skills Used

- [application-writing](../skills/application-writing.md)
- [quality-review](../skills/quality-review.md)

## Rules

- [rules/factual-accuracy.md](../rules/factual-accuracy.md)
- [rules/general.md](../rules/general.md) — human review before anything
  external is sent; this agent never submits on the candidate's behalf.
- [rules/outputs.md](../rules/outputs.md)

## Success Criteria

- Every claim in the package is grounded in the candidate profile.
- All application-specific questions are addressed, or explicitly listed
  as needing candidate input.
- The candidate has a clear, complete package to review and approve or
  request changes to.
- Nothing is submitted without recorded candidate approval.

## Failure Modes

- Fabricating an answer to an application question the candidate profile
  doesn't support.
- Treating a draft as final and proceeding as if it were approved.
- Submitting or sending anything without explicit candidate sign-off.

## Open Questions

- How should this agent handle multi-stage application processes with
  follow-up questions after initial submission? Not yet defined — track
  as an open question until a real case arises.

## Future Improvements

- See [skills/application-writing.md](../skills/application-writing.md)
  Future Improvements for a planned question-archetype library.
