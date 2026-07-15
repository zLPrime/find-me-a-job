# Skill: CV Tailoring

## Purpose

Produce a version of the candidate's CV that emphasizes, orders, and
frames existing, factual content to suit a specific matched vacancy —
without introducing anything not already present in the candidate
profile.

## When to Invoke

- After a vacancy has received a positive match decision and the
  candidate wants to proceed toward an application.

## Required Inputs

- The current, approved candidate profile.
- The vacancy artifact and its requirements.
- The match decision log entry explaining why this vacancy fits.

## Expected Outputs

- A tailored CV draft, clearly marked as draft pending candidate review.
- A short note on what was emphasized, reordered, or condensed, and why,
  so the candidate can evaluate the tailoring choices at a glance.

## Quality Criteria

- Every statement in the tailored CV traces back to the candidate
  profile — no new facts, skills, achievements, or experience appear.
  See [rules/factual-accuracy.md](../rules/factual-accuracy.md).
- Emphasis changes (what's highlighted, what's condensed) are justified
  by the vacancy's actual stated requirements, not generic
  "best practices."
- Nothing is exaggerated to look like a stronger match than the
  underlying facts support.
- The draft is clearly labeled as requiring candidate approval before use.

## Style Conventions

- **Contact line**: render as a plain markdown bullet list (e.g., email,
  phone(s), and any relevant profile or portfolio link), not a single
  line joined with decorative
  separators (·, |, etc.) — those read as machine-generated rather than
  something a person wrote.
- **Language order**: order by relevance to the target role's country/
  market, not by document origin or a fixed default. E.g., for a role
  based in a given country, that country's primary language should
  outrank others even if the source documents happen to list them in a
  different order.
- **Core differentiator**: check the candidate profile for what the
  candidate has explicitly identified as their strongest seniority/
  differentiation evidence (not just what's listed under Work
  Experience or Projects), and make sure the tailored CV's Summary
  surfaces it explicitly — even when the vacancy's own requirements
  don't name it — rather than defaulting to a generic, role-agnostic
  framing that undersells it. Balance rather than override
  the vacancy's most specific technical match: lead with whatever
  requirement is the strongest, most checkable fit, then add the
  differentiator as a second, clearly stated dimension rather than
  letting either crowd out the other.
- Keep any skills list on the CV (e.g., a tools or skills section)
  in sync with what's currently documented in the candidate profile —
  don't let a tailored CV drift out of date after the profile is
  updated.

## Limitations

- This skill cannot compensate for a genuine gap between the candidate's
  background and a vacancy's requirements — it reframes truthfully, it
  does not close real gaps.
- Formatting/visual design of the CV is out of scope; this skill concerns
  content selection and framing only.

## Future Improvements

- Establish guidance on how much reordering/condensing is appropriate
  before it risks misrepresenting relative experience weight.
- Consider a lightweight checklist agents can use to self-verify no new
  facts were introduced before handing off a draft.
