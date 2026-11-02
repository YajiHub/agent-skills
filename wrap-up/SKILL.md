---
name: wrap-up
description: >-
  One-command end of session: verify the work, a short ownership check on the diff,
  then write the session note, log my knowledge gaps, and update AGENTS.md / plan status.
disable-model-invocation: true
---

# Wrap-Up (ICM end of session)

One home per fact: status → AGENTS.md (+ active plan/MAP.md) · history → docs/sessions/ ·
my knowledge gaps → docs/learning/gaps.md · architecture → docs/SYSTEM_ATLAS.md.
Do the steps in order.

## 1. Verify (evidence, not claims)
- Run `git status` and `git diff --stat`.
- Run the project's test/lint/analyze commands (listed in AGENTS.md; otherwise detect them
  for the stack). Show the real output. If something fails, report it plainly. Do not
  fix it during wrap-up unless I ask.

## 2. Ownership check (scaled to the diff)
- Docs/no code changes: skip. Small diff: 1 question. Larger diff: 2–3 questions.
- Order: Data flow → What if it breaks → Why this layer. One at a time; wait; candid feedback.
- If I say "skip", skip it, but write "ownership check skipped" in the note.

## 3. Write docs/sessions/YYYY-MM-DD-<slug>.md
Sections: Focus · What Was Built / Changed · Verification (commands + pass/fail) ·
Mistakes & Gotchas · Decisions · Next Step (the exact first action next time).

## 4. Log knowledge gaps → docs/learning/gaps.md
For each thing I got wrong or was unsure about (step 2 or during the session), add one line:
`- [ ] <concept> — <file/function where it showed up> (YYYY-MM-DD)`.
If I answered an older gap correctly this session, tick it `[x]`.

## 5. Update routing
- AGENTS.md: replace the Current Status & Next Step block in place (create the file if
  missing: <40 lines, pointing to docs/SYSTEM_ATLAS.md, planning/, docs/sessions/,
  docs/learning/).
- Tick completed items in the active plan/MAP.md. Never leave old status lines behind.

## 6. Confirm in 3 lines: note path, gaps added, next step.