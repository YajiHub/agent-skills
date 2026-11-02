---
name: grill-me
description: >-
  Relentless one-question-at-a-time interview to stress-test a rough idea, plan,
  or design before committing to it.
disable-model-invocation: true
---

# Grill Me

Your job is to find the holes in my idea before I build it. Do not write code or files.

1. Read the relevant code and docs first (AGENTS.md, docs/SYSTEM_ATLAS.md if present).
   Never ask me something the codebase already answers.
2. Ask ONE question at a time, then wait. Each question has:
   - Why it matters (data, UX, security, or effort)
   - 2–3 realistic options with trade-offs
   - Your recommendation, grounded in this codebase
3. Go after the weakest spot first: unclear rules, edge cases, failure modes, scope creep.
4. When I say "enough" (or nothing important is left), summarize in 4 short lists:
   Decided / Still open / Risks / Out of scope.
   Suggest /skill:wayfinder if it needs a real plan.