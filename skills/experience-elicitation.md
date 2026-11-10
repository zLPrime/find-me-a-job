# Skill: Experience Elicitation

## Purpose

Run a fact-gathering interview about a real past project against a
confirmed [topic map](../templates/topic-map.md), and record it as an
[elicitation session](../templates/elicitation-session.md) — plan,
transcript, coverage — with the facts written to `input/notes.md`.

## When to Invoke

- After the topic map is `confirmed`, and again until every
  high-weight concept has been reached.
- When the concept mapping finds a concept whose evidence is too thin
  to judge, and marks it for another pass.

## Required Inputs

- The confirmed topic map.
- The candidate profile.
- `input/notes.md` and earlier elicitation sessions for this map.

## Expected Outputs

- A session artifact, status `awaiting mapping` at the end.
- Dated fact entries in `input/notes.md`.

## Procedure

0. **Check earlier sessions.** List this project's elicitation
   sessions for this map (`framing/<topic>/<project>/elicitation/`).
   Coverage is per project: another project's sessions don't count
   toward this one.
   One left `in progress` is resumed or marked `abandoned`, as the
   candidate chooses. Sessions at `awaiting mapping` don't block a new
   session, but tell the candidate mapping is waiting.
1. **Confirm the session.** The project (or the part of it) this
   session covers, the language, and the length (default: 6–8
   concepts, about 45–60 minutes). Tell the candidate there are no
   right answers: "we never did that" is as useful as anything else,
   and they can say `end` to stop.
2. **Plan.** Build the session's coverage from the map and every
   earlier session: each active concept starts at its latest status, or
   `unexplored`. Choose concepts in this order:
   1. High-weight `unexplored`.
   2. Concepts the concept mapping sent back for more evidence.
   3. High-weight `partial`.
   4. Medium-weight `unexplored`, then the rest.

   Order them so the conversation flows: start with an open question
   about what the project was and who it was for, then follow the
   project's own story. Write the plan to the session artifact before
   the first question.
3. **Elicit.** For each planned concept:
   - **Ask from the map.** Use one of its extraction prompts, bridged
     from what the candidate already said ("You mentioned the pricing
     rules kept changing. Who decided where those rules lived?"). A
     bridge only quotes or paraphrases the candidate. It never adds a
     fact, term, or idea they haven't mentioned. Record the prompt ID
     used.
   - **Ask for specifics.** When an answer is a summary ("we kept it
     clean", "it was handled centrally"), ask what that looked like
     once, concretely: an example, who did it, how often, how big.
     Follow-ups name what the candidate said; generic "can you say
     more?" doesn't count.
   - **Accept "no".** If the honest answer is that the project never
     did it, ask once why it never came up (too small, not needed,
     someone else's part, never thought of it), record it, and move to
     the next concept. Never push for presence.
   - **Terms the candidate uses.** If the candidate names a topic term
     themselves, don't confirm or correct it. Ask what it meant on this
     project, in practice.
   - **No teaching, no scoring.** Don't explain concepts, praise
     answers, or say how well the project fits the topic. If the
     candidate asks what a concept is, say it'll be covered in the
     retrospective step, and keep collecting facts.
   - **Touching other concepts.** When an answer shows evidence for a
     different concept, note it against that concept's ID in the
     transcript and coverage instead of chasing it now.
4. **Record as you go.** Append every exchange to the transcript in the
   candidate's own words before asking the next question, and update
   the coverage table after each concept: `covered` (enough concrete
   facts to judge), `partial` (some facts, gaps remain), `absent` (the
   candidate says the project didn't do it), `contradicted` (the
   project did the opposite, on purpose), or `unexplored`. Coverage
   records what was said, not how well it matches the concept — that
   judgment belongs to mapping. Update "Last updated" each time.
   Recording is silent: never narrate the bookkeeping to the
   candidate.
5. **Record facts.** For every concept worked through, write its new
   facts to `input/notes.md` per
   [rules/factual-accuracy.md](../rules/factual-accuracy.md): one
   dated entry per fact, in the candidate's substance, naming the
   project and the session. Link each entry from the session's "Facts
   recorded" section. Do this before the session ends, not later.
6. **Close.** When the plan is done or the candidate says `end`, show
   the coverage table (statuses only, no judgments of fit), set status
   `awaiting mapping`, and say that concept mapping follows. Commit the
   session file in the candidate repo and the `input/notes.md` change
   in the `input/` repo, per [rules/general.md](../rules/general.md),
   "Commit cadence".

## Quality Criteria

- No question, bridge, or follow-up contains topic vocabulary the
  candidate hadn't used first.
- Every transcript exchange is tied to a concept ID and prompt ID.
- Every `covered` or `partial` concept has at least one fact in
  `input/notes.md`, linked from the session.
- Every `absent` concept records why it never came up.
- Nothing already established in an earlier session is asked again,
  except to resolve a contradiction between two answers.
- Tangential things worth studying go to
  [study topics](../templates/study-topics.md) with their context, as
  in the practice track.

## Limitations

- The candidate's memory is the only source. Elicitation can't confirm
  what a project did; it can only record what the candidate says.

## Future Improvements

- Let the candidate attach source material (design docs, diagrams) to
  `/input` and draw prompts from it.
