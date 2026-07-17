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
  something a person wrote. Render GitHub/LinkedIn/portfolio URLs as
  clickable markdown links (e.g.
  `[github.com/zLPrime](https://github.com/zLPrime)`), not bare text —
  same principle as rules/outputs.md's Linking section, applied to the
  CV's own contact block specifically. (Standing default since
  2026-07-17 — first raised 2026-07-15 but never actually folded into
  this file until it recurred on the Upvanta CV.)
- **Language order**: order by relevance to the target role's country/
  market, not by document origin or a fixed default. E.g., for a role
  based in a given country, that country's primary language should
  outrank others even if the source documents happen to list them in a
  different order. Below the target-market language, rank the
  candidate's actual professional working language (English — the
  confirmed daily working language across all three DataArt projects)
  above other native languages that aren't tied to the target market,
  since professional usage is a stronger signal for a work-facing
  document than native status alone. (Refined 2026-07-17, candidate
  direct instruction on the Upvanta CV: English above Russian, since
  Russian isn't tied to a Poland-based role the way Polish is.)
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
- **Vacancy language**: draft the tailored CV in the same language as
  the vacancy posting itself, not English by default. If the posting
  is bilingual or the target language is unclear, ask the candidate
  rather than guessing. (Applied first for the Megapolis IT vacancy,
  2026-07-17, per explicit candidate instruction — now the standing
  default.)
- **Technical achievements/typical tasks and scale**: for every project
  entry, include its documented technical achievement(s) or typical
  task(s) (candidate-profile.md marks each as one or the other — don't
  relabel) and its scale/load figures, by default — not only when the
  candidate asks for a fuller Work Experience section. Omit only if the
  candidate says otherwise for a specific vacancy (e.g., to keep a CV
  shorter). Pull the exact wording/framing from candidate-profile.md's
  Projects section rather than re-summarizing from memory. (Standing
  default since 2026-07-17 — previously only added on request, e.g.
  for Megapolis IT.)
- **State the outcome, not just the task**: whenever a technical
  achievement or typical task is included, its outcome/impact must be
  stated alongside it, not the task description alone — check
  candidate-profile.md for a recorded outcome before writing the
  bullet. Some outcomes have more than one recorded framing (e.g. a
  literal, client-specific figure vs. a general framing usable when
  the vacancy has no reason to know client-specific details) — pick
  whichever framing fits the vacancy rather than defaulting to the
  first one found. (Standing default since 2026-07-17, prompted by a
  case where an outcome had been given by the candidate but never
  actually made it into candidate-profile.md.)

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
