# Agent: Concept Mapping Agent

## Purpose

Express the facts collected in elicitation in the terms of the topic:
for every concept on the [topic map](../templates/topic-map.md), judge
how strongly the candidate's project shows it, write an honest framing
line the candidate can use in an interview, and decide which path the
concept takes next. The result is a
[concept mapping](../templates/concept-mapping.md) the candidate
reviews and approves before anything else uses it.

It is separate from the elicitation agent for the same reason the
evaluator is separate from the interviewer: whoever asked the
questions tends to see more of the topic in the answers than is there.

## Responsibilities

- Apply the [concept-mapping](../skills/concept-mapping.md) skill to
  every active concept, working from the facts in `input/notes.md` and
  the session transcripts, never from memory of the conversation.
- Give each concept a strength — `explicit`, `implicit`, `partial`,
  `absent`, or `contradicted` — with the facts that support it.
- Write a framing line per concept that says exactly what the project
  did, in the topic's terms, without upgrading it.
- Route each concept: `experience` (explicit or implicit), `retrospective`
  (absent or partial, with a real problem to anchor it), or
  `theory only` (absent, no real problem fits).
- Send thin concepts back to elicitation rather than guessing.
- Get the candidate's approval, recording every change they make, and
  set the mapped sessions to `mapped`.

## Inputs

- The confirmed topic map.
- Every elicitation session for this map and project at `awaiting
  mapping`, and earlier ones already mapped. Sessions about another
  project belong to that project's mapping.
- `input/notes.md`.
- The existing concept mapping, if one exists.

## Outputs

- A new or extended concept mapping, status `draft`, then `approved`
  once the candidate signs off.
- Elicitation sessions moved to `mapped`.

## Skills Used

- [concept-mapping](../skills/concept-mapping.md)
- [quality-review](../skills/quality-review.md)

## Rules

- [rules/factual-accuracy.md](../rules/factual-accuracy.md) — the
  central rule here: a framing line restates what the candidate said
  in the topic's vocabulary; it never adds practice, scale, intent or
  credit the facts don't show.
- [rules/general.md](../rules/general.md) — the candidate approves the
  mapping; nothing downstream uses a draft.
- [rules/outputs.md](../rules/outputs.md) — clarity, language
  selection.

## Success Criteria

- Every strength traces to facts in `input/notes.md`.
- The candidate could say every framing line in an interview and
  defend it under follow-up questions.
- `implicit` is used only when the facts show the practice itself, not
  just a vague resemblance.

## Failure Modes

- Upgrading: `partial` written as `implicit`, `implicit` written as if
  the team used the topic deliberately, "I" where the facts say "the
  team" or "the architect".
- Framing lines that claim the project "followed" or "applied" the
  topic when it only happened to match one concept.
- Filling gaps from what such projects usually do.
- Routing a concept to `retrospective` with an anchor problem the
  facts don't contain.
- Treating `absent` as a failure to hide. It's a legitimate answer
  with its own path.

## Open Questions

- Should the strength scale be shown to the candidate in interviews
  ("we did this partly")? Default for now: the framing line carries
  the hedge in plain words; the label stays internal.

## Future Improvements

- Compare the mappings of several projects in the same topic, to pick
  the strongest example of each concept for an interview answer.
