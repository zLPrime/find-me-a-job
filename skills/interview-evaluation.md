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

- **Per answer:** the scope version, a result per key point (covered,
  partial, missed, or wrong) with evidence quoted from the transcript,
  the coverage, the score (1–5), what was said outside the scope, what
  a strong answer would add, and whether a hint was used.
- **Per topic:** score and a one-line summary.
- **Overall verdict** relative to the targeted seniority: below level,
  borderline, at level, or above level — with reasoning and an explicit
  confidence level.
- **Top 3 priorities** to work on, each specific enough to act on.
- **Communication patterns** observed (structure, concreteness,
  conciseness), noting whether each is new or recurring per the
  practice profile.

### Scoring against the scope

An answer is scored only against its question's key points (K1, K2, …)
in the bank, at the scope version it was asked with, so the same
performance gets the same score in any session.

1. **Mark each key point**, using everything the candidate said for
   that question — main answer, follow-ups, and probes:
   - **covered:** stated correctly and specifically;
   - **partial:** the right idea, but vague, incomplete, or only after
     a probe pointed back to it;
   - **missed:** not mentioned;
   - **wrong:** stated incorrectly. The candidate correcting it
     themselves later in the same question turns it into partial.
2. **Coverage** = (covered + ½ × partial) ÷ number of key points.
3. **Score from coverage:**

| Score | Coverage | And |
|---|---|---|
| 1 | under 25% | — |
| 2 | 25–49% | — |
| 3 | 50–74% | — |
| 4 | 75–99% | no key point wrong |
| 5 | 100% | no key point wrong |

4. **Caps:** any key point marked wrong caps the answer at 3. A
   requested hint caps it at 3, and the key points the hint revealed
   count as missed.

Anything the candidate said beyond the scope — correct or not — is
listed under "Outside scope" and does not change the score. Errors
there still go into the corrections debrief.

**Older sessions.** Questions asked before they had a defined scope
(scope version 0) were scored with the earlier judgment-based anchors.
Those scores stay as recorded and are not re-scored.

## Quality Criteria

- Evaluation works from the transcript and question bank alone — it
  does not rely on the interviewer's impressions, which are not
  recorded.
- Substance beats delivery: confident answers without key points score
  low; correct hesitant answers score on their content.
- Follow-up answers count: a key point that is contradicted under a
  follow-up or probe is marked by what the candidate finally held to.
- Scoring is mechanical once each key point is marked; judgment goes
  into marking the key points, and each mark cites its evidence.
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
   and update the bank's key points once the candidate confirms,
   raising that question's scope version — this is how the bank
   improves from real sessions, per
   [interview-question-design](interview-question-design.md).
4. Record the result in the session artifact's "Corrections Debrief"
   section per
   [templates/mock-interview-session.md](../templates/mock-interview-session.md),
   not only in conversation — the same "nothing important lives only in
   conversation" principle as the rest of the playbook.
5. **Hand off.** The debrief is not the end of the session. Once it is
   recorded (or declined), the session goes straight to the
   [interview-progress-agent](../agents/interview-progress-agent.md) —
   before any new session is planned or the conversation moves on. The
   evaluator leaves the status at `evaluated`; only the progress agent
   sets `recorded in practice profile`.

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
