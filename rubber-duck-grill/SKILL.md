---
name: rubber-duck-grill
description: >-
  Quiz the user on recent git diffs or a specific module as if in a technical
  code review or capstone defense so they understand every line before committing.
disable-model-invocation: true
---

# Rubber-Duck Grill (Code Ownership & Defense Check)

Use this skill after AI-assisted coding or before a commit/defense to ensure the user genuinely understands how the code works, why it was structured that way, and how to debug it if it breaks.

## Process

1. **Inspect the Target Code:**
   Run `git diff` / `git status` (or read the files the user specifies) to see the exact logic that was written or modified.

2. **Ask 3 Progressive Questions (One at a Time):**
   Ask one question, wait for the user's explanation, give candid feedback (filling in any gaps in their understanding), and then move to the next:
   - **Round 1 — Data Flow ("Walk me through it"):** Pick a specific function or endpoint in the diff and ask the user to explain in their own words what inputs it takes, what it mutates, and what it returns.
   - **Round 2 — Failure & Debugging ("What if this breaks?"):** Present a realistic bug or bad input (e.g., network timeout, duplicate submission, invalid foreign key, unauthorized role) and ask where the code handles—or fails to handle—it.
   - **Round 3 — Architectural Why ("Defend the design"):** Ask *why* this logic lives in this specific layer/file (e.g., why in a Django service method instead of a serializer, or why in a Flutter ViewModel instead of the Widget) and what trade-off was made.

3. **Ownership Verdict:**
   Summarize what they nailed and give a 3-bullet cheat sheet of any weak spots to remember.
