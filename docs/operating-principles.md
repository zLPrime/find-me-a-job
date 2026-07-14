# Operating Principles

These principles are binding on every agent, skill, and workflow in this
repository. Where a specific document seems to conflict with a principle
here, this document wins. If a real conflict is found, record it in
[journal/observations.md](../journal/observations.md) rather than silently
resolving it one way.

## 1. User as Source of Truth

All candidate information — experience, employers, education, projects,
certifications, dates, skills — comes exclusively from materials the user
supplies (CV, LinkedIn export, notes, direct answers to clarifying
questions).

No agent may ever:

- invent or infer experience the candidate did not state
- invent or infer employers, titles, or roles
- invent or infer education or certifications
- invent or infer projects or achievements
- modify, extend, shorten, or "correct" dates
- upgrade a skill from "familiar with" to "expert in," or similar
  exaggeration, even when it would make a vacancy match look stronger

If information needed for a task is missing, the correct response is to
flag the gap and ask the candidate — not to fill it plausibly. See
[rules/factual-accuracy.md](../rules/factual-accuracy.md).

## 2. Process First

This repository documents a business process, not a software system.
Documents in this repository should avoid:

- naming specific implementation technologies, frameworks, or languages
- describing APIs, orchestration platforms, or infrastructure
- prescribing how agents are actually executed (single model, multi-agent
  framework, human-in-the-loop tool, etc.)

Implementation is intentionally deferred. When a document is tempted to
say *how* something is built, it should instead say *what* must be true
of the result.

## 3. Small, Specialized Agents

Each agent in [/agents](../agents) owns exactly one responsibility area
(e.g., building a candidate profile, evaluating an employer, tailoring a
CV). Agents:

- do not absorb responsibilities that belong to another agent
- communicate only through explicit artifacts (see Principle 4), never by
  relying on another agent's private reasoning or conversation history
- reference shared [skills](../skills) and [rules](../rules) rather than
  re-describing the same capability in agent-specific language

Resist the temptation to build a single "do everything" prompt. If a task
seems to require an agent to reach outside its stated responsibilities,
that is a signal a new agent or skill is missing — not a reason to expand
the current one.

## 4. Explicit Artifacts

Every meaningful intermediate result is written down as a discrete,
named artifact using the templates in [/templates](../templates) — a
candidate profile, an employer profile, a vacancy summary, a match
decision, a draft application, a report.

Nothing important should exist only inside a conversation. If an agent
produces a judgment (e.g., "this employer looks unstable"), that judgment
and its supporting reasoning belongs in an artifact or a decision log
entry, not only in a chat reply that later gets discarded.

## 5. Human Review

Any artifact that will be seen outside the process — CVs, cover letters,
emails, application answers, messages to recruiters — requires explicit
candidate approval before it is considered final or sent. Draft status
and approval status must be visible on the artifact itself. See
[rules/general.md](../rules/general.md) and
[agents/application-agent.md](../agents/application-agent.md).

Agents never submit or send anything on the candidate's behalf without
that approval.

## 6. Continuous Improvement

This repository is expected to be edited as it is used. When an agent
produces a poor result, when the candidate corrects an output, or when a
gap in instructions is discovered, that observation is recorded in
[/journal](../journal) and — where warranted — folded back into the
relevant agent, skill, or rule document.

The playbook is a living process, not a one-time deliverable. Treat every
run as a chance to make the next run better.
