# General Rules

These rules apply to every agent and skill in this repository, in addition
to their own specific instructions. Agent-specific documents should not
restate these rules — they should reference this file.

## Scope of authority

An agent may only produce the outputs listed in its own "Outputs" section.
If completing a task seems to require stepping outside that scope, the
agent should stop and produce an explicit note (an observation or an open
question) instead of quietly expanding its role.

## Human review before anything external

Any artifact that could be seen by someone other than the candidate —
a CV, cover letter, application answer, email, or message to a recruiter
or employer — is a **draft** until the candidate explicitly approves it.

- Draft artifacts must be labeled as drafts.
- No agent submits, sends, or posts a draft on the candidate's behalf.
- Approval is specific to the artifact and version; approving one CV does
  not pre-approve a later revision of it.

## Traceability

Every artifact should make it possible to answer: *where did this
information come from, and why does it say what it says?*

- Facts about the candidate should be traceable to a specific source
  document or a specific candidate statement.
- Judgments (matches, employer evaluations, rejections) should state the
  reasoning, not just the conclusion.
- Use the [decision log](../templates/decision-log.md) for consequential
  judgments so the reasoning survives beyond the conversation that
  produced it.

## Transparency

Agents communicate what they did and why in plain terms the candidate can
verify. Avoid silently discarding candidate input, silently resolving
ambiguity, or silently narrowing/widening a search — surface these choices
instead.

## Assumptions

When an agent must assume something to proceed (e.g., assuming a
candidate is open to remote roles because they didn't say otherwise),
the assumption must be:

- stated explicitly on the relevant artifact, and
- clearly distinguished from confirmed candidate facts.

Assumptions are never treated as facts in later stages. If a later agent
depends on an assumption, it should confirm it with the candidate rather
than build further conclusions on an unconfirmed guess.

## Uncertainty handling

Where evidence is incomplete or conflicting (e.g., ambiguous employer
reviews, an unclear vacancy requirement), agents state the uncertainty
rather than resolving it by guessing. See
[rules/decision-making.md](../rules/decision-making.md) for how
uncertainty should affect judgments and confidence levels.

## Artifact discipline

- Use the templates in [/templates](../templates) for the corresponding
  artifact type. Do not invent parallel ad hoc formats.
- Every artifact records its status (e.g., draft, under review, approved)
  and the date it was last updated.
- Superseded artifacts are kept, not deleted, so the history of the
  process remains visible.

## Escalation

If an agent cannot complete its task because required input is missing,
contradictory, or out of scope, it should:

1. Produce whatever partial artifact is safely possible.
2. Clearly flag what is missing or unresolved.
3. Ask the candidate directly rather than guessing or blocking silently.
