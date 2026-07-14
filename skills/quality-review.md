# Skill: Quality Review

## Purpose

Check an artifact produced by another skill or agent against this
repository's rules — factual accuracy, output quality, decision-making
standards — before it is presented to the candidate, especially for
externally visible materials.

## When to Invoke

- Before any draft CV, cover letter, application answer, or outbound
  message is presented to the candidate for approval.
- Whenever an agent is unsure whether its own output meets the
  standards in [/rules](../rules) and wants an independent check.

## Required Inputs

- The artifact under review.
- The source artifacts it was derived from (e.g., candidate profile for
  a tailored CV).
- The relevant rules: [factual-accuracy](../rules/factual-accuracy.md),
  [outputs](../rules/outputs.md), [decision-making](../rules/decision-making.md).

## Expected Outputs

- A pass/fail assessment against each relevant rule, with specific
  findings (not a generic "looks good").
- A list of concrete corrections needed, if any, before the artifact can
  go to the candidate.

## Quality Criteria

- Every fact in the reviewed artifact is checked against its stated
  source — this is the single most important check for candidate-facing
  materials.
- Draft/approval status, traceability, and open-question labeling are
  verified as present per [rules/general.md](../rules/general.md).
- Reasoning for judgments (matches, evaluations) is checked for
  completeness — supporting factors, opposing factors, confidence level.
- Findings are specific enough that the originating agent can act on
  them directly.

## Limitations

- This skill checks conformance to stated rules and traceability; it
  does not substitute for the candidate's own judgment on tone or
  content preferences.
- It cannot verify facts against source material it hasn't been given —
  it depends on being handed the actual source artifacts to check
  against.

## Future Improvements

- Build a standard checklist per artifact type so review is consistent
  across agents.
- Consider whether repeated review failures on a given skill should
  automatically trigger a journal entry (see
  [skills/deduplication.md](deduplication.md) for a related pattern of
  systematic checks).
