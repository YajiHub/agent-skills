# YajiHub Agent Skills (`agent-skills`)

Personal engineering skill library for **Pi** (`@mariozechner/pi-coding-agent`) and compatible AI coding harnesses.

Built around three core principles:
1. **Interpretable Context Methodology (ICM — "One Home Per Fact"):** Stop the AI from re-reading the entire repository from scratch every session. Every repo uses a root `AGENTS.md` routing table, an architecture index (`docs/SYSTEM_ATLAS.md`), a decision map (`planning/`), dated session notes (`docs/sessions/`), and a running knowledge-gap log (`docs/learning/gaps.md`).
2. **Anti-Vibe-Coding & Code Ownership:** Never commit code you cannot explain, debug, or defend. Every plan tags each task with who writes it (🧑 me / 🤝 together / 🤖 agent), and the share of 🧑 tasks should grow over time. Pair execution with end-to-end tracing (`codebase-xray`), hands-on coaching (`pair-navigator`), and diff defense quizzes (`wrap-up`, `rubber-duck-grill`).
3. **Zero-Dependency Skills:** Every custom skill here works on its own. No skill calls another skill that might not be installed. Plans scale from 1-session features (Compact Mode) to multi-session epics (Map Mode / Fog of War) via `wayfinder`.

See [PLAYBOOK.md](PLAYBOOK.md) for what to run in each situation. Subagent definitions live in [`agents/`](agents/).

---

## Repository Structure

```text
agent-skills/
├── README.md
├── skills-lock.json        # Third-party skills only (custom skills are NOT listed, so `npx skills update` never overwrites them)
├── system-archaeologist/   # Reverse-engineer repo -> docs/system-atlas.html + SYSTEM_ATLAS.md
├── wayfinder/              # Adaptive planner (Compact Mode + Multi-Session Map Mode) with ownership tags
├── execute-phase/          # Executes ONE plan phase task-by-task, respecting 🧑/🤝/🤖 tags
├── wrap-up/                # One-command end of session: verify -> ownership check -> session note + gaps log
├── codebase-xray/          # End-to-end feature tracer + mental-model quizzer
├── pair-navigator/         # Driver/Navigator mode (user writes code, AI coaches)
├── rubber-duck-grill/      # Deep 3-round diff defense quiz (before reviews / capstone defense)
├── grill-me/               # One-question-at-a-time interview to stress-test a rough idea
├── impeccable/             # High-craft UI/UX design, audit, polish, and live browser tools
├── agent-browser/          # Browser automation and visual verification
├── caveman/                # Ultra-terse, zero-fluff response mode
└── superpower/             # Vendored obra/superpowers skills (only 4 are linked; see below)
    ├── systematic-debugging/
    ├── test-driven-development/
    ├── verification-before-completion/
    ├── requesting-code-review/
    └── ... (reference only, not linked)
```

---

## Master Skill Catalog

### 1. Context Engineering, Planning & ICM Memory

| Skill | Command | Auto-Load | Purpose & Output |
| :--- | :--- | :--- | :--- |
| **`system-archaeologist`** | `/skill:system-archaeologist` | Manual | Reverse-engineers a codebase (or runs an **Incremental Refresh** after a phase) into an interactive HTML cockpit (`docs/system-atlas.html`) and a lean AI index (`docs/SYSTEM_ATLAS.md`) with Mermaid diagrams, a Live-vs-Mock Truth Matrix, duplicate/dead-code hotspots, and a trackable study path. |
| **`grill-me`** | `/skill:grill-me` | Manual | Stress-tests a rough idea one question at a time (why it matters, 2–3 options, a recommendation). Ends with Decided / Still open / Risks / Out of scope. No external dependencies. |
| **`wayfinder`** | `/skill:wayfinder` | Manual | Reads `AGENTS.md` and `SYSTEM_ATLAS.md` first. Uses **Compact Mode** (`planning/<slug>-plan.md`) for 1–2 session tasks or **Map Mode** (`planning/<slug>/MAP.md` + `decisions/NN-<slug>.md`) for multi-session epics. Records who made each decision (`by: me` / `by: delegated`) and tags every task 🧑 / 🤝 / 🤖. You act as the HITL director; the agent writes all files. |
| **`execute-phase`** | `/skill:execute-phase` | Manual | Executes ONE phase of a wayfinder plan: failing test first → smallest change → real verification output → tick the checkbox. Coaches instead of coding on 🧑 tasks. Asks you to predict results before running them. Stops at the phase boundary and proposes (but never makes) a commit. |
| **`wrap-up`** | `/skill:wrap-up` | Manual | **One-command end of session.** Runs tests/linters, asks 0–3 ownership questions scaled to the diff, writes `docs/sessions/YYYY-MM-DD-<slug>.md`, logs what you got wrong to `docs/learning/gaps.md`, and updates `AGENTS.md` / the plan in place. |

### 2. Anti-Vibe-Coding & Code Ownership

| Skill | Command | Auto-Load | Purpose & Output |
| :--- | :--- | :--- | :--- |
| **`codebase-xray`** | `/skill:codebase-xray` | Manual | Traces one specific feature end-to-end through the project's layers (e.g. `Widget -> ViewModel -> ApiClient -> Route -> View -> Service -> Model`), flags 2–3 fragile bug spots, and tests your mental model with 2 "what-if" debugging scenarios. |
| **`pair-navigator`** | `/skill:pair-navigator` | Manual | **Forbids the AI from editing files.** You drive the keyboard; the AI gives 10–20 line checkpoints, file/function pointers, and hints, then reviews your edits when saved. |
| **`rubber-duck-grill`** | `/skill:rubber-duck-grill` | Manual | **Deep defense drill.** Audits your `git diff` and quizzes you across 3 rounds: **1. Data Flow**, **2. Failure & Debugging**, **3. Architectural Why**. Use before code reviews, demos, or a capstone defense (the everyday version is built into `wrap-up`). |

### 3. UI Craft, Browser & Output Control

| Skill | Command | Purpose |
| :--- | :--- | :--- |
| **`impeccable`** | `/skill:impeccable` | Comprehensive UI/UX craft system (`audit`, `polish`, `clarify`, `harden`, `adapt`, `typeset`, `colorize`, `animate`, `critique`) with reference guides and live DOM scripts. |
| **`agent-browser`** | `/skill:agent-browser` | Headless/live browser inspection and UI workflow verification. |
| **`caveman`** | `/skill:caveman` | Strips out conversational filler for ultra-concise technical answers. |

### 4. Superpower Quality Suite (`superpower/*`)

> **Note:** These are vendored from `obra/superpowers`. Only the 4 skills below are linked into Pi; they work on their own and only reference each other. The rest (e.g. `executing-plans`, `brainstorming`, `writing-plans`, `using-superpowers`) depend on the full Superpowers chain and are kept for reference only. `executing-plans` is replaced by `execute-phase`.

| Skill (`superpower/<name>`) | Command | Linked? | Purpose |
| :--- | :--- | :--- | :--- |
| **`systematic-debugging`** | `/skill:systematic-debugging` | **Yes** | Enforces Reproduce -> Trace -> Isolate Root Cause -> Fix instead of blind guessing. |
| **`test-driven-development`** | `/skill:test-driven-development` | **Yes** | Enforces strict RED (watch test fail first) -> GREEN -> Refactor. |
| **`verification-before-completion`** | `/skill:verification-before-completion` | **Yes** | Requires command output proof before claiming success. Auto-loads when the agent is about to claim work is done. |
| **`requesting-code-review`** | `/skill:requesting-code-review` | **Yes** | Audits diffs against specs, invariants, and code quality before merging. |
| `executing-plans` | — | No | Replaced by `execute-phase` (it needs `writing-plans`-format plans, git worktrees, and scripts from `subagent-driven-development`). |
| `writing-plans` / `brainstorming` | — | No | Superseded by `wayfinder` and `grill-me`. |
| Others (`subagent-driven-development`, `dispatching-parallel-agents`, `finishing-a-development-branch`, `using-git-worktrees`, `receiving-code-review`, `writing-skills`, `diagnosing-superpowers`, `using-superpowers`) | — | No | Reference only. |

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
   /skill:wrap-up
   ```

---

### Phase 2: Planning vs. Coding (The Traffic Light Rule)

Check `planning/<slug>/MAP.md` (or `AGENTS.md`) to see which mode to run:

- **🟡 Rough idea, not sure it's worth planning yet:** Run **`/skill:grill-me`** first.
- **🔴 Unchecked `[ ]` decisions block the next Phase:** Run **`/skill:wayfinder`**.
  ```text
  /skill:wayfinder Continue from AGENTS.md and planning/<slug>/MAP.md. Let's resolve the open decisions for the next phase one at a time.
  ```
- **🟢 Decisions for the current Phase are locked (`[x]` / `EMPTY` frontier):** Run **`/skill:execute-phase`**.
  ```text
  /skill:execute-phase Read AGENTS.md and planning/<slug>/MAP.md. Execute Phase X.
  ```
  `execute-phase` writes 🤖 tasks, co-writes 🤝 tasks, and coaches you on 🧑 tasks. To code a whole phase yourself instead:
  ```text
  /skill:pair-navigator Coach me step-by-step through implementing Phase X myself.
  ```
- **🐞 Something broke:** Run **`/skill:systematic-debugging`** (agent investigates) or **`/skill:pair-navigator`** (you investigate, AI coaches).

---

### Phase 3: End-of-Session Ritual (Every Session)

One command before closing your terminal:
```text
/skill:wrap-up
```
It verifies (tests/linters with real output), asks 0–3 ownership questions based on the diff size, writes the session note, logs your knowledge gaps, and updates `AGENTS.md`.

Before a code review, demo, or defense, also run the deep drill:
```text
/skill:rubber-duck-grill
```

---

### Phase 4: End-of-Phase Milestone (Delta Atlas Refresh)

Whenever a full Phase finishes (e.g., mock screens become live API screens):
```text
/skill:system-archaeologist Incremental refresh of docs/SYSTEM_ATLAS.md and docs/system-atlas.html based on recent docs/sessions/ notes and git diff. Update the Truth Matrix and study path.
```

---

### Weekly: Close Your Knowledge Gaps

Open `docs/learning/gaps.md`, pick 1–2 unchecked items, and study them on the real code:
```text
/skill:codebase-xray Explain <concept> using <file/function from the gap>. Then quiz me.
```
`wrap-up` ticks a gap `[x]` once you answer it correctly in a later session.

---

## ICM ("One Home Per Fact") Repository Convention

Every project using these skills keeps five non-overlapping homes for knowledge:

| Fact Type | Single Canonical Home | Rule |
| :--- | :--- | :--- |
| **Routing & Immediate Next Step** | `AGENTS.md` | Short (<40 lines) routing table + current branch/next step + test/lint commands. Never paste schemas or status tables here. |
| **System Architecture & Live/Mock State** | `docs/SYSTEM_ATLAS.md` & `docs/system-atlas.html` | Updated via `/skill:system-archaeologist`. |
| **Roadmap, Phase Status & Decisions** | `planning/<slug>-plan.md` or `planning/<slug>/MAP.md` & `decisions/*.md` | Written by `/skill:wayfinder`; ticked by `/skill:execute-phase` and `/skill:wrap-up` (overwrite in place, never append stale text). |
| **Session History & Gotchas** | `docs/sessions/YYYY-MM-DD-<slug>.md` | Written at the end of every session via `/skill:wrap-up`. |
| **My Knowledge Gaps** | `docs/learning/gaps.md` | One line per concept you got wrong or were unsure about, with a file pointer. Appended and ticked by `/skill:wrap-up`. |

---

## Installation & Symlink Setup

### Method 1: Local Clone + Flat Symlinks into Pi (Recommended)

Pi expects skills inside `~/.pi/agent/skills/<skill-name>/SKILL.md`. Cloning this repo to `~/agent-skills` and symlinking individual folders lets you edit skills locally and flatten cherry-picked `superpower/` skills:

```bash
# 1. Clone repo
git clone https://github.com/YajiHub/agent-skills.git ~/agent-skills
mkdir -p ~/.pi/agent/skills

# 2. Link the 11 top-level skills
for skill in wayfinder execute-phase wrap-up system-archaeologist codebase-xray pair-navigator rubber-duck-grill grill-me impeccable agent-browser caveman; do
  ln -sfn ~/agent-skills/$skill ~/.pi/agent/skills/$skill
done

# 3. Flatten and link the 4 Superpower quality skills
for sp_skill in systematic-debugging test-driven-development verification-before-completion requesting-code-review; do
  ln -sfn ~/agent-skills/superpower/$sp_skill ~/.pi/agent/skills/$sp_skill
done

# 4. Verify active links (every entry should point into ~/agent-skills)
ls -la ~/.pi/agent/skills
```
Run `/reload` inside Pi to activate immediately.

**Unlinking a skill** (keeps it in the repo): `rm ~/.pi/agent/skills/<skill-name>`. No trailing slash, or `rm` will act on the real folder the link points to.

### Method 2: Via `npx skills` CLI (Selective Install from GitHub)

```bash
# List all skills (including nested superpower/ skills)
npx skills add YajiHub/agent-skills --list --full-depth

# Install top-level custom skills globally for Pi
npx skills add YajiHub/agent-skills \
  -s wayfinder -s execute-phase -s wrap-up -s system-archaeologist \
  -s codebase-xray -s pair-navigator -s rubber-duck-grill \
  -s grill-me -s impeccable -s agent-browser -s caveman \
  -a pi -g

# Install cherry-picked Superpower skills from the superpower/ subpath
npx skills add YajiHub/agent-skills/superpower \
  -s systematic-debugging -s test-driven-development \
  -s verification-before-completion -s requesting-code-review \
  -a pi -g
```

---

## Authoring Rules for Skills in This Repo

1. **No hidden dependencies:** A custom skill must never say "call the X skill" unless X is in this repo and linked. Put the needed behavior in the skill itself.
2. **Stack-neutral:** Framework-specific layers and files (Django, Flutter, `ENDPOINTS.md`) appear only as labeled examples.
3. **Lock file = third-party only:** When you rewrite a vendored skill, remove its entry from `skills-lock.json` so `npx skills update` can't overwrite your version.
4. **Folder name = `name:` field** in the `SKILL.md` frontmatter (lowercase, hyphens).