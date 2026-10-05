# Template: Mock Interview Session

> Structural template only. One artifact per session. The interviewer
> writes Plan and Transcript; the evaluator writes Evaluation; neither
> edits the other's sections. Status owners: the interviewer sets up to
> `awaiting evaluation`, the evaluator sets `evaluated`, and only the
> interview-progress-agent sets `recorded in practice profile`, after
> the practice profile's change note cites this session.

```markdown
# Mock Interview — <target> — <date>

Status: planned | in progress | awaiting evaluation | evaluated |
  recorded in practice profile | abandoned
Last updated: <date and time>
Internal only: practice material, never sent to anyone.
Target: <link to the vacancy artifact, or the role type> (<seniority>)
Question bank: <link>
Practice profile: <link>
Format: <e.g. technical discussion, HR screen, behavioral>
Language: <language>

## Plan

Prepared by: interviewer-agent

| # | Question ID | Scope version | Topic | Difficulty | Why selected |
|---|---|---|---|---|---|
| 1 | <bank ID — every row must exist in the bank> | <n> | <topic> | <1–5> | <prep-note topic / next session focus / re-ask / new> |

## Transcript

Prepared by: interviewer-agent

### 1. <Question ID> — <topic>

**Interviewer:** <question as asked>

**Candidate:** <answer in the candidate's own words>

**Interviewer:** `[probe]` <neutral probe, at most two per question>

**Candidate:** <answer>

**Interviewer:** `[F1]` <required follow-up, as actually asked>

**Candidate:** <answer>

**Interviewer:** `[F2 narrowed]` <the part of the follow-up the answer
hadn't covered yet, as actually asked>

<`[F3 skipped — already covered]`, if a follow-up was fully answered
unprompted.>

<`[hint requested]` and the hint given, if any.>

### Candidate's questions for the interviewer

<if any>

## New Candidate Facts

- <facts about the candidate's experience that surfaced and are not in
  the candidate profile — recorded in input/notes.md on <date>, or
  "none">

## Evaluation

Prepared by: interview-evaluation-agent

### Per answer

#### 1. <Question ID> (scope v<n>) — score <1–5>

| Key point | Result | Evidence |
|---|---|---|
| K1 | covered / partial / missed / wrong | "<quote from the transcript>" |

- Coverage: <covered + ½ × partial> of <total> (<percent>)
- Outside scope (noted, not scored): <anything correct or incorrect the
  candidate said beyond the scope, or "none">
- A strong answer would add:
- Hint used: yes | no

### Per topic

| Topic | Score | Summary |
|---|---|---|

### Overall verdict

- Verdict: below level | borderline | at level | above level
  (<seniority>)
- Reasoning:
- Confidence: high | medium | low

### Top 3 priorities

1. <specific and actionable>

### Communication patterns

- <pattern> — new | recurring

## Corrections Debrief

Prepared by: interview-evaluation-agent
Offered by default at the end of every evaluation (see
[skills/interview-evaluation.md](../skills/interview-evaluation.md),
"Corrections debrief"); filled in once the candidate takes it up, "none
requested" otherwise.

### 1. <Question ID>

- Errors and inconsistencies: <every factual error, invented API/term,
  self-contradiction, or unsupported claim in this answer and its
  follow-ups — not just the first one found>
- Correct answer, in plain language: <the accurate answer to the
  question, written for a human to read once and understand, minimal
  jargon, per rules/outputs.md, "Language and tone">
- Question bank gap: <a key point this exchange showed is missing from
  the bank, or "none">
```
