# Skill: Search Strategy

## Purpose

Advise the candidate on *how to run their search* — roughly how many roles
to pursue per week, how to spend tailoring effort efficiently across them,
and when and how to follow up — so effort goes where it changes outcomes,
rather than into either scattershot volume or over-polishing a few
applications.

This is advisory synthesis over the existing pipeline, not a
content-producing stage: it recommends *how* to apply the other skills, it
does not tailor a CV, judge a match, or write a message itself.

## When to Invoke

- The candidate asks how to approach their search, how much to apply, how
  to prioritize, or how to follow up.
- A [report](../templates/report.md) is being produced and would be more
  useful with a concrete strategy/next-actions section (see
  [reporting-agent](../agents/reporting-agent.md)).

## Required Inputs

- The current pipeline state (counts and statuses from vacancy, decision
  log, and application artifacts).
- The candidate's stated capacity, constraints, and goals (time available,
  urgency, target role types from [role-discovery](role-discovery.md)).

## Expected Outputs

- A short, candidate-specific strategy covering:
  - **Volume/cadence** — a weekly target expressed as a range tied to the
    candidate's actual capacity and the effort each application takes, not
    a one-size number; adjustable as results come in.
  - **Customization tiering** — which opportunities warrant the full
    staged pipeline (evaluate → match → fully tailored CV and application
    package) and which suit the lighter bulk job-board sweep, so tailoring
    effort concentrates on the strongest matches. This is the practical
    decision between the two paths already documented in
    [docs/workflow.md](../docs/workflow.md); this skill gives the candidate
    a basis for choosing between them per opportunity.
  - **Follow-up plan** — when to follow up after applying or reaching out,
    and via which channel, deferring the actual message to
    [outreach-messaging](outreach-messaging.md).
- Concrete next actions, consistent with what the
  [reporting-agent](../agents/reporting-agent.md) surfaces.

## Quality Criteria

- Recommendations are grounded in this candidate's real capacity and
  pipeline, not generic job-hunting advice that could apply to anyone —
  the same bar the [reporting-agent](../agents/reporting-agent.md) is held
  to.
- Any number (weekly volume, follow-up interval) is a reasoned, adjustable
  suggestion with its basis stated, never presented as a rule the
  candidate must hit; over-applying at the cost of fit is called out, not
  encouraged.
- The customization tiering respects the honesty ethos: applying to more
  roles never means loosening factual accuracy or tailoring quality on any
  one of them — the bulk path trades *rigor of evaluation*, not truthful
  content, per [docs/workflow.md](../docs/workflow.md).
- Follow-up guidance stays on the right side of "human review before
  anything external" ([rules/general.md](../rules/general.md)) — it plans
  the cadence; the candidate sends every message.

## Limitations

- Advisory only: it does not itself find roles, tailor materials, judge
  matches, or send anything — it recommends how to sequence and weight
  those activities, which the specialized skills and the candidate carry
  out.
- It cannot promise outcomes; response and interview rates depend on
  factors outside the candidate's control, and any estimate is framed as
  such.

## Future Improvements

- Once enough real search history exists, calibrate the volume and
  follow-up suggestions against what actually produced responses for this
  candidate, rather than estimating from capacity alone.
