# Agent Skills Library

Personal collection of reusable, standalone workflows and domain skills for **Pi** (`@mariozechner/pi-coding-agent`) and compatible AI coding agents.

## Repository Structure

Each skill lives in its own isolated directory containing a `SKILL.md` entrypoint and optional `references/`, `scripts/`, or `assets/` subdirectories:

```text
agent-skills/
├── README.md
├── wayfinder/
│   └── SKILL.md
└── <future-skill>/
    ├── SKILL.md
    └── references/
```

---

## Available Skills

| Skill | Invocation | Auto-Load | Description |
| :--- | :--- | :--- | :--- |
| **`wayfinder`** | `/skill:wayfinder` | Disabled (`disable-model-invocation: true`) | Adaptive planning and decision-mapping for small features (Compact Mode) and multi-session epics (Map Mode / Fog of War) with zero external skill dependencies. |

---

## Installing Specific Skills into Pi (Global)

Do not link the root of this repository if you only want specific skills active. Use one of the selective methods below:

### Option A: Via `npx skills` CLI (From GitHub)

```bash
# List all skills in this repository
npx skills add <your-github-username>/agent-skills --list

# Install a single skill globally for Pi
npx skills add <your-github-username>/agent-skills --skill wayfinder -a pi -g

# Install a single skill into the current project only (.pi/skills/)
npx skills add <your-github-username>/agent-skills --skill wayfinder -a pi

# Update or remove a skill
npx skills update wayfinder -g
npx skills remove wayfinder -g
```

### Option B: Via Per-Skill Symlinks / Junctions (Local Repo Clone)

Assuming this repo is cloned to `~/agent-skills`:

**Windows (PowerShell):**
```powershell
New-Item -ItemType Directory -Force -Path "$HOME\.pi\agent\skills"

# Enable a specific skill
New-Item -ItemType Junction -Path "$HOME\.pi\agent\skills\wayfinder" -Target "$HOME\agent-skills\wayfinder"

# Disable a specific skill
Remove-Item "$HOME\.pi\agent\skills\wayfinder"
```

**macOS / Linux / Git Bash:**
```bash
mkdir -p ~/.pi/agent/skills

# Enable a specific skill
ln -s ~/agent-skills/wayfinder ~/.pi/agent/skills/wayfinder

# Disable a specific skill
rm ~/.pi/agent/skills/wayfinder
```

### Option C: Via `~/.pi/agent/settings.json`

Add the exact path of the skill subfolder you want enabled to `~/.pi/agent/settings.json`, then run `/reload` in Pi:

```json
{
  "$schema": "[https://pi.dev/schemas/settings.schema.json](https://pi.dev/schemas/settings.schema.json)",
  "skills": [
    "~/agent-skills/wayfinder"
  ]
}
```

---

## Authoring Conventions for New Skills

1. **Folder & Name Match:** The directory name (`<skill-name>/`) should match the `name:` field in `SKILL.md` frontmatter (lowercase letters, numbers, and hyphens).
2. **Frontmatter Format:**
   ```yaml
   ---
   name: my-skill-name
   description: >-
     Clear description of what the skill does and when to trigger it.
   disable-model-invocation: true # Set to true for manual slash-command workflows (/skill:name)
   ---
   ```
3. **Self-Contained Logic:** Skills in this repo must not depend on external third-party skills unless explicitly documented. Keep heavy reference docs in a `references/` subfolder so they are only read on demand.