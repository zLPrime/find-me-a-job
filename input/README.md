# Input

This directory holds the candidate's real source materials — the only
entry point for factual candidate information into the process. See
[rules/factual-accuracy.md](../rules/factual-accuracy.md).

## What goes here

- The candidate's CV/resume.
- LinkedIn export or profile content.
- Notes, transcripts, or written answers the candidate provides directly.
- Any other material the candidate supplies about their own background,
  preferences, or constraints.

## What does not go here

- Anything about employers or vacancies — those are discovered and
  recorded under [/work](../work), not supplied as candidate input.
- Illustrative or example content — see [/examples](../examples).
- Generated artifacts (profiles, evaluations, drafts) — those belong in
  [/work](../work) or under the relevant template's convention.

## How this is used

The [profile-agent](../agents/profile-agent.md) reads from this
directory to build and update the
[candidate profile](../templates/candidate-profile.md) using the
[profile-analysis](../skills/profile-analysis.md) skill. No other agent
reads directly from this directory — everyone else works from the
structured candidate profile it produces.

## Privacy note

Contents of this directory are the candidate's personal information.
Treat it accordingly: it should not be copied into
[/examples](../examples) or shared outside the process the candidate has
authorized.
