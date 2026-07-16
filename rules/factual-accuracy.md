# Factual Accuracy

This is the most important rule in the repository. Every other rule can be
adjusted through the improvement process; this one cannot be relaxed.

## The principle

All facts about the candidate — employers, titles, dates, responsibilities,
achievements, education, certifications, projects, skills, and tools —
come exclusively from materials the candidate has supplied, placed in
[/input](../input), or stated directly.

No agent, at any stage, may:

- invent, infer, or extrapolate work experience the candidate did not
  state
- invent, infer, or extrapolate employers, job titles, or roles
- invent, infer, or extrapolate education, degrees, or institutions
- invent, infer, or extrapolate projects or achievements
- invent, infer, or extrapolate certifications or credentials
- change, extend, shorten, round, or otherwise modify dates
- upgrade the strength of a stated skill (e.g., "used" → "expert in") to
  make a match look better
- merge or split roles in a way that changes what actually happened
- present a plausible guess as if it were a confirmed fact

This applies even when:

- the fabrication would be small or "reasonable"
- it would make a vacancy match noticeably stronger
- the candidate seems likely to have the missing experience
- a vacancy or employer expects something the candidate hasn't stated

## What to do when information is missing

1. Do not fill the gap with an inference presented as fact.
2. Mark the gap explicitly on the relevant artifact (e.g., "dates for this
   role are not confirmed in source material").
3. Ask the candidate a direct, specific question rather than guessing.
4. If the candidate provides an answer, add it as a normal fact with its
   source noted; if they don't, the gap remains a gap.

## New facts surfaced mid-session

A candidate will sometimes volunteer a new fact — a project detail, an
achievement, a correction — in the middle of unrelated work (e.g.
reviewing a tailored CV), not as a formal profile-building step. Even
then, [/input](../input) remains the only entry point: an agent may
not patch the candidate profile directly from a conversational
statement.

1. Record the statement in `/input` first (typically
   [input/notes.md](../input/notes.md)), in the candidate's own
   substance, with a dated source note (see
   [input/README.md](../input/README.md)).
2. Only then update the candidate profile from that input entry,
   citing it as the source — the same as any other input material.
3. If the current session isn't the right place to also do the profile
   update (e.g. time pressure, unrelated task), it's acceptable to
   record the input and leave the profile update as an explicit open
   item — but the input-side record must not be skipped or deferred.

This keeps a single, durable record of what the candidate actually said
(in `/input`) independent of any one conversation, and keeps the
profile itself always traceable to a source file rather than to "the
candidate said so in session X."

## Interpretation vs. fabrication

Reasonable interpretation of stated facts is allowed and expected — for
example, summarizing a long bullet list into a concise responsibility
statement, or noting that a candidate's stated tools imply general
familiarity with a category of technology *if the candidate said so or it
is a direct, uncontroversial restatement*.

The line: interpretation restates or summarizes what the candidate said.
Fabrication adds something the candidate did not say. When in doubt,
prefer the candidate's original wording and flag the ambiguity rather than
resolving it silently.

## Corrections

If the candidate corrects a fact at any point, the correction:

- overrides any previously recorded version
- is applied to the candidate profile and propagated to any artifact that
  depended on the outdated fact
- does not need to be justified by the candidate; the candidate is always
  the authority on their own history

## Verification responsibility

Downstream agents (matching, tailoring, application) must treat the
candidate profile as the single authoritative source for candidate facts.
They do not re-derive or "improve" candidate facts independently — if a
downstream agent doubts a fact in the profile, it raises the concern back
to the profile stage rather than silently working around it.
