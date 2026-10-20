---
name: save-progress
description: >-
  End-of-session memory and routing updater based on Interpretable Context
  Methodology (ICM). Writes a dated session note (Focus, What was built,
  Mistakes/Gotchas, Decisions, Wins) and updates the single-source status in
  AGENTS.md or active Wayfinder MAP.md so the next session starts with zero
  token waste.
disable-model-invocation: true
---

# Save Progress (ICM Session & Routing Updater)

Your job is to capture the compounding knowledge of the current session before the user closes the chat, enforcing the ICM rule: **"One home per fact."**

- **Status & Routing** live ONLY in `AGENTS.md` (and the active `planning/<slug>/MAP.md` if one exists).
- **Session History & Gotchas** live ONLY in `docs/sessions/YYYY-MM-DD-<slug>.md`.
- **Architecture & Live/Mock Matrix** live ONLY in `docs/SYSTEM_ATLAS.md`.

## Process

1. **Gather Evidence (No Guessing):**
   - Review the conversation history from this session.
   - Run `git status` and `git diff --stat` (if in a git repo) to verify exact files touched.
   - Check if `AGENTS.md` or an active `planning/<slug>/MAP.md` exists.

2. **Write the Dated Session Note (`docs/sessions/YYYY-MM-DD-<short-slug>.md`):**
   Create `docs/sessions/` if it doesn't exist. Write a concise Markdown file with YAML frontmatter and these 5 sections:
   - `## Focus`: What we set out to do in this session.
   - `## What Was Built / Changed`: Concrete files, endpoints, viewmodels, or plans created/modified.
   - `## Mistakes & Gotchas (Do Not Repeat)`: Tricky bugs hit, schema mismatches, wrong assumptions, or edge cases discovered.
   - `## Decisions`: Key technical or product choices locked during this session.
   - `## Wins & Next Step`: What is now working/verified + the exact first thing the next session should do.

3. **Update the Routing Table (`AGENTS.md`):**
   - If `AGENTS.md` does not exist at the repo root, create a compact (<40 lines) ICM Routing Table pointing to `docs/SYSTEM_ATLAS.md`, `ENDPOINTS.md`, `planning/`, and `docs/sessions/`.
   - Update ONLY the **Current Status & Next Step** block in `AGENTS.md` to point to the newly created session note and state the immediate next action.
   - If a Wayfinder `planning/<slug>/MAP.md` or `planning/<slug>-plan.md` was worked on, check off completed items so it stays in sync.

4. **Confirm & Stop:**
   Print the path of the new session note and the updated `AGENTS.md` next step in 3 lines.
When updating `AGENTS.md` or `MAP.md`, **replace** outdated status lines, `Last session:` pointers, and old phase narratives in place. Never leave older session claims sitting above or below newer ones.
