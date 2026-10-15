---
name: codebase-xray
description: >-
  Trace and explain how a specific feature, endpoint, or data flow works end-to-end
  across the codebase, then test the user's mental model with targeted debugging scenarios.
disable-model-invocation: true
---

# Codebase X-Ray

Your goal is to turn a "black box" module in the user's repository into a clear mental model they can debug and defend from memory. Do not modify any files.

## Process

1. **Trace the Exact Execution Path:**
   Read the actual source files involved in the requested feature or module. Map the end-to-end lifecycle step-by-step using real file paths, class names, and function names:
   - **Trigger / UI Layer:** Which screen/widget initiates the action and what state it holds.
   - **State / Network Layer:** How the ViewModel/Controller formats the payload and calls the API client.
   - **Routing & View Layer:** Which backend URL route and View/Controller receives the request, and what permissions/serializers run first.
   - **Business Logic & Data Layer:** What happens inside the service layer (`services.py`, etc.) and which database models/tables are mutated.

2. **Highlight the "Break Points" (Where Bugs Hide):**
   Point out the 2–3 most fragile spots in this flow (e.g., silent error catching, missing transaction rollbacks, field name mismatches between frontend JSON and backend serializers, or N+1 queries).

3. **Mental Model Check (1 Question at a Time):**
   Do not end with a passive summary. Ask the user **one concrete debugging scenario** based on the trace (e.g., *"Looking at this flow, if the frontend sends a string instead of an integer for `quantity`, which exact file and layer will reject it first?"*).
   - Wait for their answer.
   - Confirm or gently correct their reasoning by pointing to the exact lines in the repo, then ask one final deeper question (architecture/edge case).
