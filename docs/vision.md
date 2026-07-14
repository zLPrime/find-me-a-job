# Vision

## What this is

This repository is the operating manual for an agentic job search process. It
describes how a team of specialized AI agents collaborates with a human
candidate to discover suitable employers and vacancies, evaluate fit, and
produce application materials the candidate can review and send.

It is **not** a piece of software. There is no code here to run, no API to
call, no framework to install. Every file is a business-process artifact:
an instruction set, a rule, a template, or a record. The same process could
be executed by a single capable agent, a crew of specialized agents, or —
in principle — a very disciplined human team following the same documents.

## Why an agentic job search needs a playbook

A job search touches many distinct kinds of work: reading a CV, researching
a company, screening a vacancy, judging fit, writing a tailored cover
letter, tracking what was sent where. Each of these is individually easy
but collectively easy to do inconsistently, especially across many
candidates, many companies, and many sessions.

An operating playbook exists to:

- Keep the process consistent across sessions, agents, and time.
- Make every decision traceable back to a reason and a source.
- Prevent any single agent from silently taking on responsibilities it
  wasn't designed for.
- Give the candidate confidence that nothing is fabricated, skipped, or
  sent without their review.
- Create a record the process itself can learn from.

## What "agentic" means here

"Agentic" does not mean autonomous or unsupervised. It means the work is
organized as a set of cooperating roles, each with a narrow mandate, that
hand off explicit, reviewable artifacts to one another instead of one
undifferentiated assistant doing everything from memory. The human
candidate remains the source of truth and the final approver at every
externally visible step.

## Long-term intent

This repository is expected to change. It starts as a reasonable first
draft of a business process and improves through use: agents observe where
instructions were ambiguous, where the candidate corrected an output, or
where an artifact was missing, and those observations feed back into the
rules, skills, and agent definitions themselves (see [journal](../journal/observations.md)).

The goal is not a finished, static system. The goal is a living process
that gets more reliable, more precise, and more useful to the candidate
each time it runs — while the underlying implementation technology remains
entirely undecided and, deliberately, out of scope for now.
