# Skill: Profile Analysis

## Purpose

Turn raw candidate materials (CV, LinkedIn export, notes, direct answers)
into a structured, accurate [candidate profile](../templates/candidate-profile.md).

## When to Invoke

- At the start of a new job search process, once the candidate has
  supplied source materials.
- Whenever the candidate provides new or corrected information that
  should update the existing profile.

## Required Inputs

- Candidate source materials from [/input](../input).
- The existing candidate profile, if one already exists (for updates
  rather than a full rebuild).

## Expected Outputs

- A candidate profile artifact following
  [templates/candidate-profile.md](../templates/candidate-profile.md),
  with every fact traceable to a specific source document or statement.
- An explicit list of open questions or gaps where source material is
  incomplete or ambiguous.

## Quality Criteria

- Every fact in the profile can be traced back to source material — no
  exceptions. See [rules/factual-accuracy.md](../rules/factual-accuracy.md).
- Dates, titles, and employers match the source exactly; no rounding,
  merging, or reinterpretation that changes meaning.
- Ambiguities (overlapping employment dates, unclear seniority, vague
  skill levels) are flagged as open questions, not silently resolved.
- The summary section restates rather than embellishes.
- Target preferences are recorded only where the candidate actually
  stated them; unstated preferences are marked unconfirmed rather than
  assumed.

## Limitations

- This skill cannot validate that source materials themselves are
  accurate — it takes candidate-supplied information at face value and
  defers correction entirely to the candidate.
- It does not judge whether the candidate's background is strong or weak
  for any particular role; that judgment belongs to
  [matching](matching.md).

## Future Improvements

- Guidance for reconciling conflicting information across multiple
  source documents (e.g., CV vs. LinkedIn export) is not yet defined —
  currently defaults to flagging the conflict as an open question.
- Consider a lightweight intake questionnaire skill to reduce the number
  of open questions generated on first pass.
