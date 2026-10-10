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

0. **Check that practice memory is current.** Before planning, list
   the target's session artifacts. If any earlier session is not at
   `recorded in practice profile` or `abandoned`, stop and close it out
   first: `awaiting evaluation` → evaluate; `evaluated` → run the
   [interview-progress-agent](../agents/interview-progress-agent.md);
   `in progress` with an empty or partial transcript → ask the
   candidate whether to resume it or mark it `abandoned`. Also confirm
   the practice profile's change note cites the latest session — a
   status saying `recorded in practice profile` without that citation
   means the profile was never updated, and planning from it repeats
   old questions and ignores the latest results. Finally, check the
   candidate repo for uncommitted practice files (sessions, profile,
   study topics, question bank) and commit them before planning.
1. **Confirm the session.** Target, format, language, and length
   (default: 6–10 main questions, about 45–60 minutes). Tell the
   candidate they can say `hint` to ask for help and `end` to stop.
2. **Plan.** Select questions in this order of priority:
   1. Topics the employer explicitly named in prep notes (real
      interview targets only).
   2. The practice profile's "Next session focus," which sets the
      split between due and new questions to keep every bank question
      within its coverage window (see
      [practice-tracking](practice-tracking.md), "Coverage window" and
      "Session mix").
   3. Due questions: most overdue first, then the lowest score. Those
      that don't fit carry over.
   4. Never-asked questions: topics with nothing asked yet first, then
      topics with the fewest questions asked.

   **Every main question comes from the bank**, cited by its question
   ID in the plan. If the plan needs a question the bank doesn't have
   (a prep-note topic isn't covered, a focus topic has run dry, the
   candidate asks for something new), stop and have the
   [interview-question-agent](../agents/interview-question-agent.md)
   add it to the bank first — with its full scope —
   then plan it by its new ID. Never write a question into the plan or
   ask one that isn't in the bank.

   Check every selected question against the practice profile's
   Question History: a question already asked is only used again when
   its re-ask date is due.

   Start at the topic's current difficulty level from the practice
   profile (default: the targeted seniority's level). If the topic has
   no unasked question at that level, take the closest level rather
   than skipping the topic. Write the plan to
   the session artifact before the first question.
3. **Interview.** One question at a time, within the question's fixed
   scope from the bank (see
   [interview-question-design](interview-question-design.md),
   "Question scope"), so every attempt at a question is comparable:
   - **Main question,** asked as written in the bank.
   - **Required follow-ups,** every one. What's fixed is what each
     follow-up tests (its `Tests:` line and key points), not its exact
     words. The bank wording is the default. Bridge into it from the
     candidate's answer the way a real interviewer would: "You said
     the thread count keeps growing. What would you look at in
     production to confirm it's starvation?" A bridge may only quote or
     paraphrase what the candidate actually said. It never adds a fact,
     term, or key point they haven't mentioned. Order may follow the
     conversation.
     - **Already covered:** if the candidate already covered all of a
       follow-up's key points, skip it and record
       `[F2 skipped — already covered]`. If they covered some, don't
       re-ask the whole thing ("Didn't I just explain it?"). Narrow it
       to the part they haven't addressed, starting from what they
       said ("You covered the throttling. What happens to the blocked
       thread itself while it waits?"), and record it as
       `[F2 narrowed]`.
     - **Premise doesn't hold:** if a follow-up assumes experience the
       candidate says they don't have, ask the hypothetical version of
       the same question once ("How would you expect it to differ?")
       rather than moving on.
   - **Neutral probes,** only when an answer is vague, skips over
     something the candidate raised, or makes a claim worth testing.
     When an answer is clear and complete, don't probe. Zero probes is
     the normal case, and two is a hard limit, not a target. Count
     probes across the main question and its follow-ups. A probe asks
     the candidate to expand on something specific they said, and
     names it: "You said
     you'd watch unique thread IDs in the logs. What pattern there
     would tell you it's starvation?" Generic stock probes ("Why
     exactly?", "Can you say more?", "What else?") are vague, and a
     candidate can't tell what's being asked. A probe never names,
     hints at, or steers toward a key point the candidate hasn't
     mentioned. Record each one as `[probe]`.
   - **Asking for an example:** if the candidate has no example ready,
     offer a small concrete setup to work from ("Say a 200-line
     `ProcessOrder` method with nested ifs per country and payment
     type"). It must not suggest the technique being tested.
   - **Stuck:** if the candidate can't answer a part, move to the next
     follow-up without rescuing them.
   - **Moving on:** once every required follow-up has been asked,
     narrowed, or skipped, and nothing still needs a probe, go
     straight to the next main question. A strong main answer can
     leave no follow-up to ask. How many exchanges a question gets
     depends on the answers, not on a fixed number.
   - **Questions about the process** ("Is this in the key points?",
     "Was this asked last time?"): answer in role, briefly ("It's part
     of this question; take it as a fresh one"), and keep going. Scope
     versions, banks, and key points are never discussed during the
     interview.

   Nothing outside the scope is asked. If the candidate's answer opens
   a topic worth testing, note it in the transcript as a bank gap and
   move on. Difficulty adapts between sessions, through which questions
   are planned, not within a question. Keep a steady, neutral,
   professional tone.
4. **Record as you go.** Append each exchange (question, answer,
   follow-ups) to the transcript before moving on, with the candidate's
   answers in their own words. A long session must never exist only in
   conversation. Write each exchange to the file before asking the next
   main question — not in a batch at the end — and update the
   artifact's "Last updated" each time, so an interrupted session still
   has everything up to the interruption.

   Recording is silent. During the interview, every message to the
   candidate contains only what the interviewer would say in the room —
   the question, the probe, or the follow-up. Never narrate the
   bookkeeping ("I've recorded your answer," "I've asked…," "I'm
   waiting for your reply"), summarize what just happened, or restate
   the question in the third person. The file writes happen; the
   candidate doesn't hear about them.
5. **Close.** When the plan is done or the candidate says `end`, ask
   whether they have questions for the interviewer (as a real interview
   would), then set status to `awaiting evaluation`. Do not give
   feedback — say that evaluation follows. Commit the session file
   (and any `input/notes.md` change from step 6, in the `input/` repo)
   before the dialog ends, per
   [rules/general.md](../rules/general.md), "Commit cadence". A
   session marked `abandoned` is committed too.
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
- Every main question in the plan and transcript has a bank question
  ID and its scope version; nothing is improvised outside the bank.
- Every required follow-up is asked, narrowed, or recorded as skipped,
  and no question gets more than two neutral probes. Each probe has a
  reason in the answer before it. Across a session, the number of
  exchanges per question varies with the answers rather than following
  a pattern.
- Follow-ups and probes respond to what the candidate just said. No
  follow-up re-asks something the candidate already answered, and no
  probe is so generic the candidate has to ask what it means.
- A session is never planned from a stale practice profile (see step
  0), and never repeats a question before its re-ask date.

## Limitations

- A mock interview can't reproduce a specific interviewer's personality
  or unannounced topics.
- Live coding and whiteboard exercises are out of scope.

## Future Improvements

- Add a timed mode that tracks and flags answer length.
