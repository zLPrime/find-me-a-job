# Skill: Interview Question Design

## Purpose

Turn an interview target (a vacancy or a role type, at a stated
seniority) into a [question bank](../templates/question-bank.md) of
relevant, difficulty-graded questions, each paired with the key points
a strong answer covers and a fixed set of follow-ups — a defined scope
that stays the same every time the question is asked, so scores compare
across sessions.

## When to Invoke

- When the candidate wants to practice for a target that has no
  question bank yet.
- When a real interview is scheduled and prep notes name topics the
  bank doesn't cover.
- When the practice profile shows a weak topic whose questions have
  all been used.
- Whenever a mock interview needs a question the bank doesn't have —
  before the question is planned or asked, since sessions only use
  bank questions.

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
    experience-based, scenario, or design discussion), and its scope:
    numbered key points for the main question, one to three required
    follow-ups each with their own numbered key points, and a scope
    version. See "Question scope" below.

## Quality Criteria

- Topics reflect what a real interviewer for this target would cover,
  weighted toward what the vacancy and prep notes emphasize.
- Difficulty is spread so a session can move up or down: each topic has
  questions below, at, and above the targeted seniority where possible.
- Key points are concrete and checkable ("names the thread-pool
  starvation risk of sync-over-async"), not vague ("understands async").
- Key points state the idea first and give API or term names as the
  usual label, in brackets: "the app validates settings at startup and
  refuses to start with a bad value (`ValidateOnStart()`)", not
  "uses `ValidateOnStart()`". The evaluator scores the idea; see
  [interview-evaluation](interview-evaluation.md), "Mark the idea, not
  the name."
- Required follow-ups push on trade-offs, failure modes, scale, and
  "why not the alternative" — the places where shallow knowledge shows.
  Each one is unconditional (no "if the answer says X, ask Y") and has
  a one-line `Tests:` statement of what it checks. The interviewer may
  reword it to fit the conversation but never changes what it tests.
- Follow-ups are concrete, not abstract: they name a situation, a
  symptom, or a number the candidate can reason about ("p99 jumps from
  80 ms to 2 s every few minutes"), not an open-ended "what would you
  do, concretely?" that can only get an "it depends."
- A follow-up doesn't repeat what a strong main answer already covers.
  If a key point is likely to come up in the main answer, it belongs to
  the main question, not to a follow-up that re-asks it.
- A follow-up that assumes the candidate's experience ("on PostgreSQL,
  which you've used") is grounded in the profile, and still makes
  sense asked as a hypothetical.
- Every key point is reachable from the main question or a required
  follow-up. A point no question in the scope asks about can't be
  scored fairly.
- Experience-based questions reference only projects, employers, and
  achievements present in the candidate profile.
- Questions are written in the language the real interview will use;
  if that isn't known, ask. See
  [rules/outputs.md](../rules/outputs.md) "Language selection."

## Question scope

A question's scope is everything a session will ask and score for it:
the main question, its required follow-ups, and their key points. It is
the same every time, so a re-ask measures progress rather than a
different set of follow-ups.

- **Scored key points** are numbered K1, K2, … across the main
  question and its follow-ups. Usually 2–4 for the main question and
  2–3 per follow-up.
- **Required follow-ups** (F1, F2, …) are covered every time: asked,
  narrowed to what the answer left out, or skipped when already
  covered. What's fixed is what each one tests. The wording adapts to
  the conversation (see [mock-interviewing](mock-interviewing.md)).
  The interviewer may add neutral probes, but never a follow-up that
  isn't in the scope.
- **Out of scope** (optional) names nearby topics the question does
  not test, so neither the interviewer nor the evaluator drifts into
  them.
- **Scope version.** Any change to what the question or its follow-ups
  test, or to the key points, raises the version by one and records
  the date and reason on the question. That includes a key point added
  after a corrections debrief. Scores are only compared between
  attempts with the same scope version; see
  [practice-tracking](practice-tracking.md). Rewording a follow-up to
  be clearer or more concrete without changing its `Tests:` line or
  key points doesn't raise it, and neither does fixing a typo.

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
