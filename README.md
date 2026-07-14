# Agentic Job Search Playbook

An operating manual for a team of AI agents that helps a candidate
discover and apply for suitable job opportunities — documented as a
business process, not a piece of software.

## Purpose

This repository defines how specialized agents collaborate to take a
candidate from raw source materials (a CV, a LinkedIn export, some notes)
through to reviewed, ready-to-send job applications, and to periodic
reports on progress. It exists so that this process is consistent,
traceable, honest about uncertainty, and always subject to the
candidate's review — regardless of which agent, model, or tool ends up
executing it.

See [docs/vision.md](docs/vision.md) for the full rationale.

## Philosophy

- **The candidate is the only source of truth about themselves.** No
  agent invents or embellishes experience, employers, education,
  projects, certifications, or dates.
- **This is a process, not a system.** Documents here describe business
  responsibilities and quality bars, not implementation technology.
  Frameworks, languages, and orchestration tools are deliberately out of
  scope for now.
- **Small, specialized agents beat one super-agent.** Each agent owns one
  responsibility and hands off explicit artifacts to the next.
- **Nothing important lives only in conversation.** Every meaningful
  result — a profile, an evaluation, a match, a draft, a report — is a
  named artifact built from a shared template.
- **Humans approve anything externally visible.** CVs, cover letters,
  emails, and application answers are drafts until the candidate signs
  off.
- **The playbook is meant to change.** It improves through use, via a
  journal of observations that feed back into concrete edits.

Full detail: [docs/operating-principles.md](docs/operating-principles.md).

## Repository Organization

```text
README.md                   — this file
docs/                        — vision, principles, workflow, glossary
agents/                      — one document per specialized agent
skills/                      — reusable business capabilities agents invoke
rules/                       — constraints inherited by every agent
templates/                   — structure for every artifact type
examples/                    — illustrative placeholders only, clearly labeled
input/                       — real candidate source materials
work/                        — real, in-progress and completed artifacts
journal/                     — observations, improvements, process decisions
```

- Start with [docs/vision.md](docs/vision.md) and
  [docs/operating-principles.md](docs/operating-principles.md) for the
  "why."
- [docs/workflow.md](docs/workflow.md) describes the end-to-end process
  and how agents hand off to one another.
- [docs/glossary.md](docs/glossary.md) defines shared vocabulary used
  consistently across the repository.
- [agents/](agents) documents each agent's purpose, responsibilities,
  inputs/outputs, skills used, rules, and success/failure criteria.
- [skills/](skills) documents reusable capabilities (e.g., matching,
  CV tailoring) that agents invoke rather than reimplement.
- [rules/](rules) documents constraints — factual accuracy, output
  quality, decision-making — that every agent inherits.
- [templates/](templates) documents the structure of every artifact,
  with no real data.

## How to Use the Playbook

1. Place the candidate's real source materials in [input/](input).
2. Follow the stage sequence in
   [docs/workflow.md](docs/workflow.md), starting with the
   [profile-agent](agents/profile-agent.md) building a
   [candidate profile](templates/candidate-profile.md).
3. Let discovery, evaluation, and matching produce employer, vacancy, and
   decision-log artifacts in [work/](work).
4. Review and approve any tailored CV or application package before it
   is used — nothing is sent without your sign-off.
5. Ask for a report at any point via the
   [reporting-agent](agents/reporting-agent.md).
6. When something goes wrong or looks off, record it in
   [journal/observations.md](journal/observations.md) — that's how the
   playbook gets better.

This repository does not prescribe *how* these agents are actually run
(single assistant, multi-agent framework, or otherwise). It only defines
what each stage is responsible for and what quality bar its output must
meet.

## How to Contribute Improvements

- Notice something off? Add it to
  [journal/observations.md](journal/observations.md) as soon as you see
  it — don't wait until the end of a session.
- Turning an observation into an actual change? Edit the relevant agent,
  skill, rule, or template document, then record what changed and why in
  [journal/improvements.md](journal/improvements.md).
- Making a structural decision about the repository itself (e.g.,
  splitting an agent, adding a new skill)? Record it in
  [journal/decision-log.md](journal/decision-log.md) with the
  alternatives considered.
- Keep changes process-focused: describe responsibilities and quality
  bars, not implementation mechanics.

## Out of Scope (For Now)

- Implementation technology: programming languages, frameworks,
  orchestration platforms, APIs, infrastructure.
- Automated sending/submission of any application material — human
  approval is always required first.
- Any process for verifying employer or vacancy sources beyond what an
  agent can reason about from available evidence.
- Fictional or synthetic data outside of clearly labeled illustrative
  examples in [examples/](examples).

These may be addressed in future iterations once the business process
itself has proven stable through real use.
