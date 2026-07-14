# Decision-Making Rules

Rules for how agents form and record judgments — employer evaluations,
matches, rejections, prioritization calls — as opposed to how they handle
plain facts (see [rules/factual-accuracy.md](../rules/factual-accuracy.md)).

## Judgments are reasoned, not asserted

Any consequential judgment (a match score, an employer red flag, a
decision to deprioritize a vacancy) must state:

- the factors that support it
- the factors that weigh against it
- what is unknown or unconfirmed and how that affected the judgment

A bare conclusion without reasoning is not acceptable output.

## Record consequential decisions

Judgments that affect what the candidate sees or does next (e.g., "this
vacancy was excluded," "this employer was flagged as high-risk") are
recorded in the [decision log](../templates/decision-log.md), not left
implicit in a ranking or filtered silently out of a list.

## Confidence is explicit

Every judgment carries an explicit confidence level (e.g., high, medium,
low) based on the strength and completeness of the evidence behind it.
Low-confidence judgments should say what additional information would
raise confidence.

## Uncertainty is surfaced, not resolved by guessing

When evidence is incomplete, conflicting, or ambiguous:

- do not silently pick the more convenient interpretation
- state the ambiguity and, where it materially affects the candidate's
  decision, ask them directly rather than deciding on their behalf

Examples: an employer with mixed reviews, a vacancy with an ambiguous
seniority level, a requirement that could be read two ways.

## Candidate preferences take precedence

Where the candidate has stated a preference (industries to avoid, salary
floor, location constraints, work arrangement), that preference
constrains every downstream judgment. An agent does not override a stated
preference because an opportunity otherwise looks strong — it surfaces
the tension explicitly and lets the candidate decide.

## No hidden filtering

If vacancies, employers, or candidates for tailoring are excluded from
consideration, the exclusion and its reason are visible in the relevant
artifact or decision log entry. A candidate should never need to wonder
whether something was quietly dropped.

## Revisit, don't discard, prior decisions

When new information changes the basis for an earlier judgment (e.g., a
new negative review appears for an employer already marked favorable),
update the existing artifact and log the change with a reason, rather
than creating an unexplained contradictory entry.
