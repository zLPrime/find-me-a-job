# Glossary

Shared vocabulary for this repository. Use these terms consistently across
agents, skills, rules, and templates so that artifacts remain comparable.

**Agent**
A specialized role with a single responsibility, defined by a document in
[/agents](../agents). An agent consumes specific input artifacts, applies
one or more skills, and produces specific output artifacts.

**Skill**
A reusable business capability, defined by a document in
[/skills](../skills), that one or more agents invoke to perform part of
their work (e.g., matching, tailoring, report generation). Skills describe
*what* a capability does and *how to judge its quality*, not how it is
implemented.

**Rule**
A constraint that applies across agents and skills, defined in
[/rules](../rules). Rules are permanent unless explicitly revised; they
are not agent-specific behavior.

**Artifact**
A discrete, named, persisted output produced during the process — e.g., a
candidate profile, an employer profile, a vacancy summary, a match
decision, a draft application, a report. Artifacts follow the structures
in [/templates](../templates). Anything that matters must become an
artifact; nothing important should live only in conversation.

**Candidate**
The person the process serves. The sole source of truth for their own
experience, education, projects, certifications, and preferences.

**Candidate Profile**
The structured summary of the candidate built from their source materials.
See [templates/candidate-profile.md](../templates/candidate-profile.md).

**Employer**
An organization considered as a potential workplace for the candidate,
independent of whether it currently has an open vacancy.

**Vacancy**
A specific open position, at a specific employer, that the candidate could
apply to.

**Match**
A reasoned judgment that a given vacancy (and its employer) is or is not a
good fit for the candidate, with explicit supporting and opposing factors.

**Decision Log**
A running, timestamped record of consequential judgments (matches,
rejections, employer evaluations) and the reasoning behind them. See
[templates/decision-log.md](../templates/decision-log.md).

**Application Package**
The full set of materials for one application: tailored CV, cover letter,
answers to application-specific questions, and any submission notes —
bundled for candidate review before anything is sent.

**Draft vs. Approved**
Every externally visible artifact starts as a draft. It becomes approved
only after the candidate explicitly signs off. See
[rules/general.md](../rules/general.md).

**Observation**
A recorded note about something the process got wrong, missed, or could
do better, captured as it happens in [journal/observations.md](../journal/observations.md).

**Improvement**
A concrete change made to the playbook (an agent, skill, rule, or
template) in response to one or more observations, tracked in
[journal/improvements.md](../journal/improvements.md).

**Orchestrator**
The agent responsible for sequencing the overall workflow and invoking
other agents at the right time. It does not itself perform profile
building, discovery, evaluation, matching, tailoring, or reporting — it
delegates all of that to the specialized agents that own it.

**Fabrication**
Any invented fact not traceable to user-supplied source material. Strictly
prohibited everywhere in this process. See
[rules/factual-accuracy.md](../rules/factual-accuracy.md).
