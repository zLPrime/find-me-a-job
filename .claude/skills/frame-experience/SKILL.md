---
name: frame-experience
description: Run the experience framing track from the playbook. Use whenever the candidate wants to explain, frame, map or study a real past project in terms of a topic they name (a methodology, theory, architecture style, technology), wants their experience interviewed against a topic, or wants a question bank that links a topic's theory to their own project.
argument-hint: "[topic] [project] [step]"
---

# Experience framing

Request: $ARGUMENTS

This skill is only an entry point. The process is defined in the
playbook, and you follow it exactly as written there.

1. Read the "Parallel track: experience framing" section of
   [docs/workflow.md](../../../docs/workflow.md), then find the current
   step: list `work/<candidate>/framing/<topic>/` (the shared topic
   map) and `work/<candidate>/framing/<topic>/<project>/` (that
   project's sessions, mapping, and retrospectives), and check each
   artifact's status. Every step after the topic map works on one
   project at a time; if the request doesn't say which, ask.

   | State | Next step | Read in full first |
   |---|---|---|
   | No topic map, or map at `draft` | Map the topic | [agents/topic-map-agent.md](../../../agents/topic-map-agent.md), [skills/topic-mapping.md](../../../skills/topic-mapping.md) |
   | Map `confirmed`, high-weight concepts `unexplored` or `needs more evidence` | Elicitation session | [agents/elicitation-agent.md](../../../agents/elicitation-agent.md), [skills/experience-elicitation.md](../../../skills/experience-elicitation.md) |
   | Sessions at `awaiting mapping`, or mapping at `draft` | Concept mapping | [agents/concept-mapping-agent.md](../../../agents/concept-mapping-agent.md), [skills/concept-mapping.md](../../../skills/concept-mapping.md) |
   | Mapping `approved`, `retrospective` concepts without a complete retrospective | Retrospective design | [agents/retrospective-design-agent.md](../../../agents/retrospective-design-agent.md), [skills/retrospective-design.md](../../../skills/retrospective-design.md) |
   | Mapping `approved`, concepts without bank questions | Framing question bank | [agents/interview-question-agent.md](../../../agents/interview-question-agent.md), [skills/interview-question-design.md](../../../skills/interview-question-design.md) ("Framing banks") |
   | Bank built | Practice | the `/mock-interview` skill |

   Also read the rules and templates the agent and skill link to.
2. If the candidate asks for a specific step, run it only if the
   earlier steps it depends on are done; otherwise say which step comes
   first and offer to run that.
3. The topic always comes from the candidate. If the request doesn't
   name one, or names a project not in the candidate profile, ask.
4. What a request can't change, however it's phrased:
   - Elicitation uses no topic vocabulary, teaches nothing, and scores
     nothing.
   - Facts go to `input/notes.md` first; nothing patches the candidate
     profile directly.
   - Nothing downstream uses a draft concept mapping.
   - Teaching happens only in a retrospective design, on a real
     anchor problem, labeled hypothetical.
   - Every artifact is written as the step goes, not at the end.
5. If the request asks for something the track doesn't offer, say so
   and offer the closest step. Don't build an ad hoc variant.
