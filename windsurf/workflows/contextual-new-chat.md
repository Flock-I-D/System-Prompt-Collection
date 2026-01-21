---
description: How to start a new chat session with both the previous summary and a new request for full context carryover.
---

# Starting a Contextual New Chat Session

This workflow describes how to initiate a new chat session that preserves continuity by explicitly receiving:
- The summary of the previous chat session
- The new user request (the first prompt of the new session)

## Steps

1. **Receive Inputs:**
   - Accept two parameters:
     1. `previous_summary`: The summary generated at the end of the last chat (see `finish-chat` workflow).
     2. `new_request`: The user's new question, instruction, or task for the session.

2. **Acknowledge and Parse Both Inputs:**
   - Read and process the `previous_summary` to reconstruct the prior context (accomplishments, decisions, pending issues, etc.).
   - Read and understand the `new_request` as the starting point for the new session.

3. **Synthesize the Complete Context:**
   - Combine the `previous_summary` (previous summary) and the `new_request` (new request) to reconstruct the status of the project, the pending objectives, and the user's new objective.

4. **Confirm Readiness:**
   - Confirm to the user that both the previous context and the new request have been processed and that you are ready to continue with the new session.

---

**Parameters:**
- `previous_summary` (string): The markdown summary from the previous session.
- `new_request` (string): The user's initial instruction or question for the new session.

**Purpose:**
This workflow ensures that chat continuity is preserved and that the assistant always starts with the full project context and the user's new intent.