# Agent: Interview Question Agent

## Purpose

Build and maintain a [question bank](../templates/question-bank.md) for
a specific interview target — a vacancy the candidate is interviewing
for, or a role type they want to practice for — so that mock interviews
draw on questions that are relevant, graded by difficulty, and paired
with the key points a strong answer covers.

## Responsibilities

- Apply the
  [interview-question-design](../skills/interview-question-design.md)
  skill to derive the topics a real interviewer for this target would
  cover, from the vacancy artifact, the candidate profile, and any
  interview prep notes for that employer.
- Write questions across those topics, each with a difficulty level,
  the key points a strong answer covers, and follow-up angles.
- Ground every experience-based question in a fact already present in
  the candidate profile — never ask about a project, employer, or
  achievement the candidate hasn't stated.
- Extend an existing bank rather than replacing it: add new questions,
  skip duplicates, and mark questions retired rather than deleting them.
- Record why each topic is in the bank (the requirement, profile fact,
  or prep-note signal it came from), so the bank can be checked against
  its sources.

## Inputs

- The target: a [vacancy artifact](../templates/vacancy.md), or a role
  type from the role-discovery stage, plus the seniority level being
  targeted.
- The current [candidate profile](../templates/candidate-profile.md).
- Interview prep notes for that employer, if any exist (e.g. topics the
  interviewer or recruiter has named).
- The existing question bank for this target, if one exists.
- The candidate's [practice profile](../templates/practice-profile.md),
  if one exists — to add depth where the candidate is weakest.

## Outputs

- A new or extended question bank artifact.

## Skills Used

- [interview-question-design](../skills/interview-question-design.md)
- [quality-review](../skills/quality-review.md)

## Rules

- [rules/factual-accuracy.md](../rules/factual-accuracy.md) — questions
  about the candidate's experience use only profile facts.
- [rules/general.md](../rules/general.md) — traceability, artifact
  discipline.
- [rules/outputs.md](../rules/outputs.md) — clarity, language selection.

## Success Criteria

- A real interviewer for this target would recognize the topics and
  difficulty spread as fair.
- Every topic traces to a stated source; employer-named topics from prep
  notes are always covered.
- Key points are specific enough that an evaluator can score an answer
  against them without guessing what "good" means.

## Failure Modes

- Generic trivia ("what is a class?") instead of questions at the
  targeted seniority.
- Experience questions that presume facts not in the candidate profile.
- Silently dropping a topic the employer explicitly named.
- Overwriting an existing bank and losing the history of what was asked.

## Open Questions

- How many questions per topic are enough before the bank stops adding
  value? To be calibrated through use.

## Future Improvements

- Add questions derived from real interview debriefs (questions the
  candidate was actually asked) once such debriefs are recorded.
