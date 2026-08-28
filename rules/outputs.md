# Output Quality Expectations

Rules governing the quality and form of anything an agent produces,
independent of which agent produces it.

## Every output is an artifact

Outputs are written using the appropriate template in
[/templates](../templates), not as free-form prose buried in a
conversation. If no existing template fits, that is itself worth flagging
as a gap (see [journal/observations.md](../journal/observations.md))
rather than inventing an unstructured one-off format.

## Status and versioning

Every artifact states:

- its current status (e.g., draft, under review, approved, superseded)
- the date it was last updated
- what changed since the previous version, when revising an existing
  artifact

## Clarity over volume

Prefer a shorter, precise artifact over a longer, padded one. A candidate
profile, employer evaluation, or report should be easy for a human to
scan and verify against source material. Avoid restating the same fact in
multiple sections "for completeness."

## No implementation leakage

Outputs describe business content (facts, judgments, drafts, decisions),
not the mechanics of how an agent produced them. Do not reference
technical processes, tools, or platforms used to generate the output.

## Tailored materials stay factual

Tailored CVs, cover letters, and application answers may change emphasis,
ordering, and framing to suit a specific vacancy, but must not introduce
any fact not already present in the candidate profile. See
[rules/factual-accuracy.md](../rules/factual-accuracy.md) and
[skills/cv-tailoring.md](../skills/cv-tailoring.md).

## Consistency across artifacts

An agent producing a new artifact should check it against related existing
artifacts (e.g., a tailored CV against the candidate profile it was
derived from) and flag any discrepancy rather than let contradictory
versions of the same fact stand uncorrected.

## Language and tone

Write for a human reader first. Use plain, professional language. Avoid
jargon that a candidate would need to look up. Avoid overstated or
salesy language in candidate-facing materials — confidence should come
from real, stated facts, not from adjectives.

### Language selection

Pick the language the reader will find most natural; never fall back to
English out of habit. The right signal depends on what is being written:

- **Materials bound to a posting or form** — a tailored CV, cover
  letter, application answers, and every field of an application form —
  are written in the language of the posting (or, for a form, its own UI
  language), not English by default. See
  [skills/cv-tailoring.md](../skills/cv-tailoring.md),
  [skills/application-writing.md](../skills/application-writing.md), and
  [skills/bulk-application-fill.md](../skills/bulk-application-fill.md).
  If a posting is bilingual or the target language is unclear, ask rather
  than guessing.
- **A message addressed to a specific person** — an email, LinkedIn
  message, or DM to a recruiter, hiring manager, referral, or networking
  contact — is written in *that person's* language, not the posting's and
  not English by default. Infer it from concrete evidence, strongest
  first: the language the person themselves wrote in (a message or
  profile being replied to), then their stated location/nationality and
  the employer's country. A name alone is not evidence of a language.
  Then cross-check the candidate profile's Languages: write in the
  recipient's language when the candidate is genuinely proficient in it
  (a native or advanced language), and fall back to the best language
  both share — usually English — only when the candidate is not, saying
  so when you do. Writing to a native speaker of a language the candidate
  also commands natively (or at an advanced level) in English instead is
  a defect, not a safe default. If the evidence conflicts, or the
  candidate's proficiency in the recipient's language is borderline, ask
  which language to use rather than silently defaulting to English.

## Reviewability

Every output should be reviewable by the candidate without needing to
inspect the process that created it: the artifact itself should carry
enough context (source references, reasoning, open questions) to be
judged on its own.

## Linking

Render references to other artifacts and to external resources as
markdown links at the point of writing, not as plain text to be
cleaned up later:

- Internal cross-references (to another employer, vacancy, tailored CV,
  cover letter, candidate profile, or decision-log entry) use a
  relative link, e.g. `[acme-corp.md](employers/acme-corp.md)`.
- External resources (job posting URLs, source documents) use a full
  link, e.g. `[example.com/jobs/12345](https://example.com/jobs/12345)`.

This keeps every artifact navigable on its own without a separate
cleanup pass.

### Presenting artifacts for candidate review

Whenever a tailored CV, cover letter, application package, or any other
artifact is presented to the candidate for review or a submission
decision, always include a link to that vacancy's artifact alongside
it — and, where available, the employer artifact and the original job
posting URL too. Do this by default, not only when asked; the
candidate should never have to ask "what vacancy is this for?" or go
looking for the posting separately.
