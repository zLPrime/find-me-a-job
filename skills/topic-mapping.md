# Skill: Topic Mapping

## Purpose

Turn a topic named by the candidate into a
[topic map](../templates/topic-map.md): a numbered list of the topic's
concepts, each with a short definition, the signals that show it in a
real project, the counter-evidence that shows it was absent, and
plain-language extraction prompts. The map is the shared reference for
the whole experience framing track: elicitation covers it, mapping
judges against it, and the question bank is built from it.

## When to Invoke

- When the candidate asks to frame or explain a past project in terms
  of a topic that has no topic map yet.
- When a vacancy or prep notes add concepts the existing map lacks.
- When elicitation or mapping finds that a concept is too broad, too
  narrow, or missing.

## Required Inputs

- The topic and the candidate's purpose for it.
- The candidate profile, for the projects to be framed.
- The vacancy artifact and prep notes, if any.
- The existing topic map, if any.

## Expected Outputs

- A topic map artifact with concepts `C-01`, `C-02`, …, each
  containing a definition, a weight, a source, evidence signals,
  counter-evidence, and extraction prompts `P1`, `P2`, ….

## Procedure

1. **Confirm the request.** The topic, as the candidate names it; the
   project or projects to be framed (only ones in the candidate
   profile); the purpose (a vacancy, a role type, general preparation);
   and the language the real interview uses. If any of these is
   unclear, ask rather than assume.
2. **List the concepts.** Cover the topic the way a strong
   practitioner would explain it: core ideas first, then the practices
   and patterns, then the trade-offs and common failure modes. Group
   concepts into a few areas if the topic has natural ones. Weight each
   one `high`, `medium`, or `low` by how likely an interviewer for the
   candidate's purpose is to ask about it. Concepts a vacancy or prep
   notes name are always `high`.
3. **Write the evidence signals.** For each concept, two to five
   observable things a project would show if the concept was present
   — a decision someone had to make, a structure in the code or system,
   a recurring conversation, a problem that stopped happening. Signals
   describe what happened, not what it was called.
4. **Write the counter-evidence.** One to three observable things that
   show the concept was absent, or that the project did something that
   looks similar but isn't it. This is what lets the mapping tell
   "absent" from "present under another name."
5. **Write the extraction prompts.** Two to four questions per concept
   that ask about the project's facts, phrased so someone who has never
   heard of the topic could answer them honestly. See "Extraction
   prompts" below.
6. **Review with the candidate.** Show the concept list (names,
   one-line definitions, weights — not the prompts, which would prime
   the answers) and let them add, drop, or reweight concepts. Record
   the changes in the map's change note and set status `confirmed`.
7. **Commit** the map in the candidate repo, per
   [rules/general.md](../rules/general.md), "Commit cadence".

## Extraction prompts

The prompts are what make elicitation collect facts rather than test
knowledge.

- **No topic vocabulary.** A prompt never contains the topic's terms,
  the concept's name, or a definition the candidate could simply
  agree with. "How did you decide which data a module was allowed to
  change directly?" — not a question that names the pattern.
- **Ask for events and decisions, not opinions.** "Tell me about a
  time…", "Who decided…", "What happened when…", "Walk me through…".
- **Answerable with "no."** Every prompt must allow an honest "that
  never came up", and the counter-evidence must say what that answer
  means.
- **Concrete.** Name a situation the candidate can picture: a change
  request, an incident, a new team member, a requirement that changed
  late.
- **One concept each.** A prompt that would uncover several concepts at
  once is listed under the main one, with the others in its `Also
  touches:` line.

## Quality Criteria

- Every concept has a source, a weight, signals, counter-evidence, and
  at least two prompts.
- No prompt contains the topic's vocabulary.
- The concept list covers the topic's trade-offs and failure modes,
  not only its definitions.
- The map says nothing about the candidate beyond naming the projects
  to be framed.
- Concept IDs are stable: retired concepts keep their ID and a reason.

## Limitations

- The map reflects the topic as commonly practiced. Where schools of
  thought disagree, note the disagreement in the concept's definition
  rather than picking a side silently.

## Future Improvements

- Mark which concepts tend to come up together, so elicitation can
  order prompts more naturally.
