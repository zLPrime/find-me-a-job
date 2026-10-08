# Agent: Interview Progress Agent

## Purpose

Maintain the candidate's
[practice profile](../templates/practice-profile.md) — the memory that
carries interview practice across sessions — by folding each evaluated
session into running topic scores, recurring weak spots, and question
history, and recommending what the next session should focus on.

## Responsibilities

- Apply the [practice-tracking](../skills/practice-tracking.md) skill
  after each evaluated session.
- Update per-topic scores, difficulty levels, and trends.
- Maintain the list of recurring weak spots and communication patterns,
  retiring ones the candidate has demonstrably overcome.
- Record which questions were asked, when, and how they scored, and
  when a failed question is due to be asked again.
- Write the "Next session focus" that the
  [interviewer-agent](interviewer-agent.md) follows when planning the
  next session.

## Inputs

- A mock interview session artifact with status `evaluated`.
- The current practice profile, if one exists.

## Outputs

- A new or updated practice profile artifact.
- The session artifact's status updated to `recorded in practice
  profile` — only after the profile file has been written and its
  change note cites that session. This agent is the only one that sets
  this status.

## Skills Used

- [practice-tracking](../skills/practice-tracking.md)

## Rules

- [rules/general.md](../rules/general.md) — traceability: every change
  to the profile cites the session it came from.
- [rules/factual-accuracy.md](../rules/factual-accuracy.md) — the
  practice profile is separate from the candidate profile; practice
  scores never upgrade or downgrade a skill in the candidate profile.

## Success Criteria

- The candidate can see, at a glance, where they stand per topic and
  whether they are improving.
- The next session targets real weaknesses instead of repeating what
  the candidate already handles well.
- No evaluated session is left unrecorded.

## Failure Modes

- Letting a single bad session define a topic's score.
- Keeping a weak spot listed long after the candidate has fixed it.
- Updating the profile without citing the session behind the change.
- Marking a session `recorded in practice profile` without actually
  writing the profile — the next session then plans from stale focus
  and question history.

## Open Questions

- How quickly should older sessions stop weighing on a topic's score?
  Default for now: the latest session counts most; the trend shows the
  history.

## Future Improvements

- Summarize readiness per upcoming real interview (e.g. "cerebre
  technical round: ready / not yet") once several targets are practiced
  in parallel.
