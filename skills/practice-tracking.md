# Skill: Practice Tracking

## Purpose

Carry interview practice across sessions by folding each evaluated
session into the candidate's
[practice profile](../templates/practice-profile.md), and decide what
the next session should focus on.

## When to Invoke

- Whenever a session artifact has status `evaluated`.
- When the candidate asks where they stand or what to practice next.

## Required Inputs

- The evaluated session artifact.
- The current practice profile, if one exists.

## Expected Outputs

- An updated practice profile:
  - **Topic scores:** per topic, the latest score, the number of
    sessions, the trend, and the current difficulty level.
  - **Recurring weak spots** and **communication patterns**, each
    citing the sessions it appeared in.
  - **Question history:** question ID, bank, scope version, date
    asked, session number, score, and the session the question is due
    again (see "Re-ask" below).
  - **Next session focus:** the topics, difficulty levels, and specific
    questions the next session should use, with the reason for each.
  - A change note stating which session was folded in.

### Update rules

- **Difficulty level per topic:** a topic score of 4 or more moves the
  level up by one; 2 or less moves it down by one; otherwise unchanged.
  Levels stay between 1 and 5.
- **Comparing scores:** a question's scores are only compared, and its
  trend only shown, between attempts with the same scope version. The
  first attempt at a new scope version is a new baseline, recorded with
  its version, not as a rise or fall from the old one. Topic trends say
  when they span different scope versions.
- **Re-ask (spaced by score):** a question is due again a fixed number
  of sessions after the session it was asked in:

  | Score | Due again |
  |---|---|
  | 1–2 | 2 sessions later — time to study before the retest |
  | 3 | 4 sessions later — core idea there, depth still to prove |
  | 4 | 8 sessions later — a retention check |
  | 5 | not repeated |

  Record it as "session N." A question that is due but not asked keeps
  its original due session; it isn't pushed back, so it becomes
  overdue and moves up the queue. Session numbers count every session
  that reached `recorded in practice profile`; abandoned ones don't
  count.
- **Weak spots:** a gap becomes a recurring weak spot the second time it
  appears; it is retired (kept, marked `resolved`) after two consecutive
  sessions score 4 or more on it.
- **Next session focus:** list the questions due by the next session,
  oldest due first, and apply the session mix below. Weight new
  questions toward the lowest-scoring topics, keep at least one
  stronger topic for balance, and for a real upcoming interview always
  include the topics the employer named. State the split ("4 due, 4
  new") and which due questions are carried over.
- **Coverage window:** every active question in the bank is asked at
  least once within 4 sessions — counted from the session after it was
  added to the bank (for questions that existed when this rule was
  adopted: sessions 6–9). Each session's new slots are set to keep that
  pace: new slots = unasked active questions ÷ sessions left in their
  window, rounded up.
- **Session mix:** 8 main questions by default.
  - **New slots:** the larger of half the session and what the coverage
    window needs — but never more than the questions still unasked, and
    always leaving at least 3 slots for due questions while any are
    due.
  - **Due slots:** the rest of the session.
  - When more questions are due than fit, take the most overdue first,
    then the lowest score; the rest carry over to the next session.
  - When fewer are due, fill the session with new questions.
  - If the window can't be met with 8 questions and 3 due slots, say so
    in the focus and offer the candidate a longer session (up to 10)
    rather than letting the window slip silently.
  - When every bank question has been asked and fewer than 8 are due,
    run a shorter session and flag that the bank needs extending.
- **Choosing new questions:** topics with no question asked yet come
  first, then topics with the fewest questions asked, then the
  lowest-scoring topics. Within a topic, take the question closest to
  the topic's current difficulty level — a topic is never skipped
  because the bank has nothing at exactly that level. Flag the bank as
  needing extending only when a topic has no unasked questions left.
- **Overrides:** employer-named topics for a real upcoming interview
  come before the mix, and the candidate can ask for a different split
  for one session.

### Closing the session

Write the profile first, re-read it to confirm the change note, "Last
updated", topic scores, question history, and next session focus all
reflect the session, and only then set the session's status to
`recorded in practice profile`. If several sessions are at `evaluated`,
fold them in date order.

Then commit, in the candidate repo, everything the close-out touched —
the session file (evaluation and debrief), the practice profile, study
topics, and any confirmed question bank changes — as one commit naming
the session, per [rules/general.md](../rules/general.md), "Commit
cadence". The close-out isn't finished until this commit exists.

## Quality Criteria

- Every change cites the session it came from.
- The profile stays short enough to scan in under a minute: history
  lives in session artifacts; the profile holds the current state.
- A single session never swings a topic by more than one difficulty
  level.

## Limitations

- Trends over a few sessions are noisy; the profile shows direction,
  not a measurement.
- Practice scores are not candidate facts and never feed the candidate
  profile, per [rules/factual-accuracy.md](../rules/factual-accuracy.md).

## Future Improvements

- Separate readiness per real interview target when several are being
  practiced in parallel.
