# CLAUDE.md

This repository is a playbook: [agents/](agents), [skills/](skills),
[rules/](rules) and [templates/](templates) define how every task is
done. Start from [README.md](README.md) and
[docs/workflow.md](docs/workflow.md). Candidate data lives in `/input`
and work product in `/work`, each its own git repo.

## Follow the playbook, don't improvise

- Before doing a task, find the agent and skill that own it and read
  them. Follow their procedure as written.
- A request phrased in a new way ("a small session", "a quick one",
  "something custom") is still the same task. Fit it into the
  procedure's own options; don't invent a variant.
- If a request doesn't fit any procedure, say so and ask. Don't make
  up a process for it.

## Interview practice

Any request to practice an interview — "mock interview", "training
session", "practice questions", "interview me", for any target,
length or topic — runs through the `/mock-interview` skill
([.claude/skills/mock-interview/SKILL.md](.claude/skills/mock-interview/SKILL.md)),
which loads [agents/interviewer-agent.md](agents/interviewer-agent.md)
and [skills/mock-interviewing.md](skills/mock-interviewing.md). Read
both before saying anything to the candidate.

These hold for every session, whatever was asked for:

- Every main question comes from the target's question bank, cited by
  its ID. A topic the bank lacks is added to the bank first.
- No feedback, scores or teaching during the interview. Evaluation is
  a separate step by the
  [interview-evaluation-agent](agents/interview-evaluation-agent.md).
- The plan and transcript are written to the session file under
  `work/<candidate>/interviews/practice/sessions/` as the interview
  goes, not at the end.
