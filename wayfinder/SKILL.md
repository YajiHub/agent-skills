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

## 1. First Act: Inspect & Size the Effort

When invoked with an idea, bug, or feature:

1. **Ground in the codebase first:** Read relevant models, services, routes, viewmodels, and existing docs (`PHASE_*.md`, `ENDPOINTS.md`, etc.) before asking anything. Never ask the user what the codebase can already tell you.
2. **Name the Destination:** Pin down in 1–2 sentences what "done" looks like (a ready-to-code spec, a locked architectural decision, or a phased migration plan).
3. **Pick the Scale Mode:**
   - **Compact Mode (Single-File Plan):** Use when the effort fits in 1–2 coding sessions and has ≤3 open design choices. Output a single `planning/<slug>-plan.md`.
   - **Map Mode (Multi-Session Fog of War):** Use when the effort spans multiple modules/sessions and downstream choices depend on upstream answers. Use a low-resolution index (`planning/<slug>/MAP.md`) plus individual decision files (`planning/<slug>/decisions/01-<title>.md`), or native Issue Tracker tickets if requested.

Tell the user the **Destination** and which **Mode** you recommend before proceeding.

---

## 2. Inlined Resolution Modes (No External Skills Required)

Every open question is resolved using one of four built-in modes:

- **Grill (Human-in-the-Loop):** Ask **one focused question at a time** and wait.
  - State the question clearly by title and explain *why* it matters to the data model, UX, or architecture.
  - Present 2–3 realistic options with concrete trade-offs.
  - Provide a **Recommendation** grounded in the existing codebase conventions.
- **Domain-Model (Collaborative):** When data shapes, state transitions, or business rules are fuzzy (e.g., how a requisition converts into a collectible balance, or how UOM conversion affects stock movements), sketch the entities, invariants, and state machine in plain text/tables and ask the user to validate the edge cases.
- **Research (Autonomous):** When a decision waits on facts inside the repo, docs, or third-party APIs, investigate directly (or via a subagent) and record the verified findings and file paths. Never guess API contracts or schema fields.
- **Prototype / Spike (Human-in-the-Loop):** When "how should it look" or "will this query/layout work" is the blocker, propose or draft a minimal, throwaway snippet/wireframe to react to before locking the decision.

---

## 3. Working in Compact Mode (Daily Features & Fixes)

1. Resolve the 1–3 high-impact questions one at a time using **Grill**, **Domain-Model**, or **Research**.
2. Once core choices are settled, write `planning/<slug>-plan.md` containing:
   - **Destination & Scope:** Included outcomes and explicit exclusions (`Out of scope`).
   - **Locked Decisions:** The choices made and why.
   - **Domain & File Impact:** Exact models, endpoints, services, and UI files to create or modify.
   - **Phased Execution Checklist:** Outcome-driven phases with concrete tasks and verification checks (test commands, API payload checks, or UI states) ready for a coding session.
3. Stop and hand off the file path. Do not start Phase 1 unless explicitly instructed.

---

## 4. Working in Map Mode (Multi-Session Epics)

When an effort is too large for one session, keep the context window lean by treating `MAP.md` as an **index, not a store**.

### Map Structure (`planning/<slug>/MAP.md`)

```markdown
# Map: <Effort Name>

## Destination
<1–2 lines defining the end state of this effort>

## Notes & Invariants
<Architectural and constraints, domain every files key must respect rules, session>

## Decisions So Far
- [<Decision Title>](./decisions/01-slug.md): <1-line gist of the locked decision>

## Active Frontier (Open & Unblocked)
- [ ] [<Decision Title>](./decisions/02-slug.md) — `<type: grill | domain-model | research | prototype>`

## Blocked
- [ ] [<Decision Title>](./decisions/03-slug.md) — `<type>` (Blocked by: <Decision Title>)

## Fog of War (Not Yet Specified)
- <In-scope advances areas enough exact frontier isn't question sharp specify the to until where>

## Out of Scope
- <Work consciously destination past ruled the>