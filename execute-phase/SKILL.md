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

## 5. Orchestrated Mode (only when I ask for subagents)

You become the **orchestrator**: subagents write the code for 🤖 tasks; you brief, check,
and keep the plan up to date. Sections 1–4 still apply. Each subagent's model is set in its
own agent file, so never pass or guess model names.

| Subagent | Use it for |
| :--- | :--- |
| `Explore` | Locating code when the plan's file list is not enough. |
| `expressive-dev` | Implementing ONE 🤖 task. |
| `hygiene-reviewer` | Reviewing the diff of each finished task. |
| `qa-tester` | Testing user-facing flows once per phase. |

### Per 🤖 task
1. **Write a task brief (≤20 lines).** Subagents start with no memory, so the brief is
   their whole context: task text from the plan · files allowed to change · locked
   decisions that apply (link + 1-line gist) · test/verify command · done criteria ·
   out of scope.
2. Dispatch `expressive-dev` with the brief. One task per dispatch.
3. Dispatch `hygiene-reviewer` with the same brief + "review the uncommitted diff for this task".
4. `CHANGES_REQUESTED` → send only the blocking defects back to `expressive-dev`.
   Still blocked after 2 rounds, or dev reports `BLOCKED` → stop and show me both reports.
5. `APPROVED` → re-run the task's test command yourself and show the output (reports are
   claims, not proof), then tick the checkbox in the plan.

- Run devs in parallel only when their tasks touch completely separate files.
  Otherwise, one at a time.
- 🧑 and 🤝 tasks are never delegated. Handle them with me directly, as in section 2.

### At the end of the phase
1. If the phase changed something a user can do (a screen, endpoint, role, or permission):
   ask me to predict one thing QA will find, then dispatch `qa-tester` with the phase
   scope, how to run the app (AGENTS.md / QA-PROFILE.md), roles to use, and the flows to
   test. For pure refactors or docs, skip QA and say that you skipped it.
2. Confirmed QA defects: Critical/High → fix now with the same dev → review loop.
   Medium/Low → list them for me to decide.
3. Report: each task with reviewer verdict · QA summary table · deferred items ·
   proposed commit message. Keep the devs' "Gotchas" and the QA defects in that report
   so `/skill:wrap-up` can record them.

### When not to use subagents
If the phase is ≤2 small 🤖 tasks, tell me subagents will probably cost more than they
save and offer to do it inline instead.
