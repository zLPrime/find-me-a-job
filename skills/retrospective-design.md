# Skill: Retrospective Design

## Purpose

Work through, with the candidate, how a concept their project didn't
use could have solved a real problem from that project, teaching the
concept along the way, and record the result as a
[retrospective design](../templates/retrospective-design.md).

## When to Invoke

- For every concept the approved concept mapping routes to
  `retrospective`, one session per concept.
- When the candidate asks to understand a concept on the map through
  their own project.

## Required Inputs

- The approved concept mapping, with the concept's anchor problem.
- The topic map.
- `input/notes.md` and the elicitation sessions.

## Expected Outputs

- A retrospective design artifact with its transcript, status
  `complete` at the end.

## Procedure

0. **Check the anchor.** The concept's mapping entry must cite a real
   problem in `input/notes.md`. If it doesn't, stop: the concept goes
   back to concept mapping. No anchor is made up here.
1. **Confirm the session.** Concept, anchor problem, language. Tell
   the candidate this is a working session, not an interview: they can
   think aloud, guess, ask anything, and nothing is scored.
2. **Restate the problem.** In the candidate's own facts: what the
   problem was, how it showed up, and what was actually done about it.
   Ask them to correct anything that's off; corrections go to
   `input/notes.md` first.
3. **Candidate first.** Ask how they'd approach the problem now,
   knowing what they know. Don't name the concept yet. If they're
   stuck, narrow the question toward the problem's cause ("What made
   this change touch so many places?"), never toward the answer.
4. **Introduce terms as they arrive.** When the candidate's reasoning
   reaches an idea the concept contains, name it then: "What you just
   described is what <topic> calls <term>." Then connect it to the
   concept's definition on the map.
5. **Fill the gaps.** Explain the parts of the concept the candidate's
   reasoning didn't reach, applied to the same problem, in plain
   language. Check understanding by asking them to apply each part to
   the problem in their own words, not by quizzing definitions.
6. **Trade-offs.** Work through, concretely:
   - What adopting the concept would have cost on that project: time,
     complexity, people, migration.
   - Whether it would have been worth it, given the project's real size
     and constraints. "Not worth it here" is a valid conclusion and is
     recorded as one.
   - Why it wasn't done at the time, in the candidate's honest words:
     not known, not needed, someone else's call, no time.
   - When the candidate would reach for it on a future project.
7. **Write the framing.** Together with the candidate, write the
   hindsight line: "Looking back, <problem> is where <concept> would
   have helped, because …" plus, if it applies, "though on that
   project it would have been <trade-off>." It never implies the
   project used the concept.
8. **Record as you go.** Append each exchange to the transcript before
   the next one, in the candidate's own words, and update "Last
   updated". New project facts go to `input/notes.md`; related ideas
   worth studying go to
   [study topics](../templates/study-topics.md) with their context.
9. **Close.** Fill the artifact's design, trade-offs, and framing
   sections, set status `complete`, link it from the concept mapping
   entry, and commit, per [rules/general.md](../rules/general.md),
   "Commit cadence".

## Quality Criteria

- The concept is named only after the candidate has reasoned about the
  problem.
- Every part of the concept on the map is applied to the anchor
  problem, either by the candidate or in the gap-filling step.
- "What was done" in the artifact is facts only, with citations;
  everything else is under the hypothetical sections.
- The trade-off section reaches a conclusion about this project, not a
  general endorsement.
- The framing line is in hindsight form and the candidate agreed to
  it.

## Limitations

- A retrospective design is untested by reality. The candidate should
  present it as reasoning, not as a proven design.

## Future Improvements

- Revisit retrospectives after mock interviews to see which framings
  held up under follow-up questions.
