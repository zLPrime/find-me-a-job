# Skill: Mock Interviewing

## Purpose

Plan and conduct a realistic mock interview from a question bank, and
record it faithfully as a
[mock interview session](../templates/mock-interview-session.md)
artifact.

## When to Invoke

- Whenever the candidate asks to practice an interview for a target
  that has a question bank.

## Required Inputs

- The question bank for the target.
- The practice profile, if one exists.
- The vacancy artifact and interview prep notes, for a real upcoming
  interview.

## Expected Outputs

- A session artifact with a Plan and a Transcript, status
  `awaiting evaluation` at the end.

## Procedure

1. **Confirm the session.** Target, format, language, and length
   (default: 6–10 main questions, about 45–60 minutes). Tell the
   candidate they can say `hint` to ask for help and `end` to stop.
2. **Plan.** Select questions in this order of priority:
   1. Topics the employer explicitly named in prep notes (real
      interview targets only).
   2. The practice profile's "Next session focus."
   3. Questions due for a re-ask.
   4. Questions never asked, on topics not yet covered.

   Start at the topic's current difficulty level from the practice
   profile (default: the targeted seniority's level). Write the plan to
   the session artifact before the first question.
3. **Interview.** One question at a time. After each answer, decide:
   - vague, buzzword-heavy, or unsupported → probe ("how exactly?",
     "give me a concrete case", "why that and not X?");
   - solid → push one level harder with a follow-up angle, then move on;
   - clearly stuck after one probe → note it and move on, without
     rescuing the candidate.

   Adjust difficulty for the next question in the same topic by the
   same logic. Keep a steady, neutral, professional tone.
4. **Record as you go.** Append each exchange (question, answer,
   follow-ups) to the transcript before moving on, with the candidate's
   answers in their own words. A long session must never exist only in
   conversation.
5. **Close.** When the plan is done or the candidate says `end`, ask
   whether they have questions for the interviewer (as a real interview
   would), then set status to `awaiting evaluation`. Do not give
   feedback — say that evaluation follows.
6. **Surface new facts.** If an answer revealed a fact about the
   candidate's experience that isn't in the candidate profile, list it
   in the session's "New candidate facts" section and record it in
   `input/notes.md` per
   [rules/factual-accuracy.md](../rules/factual-accuracy.md).

## Quality Criteria

- If a tangential concept, tool, or technique comes up during the
  interview — in a candidate's answer, a hint given, or the
  candidate's own question at the close — that's worth studying later
  but wasn't itself what the question was testing, record it in
  [templates/study-topics.md](../templates/study-topics.md) with the
  context it came up in, alongside the session.
- The interviewer never reveals key points, directly or through
  leading questions.
- Help given on request is recorded as `[hint requested]` with the hint
  itself, so the evaluator can account for it.
- The transcript lets someone who wasn't present follow the whole
  interview.

## Limitations

- A mock interview can't reproduce a specific interviewer's personality
  or unannounced topics.
- Live coding and whiteboard exercises are out of scope.

## Future Improvements

- Add a timed mode that tracks and flags answer length.
