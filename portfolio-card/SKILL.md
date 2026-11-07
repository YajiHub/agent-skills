---
name: portfolio-card
description: >-
  Run from my portfolio repo (yaji-dev). Read a project folder (read-only) and write a
  short, verified entry into data/projects.json plus private interview notes.
disable-model-invocation: true
---

# Portfolio Card

Usage: `/skill:portfolio-card <path to project> [slug]`

## Rules
- The project folder is READ-ONLY. Never write, commit, or run state-changing commands there.
- Only claim features that are live in code. Skip mock or unfinished ones, or label them in progress.
- Plain words, no hype (seamless, robust, cutting-edge, revolutionary, enterprise-grade).

## 1. Read the project
AGENTS.md, docs/SYSTEM_ATLAS.md, README.md and the newest docs/sessions note if they exist.
Otherwise read the entry points, routes and models.
If `data/projects.json` already has this slug, this is a refresh: start from the existing entry.

## 2. My contribution
Run `git -C <project> log --author="<my git name>" --name-only --oneline` (ask for my git
name once if unknown) and summarize which areas I touched. Then ask me ONE question:
"In one sentence, what did you personally build or own here?" Never guess my role in a team repo.

## 3. Draft the entry → data/projects.json
Follow this schema (keep all other entries untouched; preserve order). `app.js` renders every
field below; a missing display field breaks ALL cards, not just this one.
- slug · section (`projects` | `game-lab`) · title
- tagline (≤15 words) · role (≤12 words, from my answer)
- status (`live` | `in-progress` | `archived`) · stack (≤6, only what's really used)
- bullets: 2–3 `{ "title": "2–4 words", "text": "one concrete, checkable line" }`
- links { repo, demo } (null if private or none) · cover (path or null)
- Display fields (reuse the existing entry's values on a refresh):
  - accent: `emerald` | `sky` | `purple` | `rose` (pick one not used by the neighbour card)
  - badges: 1–3 `{ "text": "UPPERCASE LABEL", "tone": "<accent>-tint" | "amber-tint" | "glass" }`
  - icon, metaIcon: Material Symbols names (e.g. `inventory_2`, `point_of_sale`)
  - platform: footer tag, e.g. `Android & Desktop`

Validate afterwards and fix every problem it reports for this entry:
`node scripts/check-projects.mjs`

## 4. Private notes → private/notes/<slug>.md
First make sure `private/` is in .gitignore (add it if missing, and tell me).
Contents: each bullet → the files that prove it · claims you checked and dropped, and why ·
3 interview questions I'm likely to get about this project, with the file to re-read first.

## 5. Stop
Show me the entry and the notes. I rewrite the tagline and bullets in my own words.
Do not commit.
