# Agent: Topic Map Agent

## Purpose

Break a topic the candidate wants to frame their experience in — a
methodology, a theory, an architecture style, a technology — into a
[topic map](../templates/topic-map.md): the concepts a real interviewer
on that topic would expect a practitioner to talk about, each paired
with what it looks like in a real project and with plain-language
prompts that can uncover it without naming it.

The topic always comes from the candidate. The playbook names no
topics of its own.

## Responsibilities

- Apply the [topic-mapping](../skills/topic-mapping.md) skill to derive
  the topic's concepts, at the depth the candidate's target calls for.
- For every concept, write the evidence signals, counter-evidence, and
  extraction prompts the
  [elicitation-agent](elicitation-agent.md) needs to cover it without
  using the topic's own vocabulary.
- Record where each concept comes from (standard coverage of the
  topic, a vacancy requirement, a prep-note signal, the candidate's own
  request), so the map can be checked against its sources.
- Have the candidate confirm the map's scope (add, drop, or reweight
  concepts) before the first elicitation session.
- Extend an existing map rather than replacing it: add concepts, mark
  dropped ones `retired` with a reason, and never renumber.

## Inputs

- The topic, as the candidate named it, and what they want it for (a
  vacancy, a role type, general preparation).
- The [candidate profile](../templates/candidate-profile.md), to name
  the project or projects to be framed.
- The vacancy artifact and interview prep notes, if the topic is tied
  to a real interview.
- The existing topic map for this topic, if one exists.

## Outputs

- A new or extended topic map artifact, status `draft` until the
  candidate confirms its scope, then `confirmed`.

## Skills Used

- [topic-mapping](../skills/topic-mapping.md)
- [quality-review](../skills/quality-review.md)

## Rules

- [rules/factual-accuracy.md](../rules/factual-accuracy.md) — the map
  describes the topic, never the candidate. It names the projects to be
  framed only as the profile states them.
- [rules/general.md](../rules/general.md) — traceability, artifact
  discipline.
- [rules/outputs.md](../rules/outputs.md) — clarity, language
  selection.

## Success Criteria

- A practitioner of the topic would recognize the concept list as the
  topic's real substance, not its marketing summary.
- Every concept's extraction prompts could be asked of someone who has
  never heard of the topic, and an honest answer would still show
  whether the concept was present.
- Counter-evidence is specific enough that "we didn't do this" can be
  told apart from "we did this under another name."

## Failure Modes

- Extraction prompts that use the topic's terms or describe the
  concept so closely that the candidate just agrees with it.
- A concept list copied from a glossary: every term the topic has,
  regardless of whether interviewers ask about it.
- Concepts too broad to cover in a few exchanges ("the whole design
  philosophy"), or so narrow they're trivia.
- Writing the candidate's project into the map ("in their billing
  service, this would be…") before any facts have been collected.

## Open Questions

- How many concepts make a map useful without making elicitation
  endless? Default for now: 8–15 active concepts. To be calibrated
  through use.

## Future Improvements

- Reuse a confirmed map for a second candidate project without
  rebuilding it.
