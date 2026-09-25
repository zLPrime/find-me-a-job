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
  - **Question history:** question ID, bank, date asked, score, and a
    re-ask date for questions scored 1–2.
  - **Next session focus:** the topics, difficulty levels, and specific
    questions the next session should use, with the reason for each.
  - A change note stating which session was folded in.

### Update rules

- **Difficulty level per topic:** a topic score of 4 or more moves the
  level up by one; 2 or less moves it down by one; otherwise unchanged.
  Levels stay between 1 and 5.
- **Re-ask:** questions scored 1–2 are due again after two further
  sessions, so the candidate has time to study before being retested.
- **Weak spots:** a gap becomes a recurring weak spot the second time it
  appears; it is retired (kept, marked `resolved`) after two consecutive
  sessions score 4 or more on it.
- **Next session focus:** weight toward the lowest-scoring topics and
  due re-asks, keep at least one stronger topic for balance, and for a
  real upcoming interview always include the topics the employer named.

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
