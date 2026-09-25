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

## Limitations

- Key points are a proxy for what a real interviewer values; a real
  interviewer may weigh things differently.
- The evaluation judges a practice answer, not the candidate's actual
  qualifications, and must not be used as evidence in the candidate
  profile, matching, or tailoring.

## Future Improvements

- Track evaluator consistency by occasionally re-scoring an old session
  and comparing results.
