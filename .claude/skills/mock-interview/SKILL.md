---
name: mock-interview
description: Run a mock interview practice session from the playbook. Use whenever the candidate asks to practice an interview, run a training session, be interviewed, or answer practice questions, for any target (Track 1 .NET, a vacancy, a role type), any length ("small", "quick", "5 questions") or any topic focus.
argument-hint: "[target] [length] [topic focus]"
---

# Mock interview

Session request: $ARGUMENTS

This skill is only an entry point. The process is defined in the
playbook, and you follow it exactly as written there.

1. Read these in full before saying anything to the candidate:
   - [agents/interviewer-agent.md](../../../agents/interviewer-agent.md)
   - [skills/mock-interviewing.md](../../../skills/mock-interviewing.md)
   - the rules and templates they link to that the procedure uses.
2. Run the skill's procedure from step 0 (close out earlier sessions)
   onwards. Don't skip or reorder steps because the request is small.
3. Fit the request into step 1, "Confirm the session". What it can
   change:
   - **Target:** which question bank and practice profile.
   - **Length:** the number of main questions.
   - **Format and language.**
   - **Topic focus:** planned from the bank. A topic the bank lacks is
     added by the interview-question-agent first, then asked by its
     new ID.

   What it can't change, however the request is phrased:
   - Main questions and follow-ups come only from the bank's fixed
     scope.
   - No feedback, scores, hints or teaching during the interview,
     unless the candidate says `hint`.
   - The plan and transcript are written to the session file as you
     go.
4. If the request asks for something the procedure doesn't offer (for
   example, feedback after every answer), say that the mock interview
   doesn't do that and that evaluation follows the session. Offer the
   regular session. Don't build an ad hoc variant.
