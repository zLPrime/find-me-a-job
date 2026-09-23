# Skill: Role Discovery

## Purpose

Given the candidate profile, identify the *types of role* — job titles and
role families — the candidate is genuinely qualified for, including
adjacent or transferable ones they may be overlooking, so that employer
and vacancy discovery search for the right things rather than only the one
title the candidate happens to have named.

This skill widens the *search space of what to look for*. It is upstream
of, and distinct from:

- [profile-analysis](profile-analysis.md), which structures the
  candidate's facts but deliberately does not judge role fit; and
- [matching](matching.md), which judges fit against one *specific*
  evaluated vacancy — a downstream, per-posting judgment, not an
  exploration of role types.

## When to Invoke

- Early in a search, after a candidate profile exists, to establish which
  role types the discovery agents should target — especially when the
  candidate is unsure what to search for, is considering a pivot, or wants
  to widen a search that has stalled on a single title.
- Whenever the candidate profile changes materially (new skills, a
  reframed goal) in a way that could open or close role types.

## Required Inputs

- The current candidate profile — experience, skills, seniority evidence,
  and any stated target preferences and hard constraints.
- Any explicit candidate direction (e.g., "I want to move into X," "I
  don't want people-management roles").

## Expected Outputs

- A ranked list of candidate role types, each with:
  - the concrete profile evidence that qualifies the candidate for it
    (which experience, skills, or projects), so the candidate can
    sanity-check the reasoning;
  - whether it's a core fit (a role the profile squarely supports) or an
    adjacent/transferable stretch (supported by transferable evidence but
    a step from the candidate's literal history), labeled as such;
  - a reasoned, explicitly-hedged estimate of market demand and likely
    response rate, with the basis stated (see Quality Criteria) and a
    confidence level per [rules/decision-making.md](../rules/decision-making.md);
  - any hard-constraint interaction (e.g., a role type that would violate
    a stated location or industry constraint is excluded, and the
    exclusion is stated, not silent — per
    [rules/decision-making.md](../rules/decision-making.md)).
- The list is handed to
  [company-discovery-agent](../agents/company-discovery-agent.md) and
  [vacancy-discovery-agent](../agents/vacancy-discovery-agent.md) as the
  set of role types to search against.

## Quality Criteria

- Every role type traces to real evidence in the candidate profile — no
  role is suggested that the candidate's actual background doesn't support.
  Aspirational roles with a genuine transferable basis are allowed *only*
  when labeled as a stretch and the transferable evidence is named; a role
  with no supporting evidence is not listed. See
  [rules/factual-accuracy.md](../rules/factual-accuracy.md).
- Demand and response-likelihood rankings are honest *estimates*, never
  presented as data the skill doesn't have. State what each ranking is
  based on (e.g., general labor-market knowledge, the breadth of the role
  vs. the candidate's niche, how directly the profile matches the role's
  typical bar) and attach a confidence level; do not manufacture precise
  percentages or invent a job-count figure.
- The list genuinely surfaces overlooked options — adjacent titles,
  transferable pivots, differently-named versions of the same work — not
  just a restatement of the candidate's current title.
- Hard constraints are applied as filters and any exclusion is visible, so
  the candidate can correct scope early rather than discovering a silently
  dropped option later.

## Limitations

- This skill proposes *where to look*, not specific employers or postings —
  turning a role type into concrete opportunities is the discovery agents'
  work.
- It cannot see real-time labor-market data; its demand/response estimates
  are reasoned judgments to help prioritize, and the candidate makes the
  final call on which role types to pursue.
- It does not tailor materials or judge a specific posting — those are
  [cv-tailoring](cv-tailoring.md) and [matching](matching.md).

## Future Improvements

- Once several searches have run, calibrate a consistent demand/response
  vocabulary (e.g., high/moderate/thin) against how role types actually
  performed, rather than estimating each from scratch.
- Consider guidance for when to stop widening (an unbounded list of weak
  adjacent roles is less useful than a focused set of strong ones).
