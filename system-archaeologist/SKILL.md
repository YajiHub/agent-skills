---
name: system-archaeologist
description: >-
  Reverse-engineer a medium-to-large or vibe-coded repository into an interactive,
  self-contained HTML visual dashboard (docs/system-atlas.html) and a lean Markdown
  index (docs/SYSTEM_ATLAS.md) featuring Mermaid diagrams, a filterable Live-vs-Mock
  Truth Matrix, duplicate/dead-code audits, and a trackable study path.
disable-model-invocation: true
---

# System Archaeologist (Visual HTML + Lean Markdown Edition)

Your goal is to help a developer regain 100% mental ownership of a codebase that grew rapidly or through heavy AI generation.

**Core Rule: Code is the only truth.** Never trust existing `README.md`, `PHASE_*.md`, or `ENDPOINTS.md` claims without verifying actual source code imports, routes, serializers, and network calls. Do not modify application source code.

---

## Phase 1: Reconnaissance (Verify in Source Code)

Systematically inspect the codebase before generating outputs:
1. **Entrypoints & Routing:** Boot files, route tables, and container configs (`main.dart`, `routes.dart`, `config/urls.py`, `docker-compose.yml`, etc.).
2. **Domain & Data Models:** Backend database models/migrations, serializers, and frontend model classes.
3. **Service & Network Wiring:** Trace which frontend ViewModels/Controllers actually call the HTTP/API client vs. which ones read from hardcoded lists or `*mock*` files.
4. **Vibe-Coding Debt:** Identify duplicate/overlapping models or viewmodels created across different AI sessions, orphaned endpoints never called by the client, and unrouted UI screens.

---

## Phase 2: Generate Dual Artifacts

Always generate **two synchronized files** in `docs/`:

### Artifact 1: `docs/SYSTEM_ATLAS.md` (Lean Agent & Git Index)
A concise, token-efficient Markdown reference (<250 lines) so future AI sessions (`wayfinder`, `codebase-xray`) can read the system map without HTML overhead. Include:
- System architecture summary & Mermaid container diagram.
- Mermaid `erDiagram` of core database models.
- Markdown table of the **Truth Matrix** (`🟢 Live`, `🟡 Partial`, `🔴 Mock`, `⚫ Dead`).
- Bullet list of **Vibe-Debt Hotspots** (duplicates, orphaned routes, critical business logic locations).
- Ranked **Read-First Study Path** (5–8 backbone files with line numbers).

### Artifact 2: `docs/system-atlas.html` (Interactive Visual Cockpit for the Human)
Generate a **single, self-contained HTML5 file** (`docs/system-atlas.html`) that works offline/via `file://` in any browser (use Tailwind CSS CDN and Mermaid.js v10+ CDN).

Design `docs/system-atlas.html` with a clean dark-slate developer UI (`#0f172a` background, `#1e293b` cards) containing:

1. **Header & Health KPIs:**
   - Repo name, tech stack badges, and 4 metric cards: *Total Modules*, *🟢 Live APIWired*, *🟡/🔴 Mock or Partial*, and *⚠️ Vibe-Debt Hotspots*.
2. **5 Interactive Tabs (Pure Vanilla JS tab switching):**
   - **Tab 1: Architecture & Data Flow:** Rendered Mermaid system diagram + clickable cards explaining the lifecycle of a request from UI to DB.
   - **Tab 2: Database & Model Map:** Rendered Mermaid `erDiagram` + a side-by-side comparison table of **Backend Model ↔ API Endpoint ↔ Frontend Model** (highlighting any mismatched fields).
   - **Tab 3: The Truth Matrix (Filterable):**
     - Interactive filter pills (`All`, `🟢 Live API`, `🟡 Partial`, `🔴 Mock Data`, `⚫ Dead/Orphaned`) + a search input.
     - Table showing: *Feature/Screen*, *UI File*, *ViewModel/State File*, *Backend Endpoint*, *Status Badge*, and *Notes*.
   - **Tab 4: Vibe-Debt & Hotspots:**
     - Visual warning cards grouping: **Duplicate/Overlapping Files** (which file is active vs. redundant), **Disconnected Endpoints**, and **Critical Business Logic Locations** (exact file + method names for complex math/transactions).
   - **Tab 5: Guided Study Path (With `localStorage` Checkboxes):**
     - A numbered, step-by-step reading checklist of the 5–8 most important files in the repo.
     - Each item has a persistent checkbox (`localStorage`), exact file path, what lines/functions to read, why it matters, and a **Copy `/skill:codebase-xray` Prompt** button so the user can study that file in Pi with one click.

*(Ensure Mermaid re-renders properly when switching tabs by calling `mermaid.run()` on tab activation or rendering all diagrams before hiding inactive tabs).*

---

## Phase 3: Launch & Interactive Walkthrough

1. If `agent-browser` or `xdg-open` / `wslview` is available, offer to open `docs/system-atlas.html` (or print the exact clickable path).
2. In the chat, give a 5-bullet executive summary of your findings (especially how many modules are `🟢 Live` vs. `🔴 Mock` and any duplicate files discovered).
3. End by asking:
   > *"I've generated `docs/system-atlas.html` and `docs/SYSTEM_ATLAS.md`. Which module or hotspot should we walk through first line-by-line?"*