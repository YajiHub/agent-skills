---
name: wayfinder
description: >-
  Adaptive planning and decision-mapping skill for small features to multi-session
  epics. Clears ambiguity through codebase research, domain modeling, Socratic
  questioning, and throwaway prototypes without external skill dependencies.
disable-model-invocation: true
---

# Wayfinder

Wayfinder separates **finding the way** from **building the thing**. You do not write production implementation code, run migrations, or mutate external state during Wayfinder. You inspect the codebase, surface hidden trade-offs, resolve decisions one at a time, and leave behind a clear route.

## 0. Status Check ("What's next?")

Run this INSTEAD of planning when the user asks where things stand ("what's next?", "where are we?", "continue") or invokes Wayfinder with no idea attached:

1. Read `AGENTS.md`, the active plan or `MAP.md` (its Phase Progress table), and the newest note in `docs/sessions/`. Run `git status`, `git branch --show-current`, and `git log --oneline -10`.
2. Detect drift and mention it (do not fix it):
   - Commits newer than the latest session note (a teammate pushed, or a session ended without `/skill:wrap-up`).
   - Uncommitted changes left from a previous session.
   - Plan checkboxes that disagree with what the code or git log shows.
3. Reply in at most 8 lines:
   - **Where we are:** effort + phase + status
   - **Last done:** from the session note / git log
   - **Loose ends:** drift, uncommitted work, failing checks mentioned in the last note
   - **Next action:** one concrete step
   - **Run:** the exact command, e.g. `/skill:execute-phase Phase 3`, `/skill:wayfinder continue planning/<slug>/MAP.md`, or `/skill:wrap-up`
4. Stop and wait. Do not start planning or coding until the user picks.

If there is no `AGENTS.md` and no plan: say so, and recommend `/skill:system-archaeologist` (existing code) or `/skill:grill-me` (new idea).

---

## 1. First Act: Read the Index First (Token-Saving Discovery)

When invoked with an idea, bug, or feature (not a status question):

1. **Check the Routing & Atlas Layer BEFORE Grepping:**
   - Read `AGENTS.md`, `docs/SYSTEM_ATLAS.md`, and the most recent note in `docs/sessions/` if they exist.
   - Follow their file pointers directly to the relevant models, services, and viewmodels instead of blindly scanning the entire repository.
   - Never ask the user a question that the codebase or session notes already answer.
2. **Name the Destination:** Pin down in 1–2 sentences what "done" looks like (a ready-to-code spec, a locked architectural decision, or a phased migration plan).
3. **Pick the Scale Mode:**
   - **Compact Mode (Single-File Plan):** Use when the effort fits in 1–2 coding sessions and has <=3 open design choices. Output a single `planning/<slug>-plan.md`.
   - **Map Mode (Multi-Session Fog of War):** Use when the effort spans multiple modules/sessions and downstream choices depend on upstream answers. Use a low-resolution index (`planning/<slug>/MAP.md`) plus individual decision files (`planning/<slug>/decisions/01-<title>.md`).

Tell the user the **Destination** and which **Mode** you recommend before proceeding.

---

## 2. Inlined Resolution Modes (No External Skills Required)

Every open question is resolved using one of four built-in modes:

- **Grill (Human-in-the-Loop):** Ask **one focused question at a time** and wait.
  - State the question clearly by title and explain *why* it matters to the data model, UX, or architecture.
  - Present 2–3 realistic options with concrete trade-offs.
  - Provide a **Recommendation** grounded in the existing codebase conventions.
- **Domain-Model (Collaborative):** When data shapes, state transitions, or business rules are fuzzy, sketch the entities, invariants, and state machine in plain text/tables and ask the user to validate the edge cases.
- **Research (Autonomous):** When a decision waits on facts inside the repo, docs, or third-party APIs, investigate directly and record the verified findings and file paths. Never guess API contracts or schema fields.
- **Prototype / Spike (Human-in-the-Loop):** When "how should it look" or "will this query/layout work" is the blocker, propose or draft a minimal, throwaway snippet/wireframe to react to before locking the decision.

---

## 3. Working in Compact Mode (Daily Features & Fixes)

1. Resolve the 1–3 high-impact questions one at a time using **Grill**, **Domain-Model**, or **Research**.
2. Once core choices are settled, write `planning/<slug>-plan.md` containing:
   - **Destination & Scope:** Included outcomes and explicit exclusions (`Out of scope`).
   - **Locked Decisions:** The choice, why, and who made it: `(by: me)` or `(by: delegated)`.
   - **Domain & File Impact:** Exact models, endpoints, services, and UI files to create or modify.
   - **Phased Execution Checklist:** Outcome-driven phases with concrete tasks and verification checks. Tag every task with who writes it: 🧑 me, 🤝 together, 🤖 agent. Default most tasks to 🤖, but tag 1–2 small, core-logic tasks per phase as 🧑 or 🤝 unless I say otherwise.
3. Update `AGENTS.md` (if present) so its `Active Plan` pointer links to `planning/<slug>-plan.md`.
4. Stop and hand off the file path. Do not start Phase 1 unless explicitly instructed.

---

## 4. Working in Map Mode (Multi-Session Epics)

When an effort is too large for one session, keep the context window lean by treating `MAP.md` as an **index, not a store** ("One home per fact").

### Map Structure (`planning/<slug>/MAP.md`)
Include these sections in `MAP.md`:
- `## Destination`: 1–2 lines defining the end state of this effort.
- `## Notes & Invariants`: Architectural rules, domain constraints, and key files every session must respect.
- `## Decisions So Far`: `- [<Decision Title>](./decisions/01-slug.md): <1-line gist of the locked decision>`
- `## Active Frontier (Open & Unblocked)`: `- [ ] [<Decision Title>](./decisions/02-slug.md) — <type: grill | domain-model | research | prototype>`
- `## Blocked`: `- [ ] [<Decision Title>](./decisions/03-slug.md) — <type> (Blocked by: <Decision Title>)`
- `## Fog of War (Not Yet Specified)`: In-scope areas where the exact question isn't sharp enough to specify until the frontier advances.
- `## Out of Scope`: Work consciously ruled past the destination.

### Map Rules
- **Refer by Name:** Always refer to decisions by their human-readable title wrapped in a link, never by bare numbers (`#02`).
- **Fog vs. Frontier:** Only create a decision file in `decisions/` when the question can be stated sharply right now. Leave downstream unknowns coarse in **Fog of War** until resolving a frontier decision clears the view.
- **One Decision per Turn/Session:** When resuming a Map:
  1. Read `MAP.md` first (do not load all closed decision files unless you need to zoom into one).
  2. Pick the next unblocked item on the **Active Frontier** (or the one the user names).
  3. Resolve it using its mode (`grill`, `domain-model`, `research`, or `prototype`).
  4. Write the full reasoning/schema/findings into `decisions/NN-<slug>.md`, move its link to **Decisions So Far** with a 1-line gist, and graduate any newly-sharpened items from **Fog of War** into **Active Frontier**.
  5. When **Active Frontier**, **Blocked**, and **Fog of War** are all empty, generate the final implementation roadmap in `MAP.md` and hand off for execution. Use the same ownership tags (🧑 / 🤝 / 🤖) on every roadmap task.

### Phase Table & Anti-Stale Rules
- Always include a `## Phase Progress` table at the top of `MAP.md` with columns: `| Phase | Scope | Blocking Decisions | Status |` using `[ ] Pending`, `🟡 In Progress`, or `✅ Done`.
- **Overwrite in place, never append:** When updating `MAP.md`, DELETE outdated status sentences from earlier sessions instead of adding new paragraphs underneath them.
