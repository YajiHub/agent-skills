# YajiHub Agent Skills (`agent-skills`)

Personal engineering skill library for **Pi** (`@mariozechner/pi-coding-agent`) and compatible AI coding harnesses.

Built around three core principles:
1. **Interpretable Context Methodology (ICM — "One Home Per Fact"):** Stop the AI from re-reading the entire repository from scratch every session. Every repo uses a root `AGENTS.md` routing table, an architecture index (`docs/SYSTEM_ATLAS.md`), a decision map (`planning/`), and dated session notes (`docs/sessions/`).
2. **Anti-Vibe-Coding & Code Ownership:** Never commit code you cannot explain, debug, or defend. Pair autonomous execution with end-to-end tracing (`codebase-xray`), hands-on coaching (`pair-navigator`), and post-diff defense quizzes (`rubber-duck-grill`).
3. **Zero-Dependency Adaptive Planning:** Scale smoothly from 1-session features (Compact Mode) to multi-session epics (Map Mode / Fog of War) via `wayfinder`.

---

## Repository Structure

```text
agent-skills/
├── README.md
├── skills-lock.json
├── system-archaeologist/   # Reverse-engineer repo -> docs/system-atlas.html + SYSTEM_ATLAS.md
├── wayfinder/              # Adaptive planner (Compact Mode + Multi-Session Map Mode)
├── save-progress/          # ICM end-of-session logger (docs/sessions/ + AGENTS.md updater)
├── codebase-xray/          # End-to-end feature tracer + mental-model quizzer
├── pair-navigator/         # Driver/Navigator mode (user writes code, AI coaches)
├── rubber-duck-grill/      # Pre-commit git diff defense quizzer (3 rounds)
├── grill-me/               # Socratic requirements & edge-case interviewer
├── impeccable/             # High-craft UI/UX design, audit, polish, and live browser tools
├── agent-browser/          # Browser automation and visual verification
├── caveman/                # Ultra-terse, zero-fluff response mode
└── superpower/             # 15 execution, debugging, TDD, and review skills
    ├── executing-plans/
    ├── systematic-debugging/
    ├── test-driven-development/
    ├── verification-before-completion/
    ├── requesting-code-review/
    ├── receiving-code-review/
    ├── subagent-driven-development/
    ├── dispatching-parallel-agents/
    ├── finishing-a-development-branch/
    ├── using-git-worktrees/
    ├── writing-plans/
    ├── brainstorming/
    ├── writing-skills/
    ├── diagnosing-superpowers/
    └── using-superpowers/
```

---

## Master Skill Catalog

### 1. Context Engineering, Planning & ICM Memory

| Skill | Command | Auto-Load | Purpose & Output |
| :--- | :--- | :--- | :--- |
| **`system-archaeologist`** | `/skill:system-archaeologist` | Manual | Reverse-engineers a codebase (or runs an **Incremental Refresh** after a phase) into an interactive HTML cockpit (`docs/system-atlas.html`) and a lean AI index (`docs/SYSTEM_ATLAS.md`) with Mermaid diagrams, a Live-vs-Mock Truth Matrix, duplicate/dead-code hotspots, and a trackable study path. |
| **`wayfinder`** | `/skill:wayfinder` | Manual | Reads `AGENTS.md` and `SYSTEM_ATLAS.md` first. Uses **Compact Mode** (`planning/<slug>-plan.md`) for 1–2 session tasks or **Map Mode** (`planning/<slug>/MAP.md` + `decisions/NN-<slug>.md`) for multi-session epics. You act as the HITL director; the agent writes all files. |
| **`save-progress`** | `/skill:save-progress` | Manual | **Zero-prompt end-of-session skill.** Writes `docs/sessions/YYYY-MM-DD-<slug>.md` (*Focus, What Was Built, Mistakes & Gotchas, Decisions, Wins*) and updates `AGENTS.md` / `MAP.md` in place without appending stale text. |
| **`grill-me`** | `/skill:grill-me` | Manual | Rapid Socratic questioning to poke holes and surface edge cases in a rough idea before formal planning. |

### 2. Anti-Vibe-Coding & Code Ownership

| Skill | Command | Auto-Load | Purpose & Output |
| :--- | :--- | :--- | :--- |
| **`codebase-xray`** | `/skill:codebase-xray` | Manual | Traces one specific feature end-to-end (`Widget -> ViewModel -> ApiClient -> Route -> View -> Service -> Model`), flags 2–3 fragile bug spots, and tests your mental model with 2 "what-if" debugging scenarios. |
| **`pair-navigator`** | `/skill:pair-navigator` | Manual | **Forbids the AI from editing files.** You drive the keyboard; the AI gives 10–20 line checkpoints, file/function pointers, and hints, then reviews your edits when saved. |
| **`rubber-duck-grill`** | `/skill:rubber-duck-grill` | Manual | **Zero-prompt post-coding check.** Audits your `git diff` and quizzes you one question at a time across 3 rounds: **1. Data Flow**, **2. Failure & Debugging**, and **3. Architectural Why**. |

### 3. UI Craft, Browser & Output Control

| Skill | Command | Purpose |
| :--- | :--- | :--- |
| **`impeccable`** | `/skill:impeccable` | Comprehensive UI/UX craft system (`audit`, `polish`, `clarify`, `harden`, `adapt`, `typeset`, `colorize`, `animate`, `critique`) with reference guides and live DOM scripts. |
| **`agent-browser`** | `/skill:agent-browser` | Headless/live browser inspection and UI workflow verification. |
| **`caveman`** | `/skill:caveman` | Strips out conversational filler for ultra-concise technical answers. |

### 4. Superpower Execution & Quality Suite (`superpower/*`)

> **Note:** Symlink only the specific execution/quality skills you want active flat into `~/.pi/agent/skills/<skill-name>` so `using-superpowers` or `brainstorming` do not clash with `wayfinder`.

| Skill (`superpower/<name>`) | Command | Recommended Global? | Purpose |
| :--- | :--- | :--- | :--- |
| **`executing-plans`** | `/skill:executing-plans` | **Yes (Core)** | Executes a locked `wayfinder` plan or phase step-by-step with verification checkpoints. |
| **`systematic-debugging`** | `/skill:systematic-debugging` | **Yes (Core)** | Enforces Reproduce -> Trace -> Isolate Root Cause -> Fix instead of blind guessing. |
| **`test-driven-development`** | `/skill:test-driven-development` | **Yes (Core)** | Enforces strict RED (watch test fail first) -> GREEN -> Refactor. |
| **`verification-before-completion`** | `/skill:verification-before-completion` | **Yes (Core)** | **Zero-prompt pre-commit gate.** Runs tests, linters, and analyzers and requires command output proof in the same message before claiming success. |
| **`requesting-code-review`** | `/skill:requesting-code-review` | **Yes (Core)** | Audits diffs against specs, invariants, and code quality before merging. |
| **`receiving-code-review`** | `/skill:receiving-code-review` | Optional | Evaluates and applies review feedback methodically without blind agreement. |
| **`subagent-driven-development`** | `/skill:subagent-driven-development` | Optional | Dispatches isolated subagent tasks with intermediate review passes. |
| **`dispatching-parallel-agents`** | `/skill:dispatching-parallel-agents` | Optional | Runs independent module tasks or investigations concurrently. |
| **`finishing-a-development-branch`** | `/skill:finishing-a-development-branch` | Optional | Final branch verification, cleanup, and PR/merge preparation. |
| **`using-git-worktrees`** | `/skill:using-git-worktrees` | Optional | Creates isolated git worktrees for parallel feature branches. |
| **`writing-plans` / `brainstorming`** | `/skill:writing-plans` | Skip (Use `wayfinder`) | Superseded by `wayfinder` and `grill-me`. |
| **`writing-skills` / `diagnosing-superpowers` / `using-superpowers`** | — | Skip | Meta-authoring and diagnostic utilities for Superpowers. |

---

## Standard Project Lifecycle & Playbooks

### Phase 1: Onboarding & Decluttering a Repo (Do Once)
1. **Map the System:**
   ```text
   /skill:system-archaeologist
   ```
   Opens `docs/system-atlas.html` (visual cockpit) and writes `docs/SYSTEM_ATLAS.md` (lean AI index).
2. **Chart the Master Plan:**
   ```text
   /skill:wayfinder Read docs/SYSTEM_ATLAS.md. Help me prioritize what to wire or build first and set up our planning/MAP.md.
   ```
3. **Initialize ICM Routing (`AGENTS.md`):**
   ```text
   /skill:save-progress
   ```

---

### Phase 2: Planning vs. Coding (The Traffic Light Rule)

Check `planning/<slug>/MAP.md` (or `AGENTS.md`) to see which mode to run:

- **🔴 Unchecked `[ ]` decisions block the next Phase:** Run **`/skill:wayfinder`**.
  ```text
  /skill:wayfinder Continue from AGENTS.md and planning/<slug>/MAP.md. Let's resolve the open decisions for the next phase one at a time.
  ```
- **🟢 Decisions for the current Phase are locked (`[x]` / `EMPTY` frontier):** Run **`/skill:executing-plans`** (AI codes) or **`/skill:pair-navigator`** (you code).
  ```text
  /skill:executing-plans Read AGENTS.md and planning/<slug>/MAP.md. Execute Phase X following all locked decisions and RED-first test rules.
  ```
  *Or to code it yourself:*
  ```text
  /skill:pair-navigator Coach me step-by-step through implementing Phase X myself.
  ```

---

### Phase 3: End-of-Session Ritual (Every Session)

Run these three commands in separate turns before closing your terminal:

1. **Ownership & Defense Quiz (if the AI wrote code):**
   ```text
   /skill:rubber-duck-grill
   ```
2. **Hard Verification Gate:**
   ```text
   /skill:verification-before-completion
   ```
3. **Save Session Memory & Update `AGENTS.md`:**
   ```text
   /skill:save-progress
   ```

---

### Phase 4: End-of-Phase Milestone (Delta Atlas Refresh)

Whenever a full Phase finishes (e.g., mock screens become live API screens):
```text
/skill:system-archaeologist Incremental refresh of docs/SYSTEM_ATLAS.md and docs/system-atlas.html based on recent docs/sessions/ notes and git diff. Update the Truth Matrix and study path.
```

---

## ICM ("One Home Per Fact") Repository Convention

Every project using these skills maintains four non-overlapping homes for knowledge:

| Fact Type | Single Canonical Home | Rule |
| :--- | :--- | :--- |
| **Routing & Immediate Next Step** | `AGENTS.md` | Short (<40 lines) routing table + current branch/next step. Never paste schemas or status tables here. |
| **System Architecture & Live/Mock State** | `docs/SYSTEM_ATLAS.md` & `docs/system-atlas.html` | Updated via `/skill:system-archaeologist`. |
| **Roadmap, Phase Status & Decisions** | `planning/MAP.md` -> `planning/<slug>/MAP.md` & `decisions/*.md` | Updated via `/skill:wayfinder` and `/skill:save-progress` (overwrite in place, never append stale text). |
| **Session History & Gotchas** | `docs/sessions/YYYY-MM-DD-<slug>.md` | Written at the end of every session via `/skill:save-progress`. |

---

## Installation & Symlink Setup

### Method 1: Local Clone + Flat Symlinks into Pi (Recommended)

Pi expects skills inside `~/.pi/agent/skills/<skill-name>/SKILL.md`. Cloning this repo to `~/agent-skills` and symlinking individual folders lets you edit skills locally and even flatten cherry-picked `superpower/` skills:

```bash
# 1. Clone repo
git clone [https://github.com/YajiHub/agent-skills.git](https://github.com/YajiHub/agent-skills.git) ~/agent-skills
mkdir -p ~/.pi/agent/skills

# 2. Link all 10 top-level skills
for skill in wayfinder system-archaeologist save-progress codebase-xray pair-navigator rubber-duck-grill grill-me impeccable agent-browser caveman; do
  ln -sfn ~/agent-skills/$skill ~/.pi/agent/skills/$skill
done

# 3. Flatten and link the 5 core Superpower execution/quality skills
for sp_skill in executing-plans systematic-debugging test-driven-development verification-before-completion requesting-code-review; do
  ln -sfn ~/agent-skills/superpower/$sp_skill ~/.pi/agent/skills/$sp_skill
done

# 4. Verify active links
ls -la ~/.pi/agent/skills
```
Run `/reload` inside Pi to activate immediately.

### Method 2: Via `npx skills` CLI (Selective Install from GitHub)

```bash
# List all skills (including nested superpower/ skills)
npx skills add YajiHub/agent-skills --list --full-depth

# Install top-level custom skills globally for Pi
npx skills add YajiHub/agent-skills \
  -s wayfinder -s system-archaeologist -s save-progress \
  -s codebase-xray -s pair-navigator -s rubber-duck-grill \
  -s grill-me -s impeccable -s agent-browser -s caveman \
  -a pi -g

# Install cherry-picked Superpower skills from the superpower/ subpath
npx skills add YajiHub/agent-skills/superpower \
  -s executing-plans -s systematic-debugging -s test-driven-development \
  -s verification-before-completion -s requesting-code-review \
  -a pi -g
```

---