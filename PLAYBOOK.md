# Playbook: What To Run, When

The README says what each skill is. This file says **which one to type in every situation**.

**Default when unsure:** `/skill:wayfinder what's next?`
It reads `AGENTS.md`, the plan, the last session note, and git, then tells you exactly which command to run next and stops.

---

## Quick Router

| Situation | Type this |
| :--- | :--- |
| Opened the project, forgot where I am | `/skill:wayfinder what's next?` |
| Brand-new idea, nothing built | `/skill:grill-me <idea>`, then `/skill:wayfinder <idea>` |
| Existing messy / vibe-coded repo, first time with this system | `/skill:system-archaeologist`, then `/skill:wayfinder what should we build first?` |
| Open `[ ]` decisions block the next phase | `/skill:wayfinder continue planning/<slug>/MAP.md` |
| Phase is unblocked, small (≤2 small tasks) | `/skill:execute-phase` |
| Phase is unblocked, bigger | `/skill:execute-phase next phase, use subagents` |
| I want to write the code myself | `/skill:pair-navigator coach me through Phase X` |
| Something is broken | `/skill:systematic-debugging <symptom>`, or `/skill:pair-navigator` to find it yourself |
| Tiny change (typo, label, color) | Just ask for it in plain words. No skill needed. |
| Done for today | `/skill:wrap-up` |
| Finished a whole phase / milestone | commit → `/skill:system-archaeologist incremental refresh` → `/skill:wrap-up` |
| Demo, code review, or defense coming | `/skill:rubber-duck-grill`, then `/skill:codebase-xray <key flow>` |
| Weekly study | open `docs/learning/gaps.md` → `/skill:codebase-xray <gap>` |

---

## Scenario Details

### 1. The lazy start ("what's next?")
**Type:** `/skill:wayfinder what's next?` (or just `/skill:wayfinder`)
**You get:** where you are, what was last done, loose ends, the next action, and the exact command.
**Then:** copy the command it gives you. It does not plan or code until you choose.
**Watch for:** if it reports drift (commits after the last session note, uncommitted changes), deal with that first (see 9 and 10).

### 2. Brand-new project or feature idea
1. `/skill:grill-me <rough idea>`. Answer until it summarizes Decided / Open / Risks.
2. `/skill:wayfinder <idea>`. It picks Compact (1–2 sessions) or Map mode (bigger).
3. `/skill:wrap-up`. This creates `AGENTS.md` if missing.

Skip grill-me if the idea is already clear.

### 3. Taking over an existing messy repo
1. `/skill:system-archaeologist`. Read the HTML atlas, especially the Truth Matrix and hotspots.
2. `/skill:wayfinder Read docs/SYSTEM_ATLAS.md and help me pick what to wire first.`
3. `/skill:wrap-up`.

Also create `docs/testing/QA-PROFILE.md` from `templates/QA-PROFILE.md` once, so qa-tester can run the app.

### 4. Resolving decisions (planning day)
`/skill:wayfinder continue planning/<slug>/MAP.md`. One decision at a time.
- Answer with an option, push back, or say "you decide". Delegated decisions get tagged `(by: delegated)`.
- Before your defense, review every `(by: delegated)` decision until you can explain it.

### 5. Building a phase yourself with one agent
`/skill:execute-phase Phase X` (or "next phase")
- 🤖 tasks: agent writes test → change → proof. You predict outcomes in one line.
- 🤝 tasks: agent writes the skeleton and test, you write the body.
- 🧑 tasks: you write it, the agent coaches and reviews.
- It stops at the end of the phase and proposes a commit message. **You** read the diff and commit.

### 6. Building a phase with subagents (orchestrator mode)
**Type:** `/skill:execute-phase next phase, use subagents`

You don't need to name models. They're set in each agent file, and typing them risks typos.

**Flow per 🤖 task:** orchestrator writes a brief → `expressive-dev` implements → `hygiene-reviewer` checks the diff and re-runs tests → max 2 fix rounds → orchestrator re-runs tests itself → ticks the plan.
**End of phase:** you predict one thing QA will find → `qa-tester` tests user flows → Critical/High fixed now, Medium/Low listed for you.
**🧑/🤝 tasks** are never sent to subagents. The orchestrator handles them with you.

**Edge cases:**
- Dev reports `BLOCKED`, or review fails twice → the orchestrator stops and shows both reports. Usually the plan is unclear, so go to scenario 8.
- QA reports `BLOCKED` (app not running) → start the servers yourself, or fill in QA-PROFILE.md, then ask: "re-run qa-tester".
- Two tasks touch the same file → they run one after another, not in parallel. That's intended.
- Small phase → the orchestrator suggests doing it inline. Accept, because subagents cost more on small work.

### 7. Coding it myself
`/skill:pair-navigator coach me through Phase X` (whole phase) or a single 🧑 task inside execute-phase.
Ask for "I'm stuck, show me the exact code" only after a real attempt.

### 8. The plan turns out wrong mid-build
execute-phase stops when the code contradicts a locked decision. **Don't let the agent improvise.**
1. `/skill:wayfinder the decision "<title>" is wrong because <what you found>. Re-open it.`
2. Resolve it, then `/skill:execute-phase continue Phase X`.

### 9. A session ended without wrap-up (crash, closed laptop, context full)
1. `/skill:wayfinder what's next?` It will flag uncommitted changes and unticked boxes.
2. If the work looks right: `/skill:wrap-up` now (it records the missing session).
3. If unsure whether the leftover code is right: ask "use the hygiene-reviewer subagent to review the uncommitted diff against Phase X of <plan>". Then either `/skill:execute-phase continue Phase X`, or `git stash` and redo the task.

The plan checkboxes plus git are your recovery record. That's why you tick them as you go.

### 10. A teammate pushed changes
`git pull` → `/skill:wayfinder what's next?`. It flags commits newer than your last session note.
If they changed a lot (new screens or endpoints): `/skill:system-archaeologist incremental refresh` before planning.

### 11. Bug found during a phase
- Caused by the current task → execute-phase's own failure rule handles it (root cause first, max 2 tries).
- Unrelated, small → finish the task, then `/skill:systematic-debugging <symptom>`.
- Unrelated, big or changes the design → note it, let wrap-up record it, plan it later with wayfinder.

### 12. Bug reported outside any plan
- Want to learn: `/skill:pair-navigator help me debug <symptom>`.
- Need it fixed: `/skill:systematic-debugging <symptom>`.
- Then `/skill:wrap-up`. If the fix reveals a design problem → `/skill:wayfinder`.

### 13. New idea mid-phase (scope creep)
Don't switch. Say "park this: <idea>". Wrap-up records it, and wayfinder later puts it in Fog of War or Out of Scope.

### 14. Tiny change
Ask directly ("change the button label to Save"). No skills. Run `/skill:wrap-up` at the end of the day as usual.

### 15. UI work inside a phase
Add `/skill:impeccable <audit|polish|...>` for design quality and `/skill:agent-browser` to check it visually, after the phase's logic is done.

### 16. Phase finished
1. Read the diff and commit.
2. If mock screens became live, or the architecture shifted: `/skill:system-archaeologist incremental refresh`.
3. `/skill:wrap-up`.

### 17. Before a demo, code review, or defense
1. `/skill:rubber-duck-grill` on the key modules.
2. `/skill:codebase-xray <the flows the panel will ask about>`.
3. Go through `(by: delegated)` decisions and open items in `docs/learning/gaps.md`.

### 18. Lazy / tired day
Fine: let 🤖 do more, and say "skip" to the ownership questions in wrap-up.
Not fine: skipping wrap-up itself. It's the only thing that makes tomorrow's "what's next?" work.
**Rule:** don't skip the ownership check two sessions in a row.

### 19. Weekly (15 minutes)
Open `docs/learning/gaps.md` → pick 1–2 unchecked items → `/skill:codebase-xray explain <gap> using <file>, then quiz me`.
Next session's wrap-up ticks a gap `[x]` once you get it right.

### 20. Switching between projects
Skills are global. Memory is per project (`AGENTS.md`, `planning/`, `docs/`). Just `cd` into the other project and run scenario 1.

---

## Growing out of vibe coding

Every few phases, check the ratio of 🧑 + 🤝 tasks to 🤖 tasks in your plans. Raise it on purpose: tell wayfinder "tag 3 tasks per phase as 🧑 this time".
