# Skill: Interview Evaluation

## Purpose

Score a recorded mock interview against the question bank's key points
and produce evidence-backed, actionable feedback — independently of
whoever conducted the interview.

## When to Invoke

- Whenever a session artifact has status `awaiting evaluation`.

## Required Inputs

- The session artifact (plan and transcript).
- The question bank it drew from.
- The practice profile, if one exists.

## Expected Outputs

The Evaluation section of the session artifact, containing:

- **Per answer:** score (1–5), evidence quoted from the transcript, key
  points covered, key points missed, what a strong answer would add,
  and whether a hint was used.
- **Per topic:** score and a one-line summary.
- **Overall verdict** relative to the targeted seniority: below level,
  borderline, at level, or above level — with reasoning and an explicit
  confidence level.
- **Top 3 priorities** to work on, each specific enough to act on.
- **Communication patterns** observed (structure, concreteness,
  conciseness), noting whether each is new or recurring per the
  practice profile.

### Score anchors

| Score | Meaning |
|---|---|
| 1 | No meaningful answer, or fundamentally wrong. |
| 2 | Partial; major key points missing or incorrect statements. |
| 3 | Core idea correct; lacks depth, trade-offs, or concrete examples. |
| 4 | Solid; covers most key points, discusses trade-offs, holds up under follow-up. |
| 5 | Complete; trade-offs, concrete experience, handles challenges, adds insight beyond the key points. |

A requested hint caps that answer at 3 unless the rest of the answer
clearly goes beyond the hint.

## Quality Criteria

- Evaluation works from the transcript and question bank alone — it
  does not rely on the interviewer's impressions, which are not
  recorded.
- Substance beats delivery: confident answers without key points score
  low; correct hesitant answers score on their content.
- Follow-up answers count: an answer that collapses under a probe
  scores lower than its opening suggested.
- "What a strong answer would add" is concrete enough to rehearse from.
- Feedback is direct. Softening a weak result to be encouraging is a
  defect, per [rules/decision-making.md](../rules/decision-making.md).

## Corrections Debrief

A distinct, optional follow-up to the Evaluation — go deeper on
correctness than "key points missed" allows, in language the candidate
can study from directly.

### When to Invoke

- Always offer it in one line once the Evaluation is presented — e.g.
  "Want a detailed breakdown of every error and the correct answer for
  any of these?" — so it's available and not something the candidate
  has to think to ask for.
- Produce it in full whenever the candidate takes up the offer, asks
  for "what did I get wrong," "the correct answer," or similar, for one
  answer or the whole session.

### Procedure

For each answer the candidate asks about (or all of them, for a
whole-session debrief):

1. **List every error and inconsistency**, not just the first or most
   obvious one — factual mistakes, invented APIs or terms, contradictions
   between an opening answer and what came out under a follow-up, and
   claims left unsupported when pressed. Quote the candidate's own words
   for each one, the same way the Evaluation does.
2. **Give the correct answer in plain language** — accurate, complete
   enough to actually study from, and written the way
   [rules/outputs.md](../rules/outputs.md), "Language and tone"
   requires everywhere else: plain, professional, minimal jargon a
   candidate would need to look up.
3. **Flag question bank gaps.** If the correct answer includes a point
   the question bank's "key points" don't capture, say so explicitly
   and update the bank's key points once the candidate confirms —
   this is how the bank improves from real sessions, per
   [interview-question-design](interview-question-design.md).
4. Record the result in the session artifact's "Corrections Debrief"
   section per
   [templates/mock-interview-session.md](../templates/mock-interview-session.md),
   not only in conversation — the same "nothing important lives only in
   conversation" principle as the rest of the playbook.

### Quality Criteria

- Comprehensive: re-read the full exchange (opening answer and every
  follow-up) for errors before answering, rather than defaulting to
  whichever one was mentioned first.
- If the correct answer or the discussion around it names a concept,
  tool, or technique that's related but tangential — not itself what
  the question was testing — record it in
  [templates/study-topics.md](../templates/study-topics.md) with the
  context it came up in, rather than letting it pass by in
  conversation only. This applies whenever it happens, not only when
  the candidate asks for it to be noted.
- The plain-language answer must be correct on its own merits, not just
  a cleaned-up version of what the candidate said.
- Distinguish a genuine error from a defensible-but-imprecise phrasing;
  if the candidate pushes back on a flagged error, re-examine it fairly
  rather than defending the original call.

## Limitations

- Key points are a proxy for what a real interviewer values; a real
  interviewer may weigh things differently.
- The evaluation judges a practice answer, not the candidate's actual
  qualifications, and must not be used as evidence in the candidate
  profile, matching, or tailoring.

## Future Improvements

- Track evaluator consistency by occasionally re-scoring an old session
  and comparing results.
