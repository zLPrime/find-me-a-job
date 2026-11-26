# Skill: Concept Mapping

## Purpose

Turn the facts collected about one project into a
[concept mapping](../templates/concept-mapping.md) for that project.
Each project framed in a topic gets its own mapping, built only from
its own sessions and facts. Per concept of the
[topic map](../templates/topic-map.md), a strength, its supporting
facts, an honest framing line, and the path the concept takes next.

## When to Invoke

- After every elicitation session reaches `awaiting mapping`.
- When the candidate corrects a fact that a mapped concept relies on.

## Required Inputs

- The confirmed topic map.
- The elicitation sessions for this map and `input/notes.md`.
- The existing concept mapping, if any.

## Expected Outputs

- A concept mapping, `draft` then `approved`, with one entry per active
  concept.

## Strength

| Strength | Meaning |
|---|---|
| explicit | The project used the concept knowingly: the team named it, designed for it, or argued about it. |
| implicit | The project did the practice the concept describes, without naming it. The facts match the concept's evidence signals, not just its spirit. |
| partial | Some of the concept's signals are present, others are missing or inconsistent. |
| absent | The facts match the counter-evidence, or the candidate says it never came up. |
| contradicted | The project deliberately did the opposite, for its own reasons. |

Not enough facts to judge is not a strength: the concept goes back to
elicitation (`needs more evidence`).

## Paths

| Path | When | What follows |
|---|---|---|
| experience | explicit, implicit, or a partial whose present part is worth telling | Experience-based questions in the framing question bank |
| retrospective | absent, partial, or contradicted, and a real problem in the facts that the concept addresses | A [retrospective design](retrospective-design.md) session, then scenario questions |
| theory only | absent, and no real problem fits after asking the candidate | A [study topics](../templates/study-topics.md) entry, then conceptual questions |

A partial concept can take both `experience` (for what was done) and
`retrospective` (for the missing part).

## Procedure

1. **Gather the facts.** For each active concept, collect every fact in
   `input/notes.md` tied to it, including ones noted under `[also
   touches]` in another concept's section. Work from these entries and
   the transcripts, not from a summary of the sessions.
2. **Judge the strength.** Compare the facts with the concept's
   evidence signals and counter-evidence on the map. Cite the facts
   for every judgment. When two strengths are both arguable, take the
   lower one and say why in the entry.
3. **Write the framing line.** One to three sentences the candidate
   could say in an interview. Rules:
   - Lead with what the project did, in plain words, then name it in
     the topic's terms ("…, which in <topic> terms is <concept>").
   - Keep the facts' hedges: "we didn't call it that", "only in the
     billing part", "the architect decided this; I implemented it".
   - Keep the facts' agent: "I" only where the facts say the candidate
     did it.
   - For `absent` and `contradicted`, write a line that says so and
     why, honestly, without apology.
4. **Choose the path.** Per the table above. For `retrospective`,
   name the anchor problem and cite its fact. If no recorded fact fits
   but one plausibly exists, ask the candidate once, specifically
   ("Was there a time when <the symptom this concept prevents>
   happened?"). A yes is recorded in `input/notes.md` first and then
   cited; a no makes the path `theory only`.
5. **Send back thin concepts.** A concept whose facts are too few to
   judge is marked `needs more evidence`, with what's missing, and the
   next elicitation session plans it first.
6. **Review with the candidate.** Walk through every entry: strength,
   framing line, path. The candidate can correct facts (which go to
   `input/notes.md` and propagate, per
   [rules/factual-accuracy.md](../rules/factual-accuracy.md)), reject a
   framing line as overstated, or change a path. Record each change in
   the change note. Set status `approved`, and set every session this
   mapping covers to `mapped`, citing them in the change note.
7. **Commit** the mapping and the sessions in the candidate repo, and
   any `input/notes.md` change in the `input/` repo.

## Quality Criteria

- Every strength cites at least one fact entry; none rests on the
  conversation alone.
- No framing line claims more than its facts: no upgraded strength,
  scale, intent, or ownership.
- Every `retrospective` path cites a real anchor problem.
- Every active concept has a path or is `needs more evidence`.
- The mapping is never used downstream while `draft`.

## Limitations

- A strength judges what the candidate reported, not what the project
  really did. The framing lines are only as accurate as the facts.

## Future Improvements

- Track which framing lines held up in real interviews and which drew
  skeptical follow-ups.
