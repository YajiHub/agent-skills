---
name: execute-phase
description: >-
  Execute ONE phase of a wayfinder plan (planning/<slug>-plan.md or a MAP.md roadmap)
  task by task with tests and verification, respecting who-codes ownership tags.
disable-model-invocation: true
---

# Execute Phase

## 1. Load (read, don't scan)
- Read AGENTS.md and the plan file I name (or the Active Plan pointer in AGENTS.md).
- Pick the phase I name, else the first one not ✅. State its tasks, files, and checks.
- If the phase depends on an unresolved decision `[ ]`, stop and tell me to run wayfinder.
- Run `git status`. If on main/master or there are unrelated uncommitted changes, ask first
  (suggest a branch like `feat/<slug>-phase-N`).

## 2. Work each task in order, by its ownership tag
- 🤖 (agent): write a test that fails for the right reason (or state the manual check if
  it isn't testable) → run it, show the failure → make the smallest change → run it again
  and show the real output → tick the checkbox in the plan.
- 🤝 (together): write the signature/skeleton and the test; I write the body; you review.
- 🧑 (me): do NOT edit files. Give me Where / What & Why / a hint, wait for me to save,
  then review my code.
- Before running a test or command, ask me to predict the result in one line
  (skip if I say "no predictions").
- Stay inside the plan's file list. If you need another file, say why before touching it.

## 3. When something fails
Do not guess-fix. Reproduce → read the full error → trace to the root cause → state the
cause in one sentence → fix. After 2 failed fixes on the same problem, stop and report.

## 4. Stop at the phase boundary
- Run the full test suite / analyzer once and show the output.
- Update the phase status in the plan (✅, or 🟡 plus what's left). Overwrite in place.
- Summarize in ≤5 lines: files changed, what was verified, anything deferred.
- Propose a commit message, but do not commit, push, or start the next phase unless I ask.
  Suggest /skill:wrap-up.