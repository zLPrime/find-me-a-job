# Skill: Interview Question Design

## Purpose

Turn an interview target (a vacancy or a role type, at a stated
seniority) into a [question bank](../templates/question-bank.md) of
relevant, difficulty-graded questions, each paired with the key points
a strong answer covers and the follow-up angles a real interviewer
would use.

## When to Invoke

- When the candidate wants to practice for a target that has no
  question bank yet.
- When a real interview is scheduled and prep notes name topics the
  bank doesn't cover.
- When the practice profile shows a weak topic whose questions have
  all been used.

## Required Inputs

- The target vacancy artifact, or the role type and seniority.
- The candidate profile.
- Interview prep notes for that employer, if any.
- The existing question bank, if any.

## Expected Outputs

- A question bank artifact, new or extended, containing:
  - **Topics**, each with its source: a vacancy requirement, a profile
    fact, a prep-note signal (e.g. "the interviewer named Dijkstra"),
    or standard coverage for the role and seniority.
  - **Questions** per topic, each with a stable ID, a difficulty level
    (1–5, as defined in the template), the type (conceptual,
    experience-based, scenario, or design discussion), the key points a
    strong answer covers, and two or three follow-up angles.

## Quality Criteria

- Topics reflect what a real interviewer for this target would cover,
  weighted toward what the vacancy and prep notes emphasize.
- Difficulty is spread so a session can move up or down: each topic has
  questions below, at, and above the targeted seniority where possible.
- Key points are concrete and checkable ("names the thread-pool
  starvation risk of sync-over-async"), not vague ("understands async").
- Follow-up angles push on trade-offs, failure modes, scale, and "why
  not the alternative" — the places where shallow knowledge shows.
- Experience-based questions reference only projects, employers, and
  achievements present in the candidate profile.
- Questions are written in the language the real interview will use;
  if that isn't known, ask. See
  [rules/outputs.md](../rules/outputs.md) "Language selection."

## Limitations

- Key points reflect common expert consensus, not one interviewer's
  private expectations; a real interviewer may want something else.
- The skill cannot know what a specific employer will actually ask
  beyond what prep notes and the posting reveal.
- Practical exercises (live coding, whiteboard) are out of scope; a
  design question is a spoken discussion.

## Future Improvements

- Add a behavioral-question pattern (situation, action, result) that
  draws its scenarios from profile facts only.
