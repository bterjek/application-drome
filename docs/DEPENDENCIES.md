# File Dependencies

This file tracks which documentation files depend on which, so that when one thing changes, you know everything else that needs updating too.

---

## Dependency map

```
README.md
├── links to → docs/how-to-use.md
├── links to → docs/usage-guide.md (via "see docs/usage-guide.md")
├── mirrors → Platform support table (costs, platform names, availability)
├── mirrors → Workflow steps table
└── mirrors → Files-in-this-project table

docs/how-to-use.md
├── mirrors → Platform support table (costs, platform names, availability)
├── mirrors → Decision matrix (platform names, costs, capabilities)
├── mirrors → Workflow steps (steps 01–12, what each does, output files)
├── references → GEMINI.md (mentions it as the router for Antigravity CLI)
├── references → .github/copilot-instructions.md (mentions it as router for Copilot)
├── references → platforms/gemini-cli/SETUP.md
└── references → platforms/github-copilot/SETUP.md

docs/usage-guide.md
└── references → README.md ("See README.md for setup...")

GEMINI.md
├── mirrors → Workflow steps table (skill file paths, what each step does)
└── references → .claude/skills/*/SKILL.md (all 12 paths)

.github/copilot-instructions.md
├── mirrors → Workflow steps table (skill file paths, what each step does)
└── references → .claude/skills/*/SKILL.md (all 12 paths)

platforms/gemini-cli/SETUP.md
└── references → GEMINI.md

platforms/github-copilot/SETUP.md
└── references → .github/copilot-instructions.md
```

---

## What to update when things change

### A platform is added or removed
Update all of these:
- `README.md` — Platform support table
- `docs/how-to-use.md` — Platform support summary, decision matrix (all four sub-tables + quick recommendations), Option A/B/C setup sections
- `platforms/` — Add or remove the relevant `SETUP.md`
- Add or remove the platform router file (`GEMINI.md`, `.github/copilot-instructions.md`, etc.)

### A platform's cost, tier, or version changes
Update:
- `README.md` — Platform support table
- `docs/how-to-use.md` — Tested versions table + decision matrix cost section + platform setup "What you need" section + quick recommendations
- `platforms/[platform]/SETUP.md` — Tier comparison table (if present)

### A skill is added, removed, or renamed
Update:
- `GEMINI.md` — Workflow steps table
- `.github/copilot-instructions.md` — Workflow steps table
- `README.md` — Workflow steps table
- `docs/how-to-use.md` — The pipeline section (Step 4)
- `docs/usage-guide.md` — If the edge case behaviour of that skill is documented

### A skill's output file changes
Update:
- `README.md` — Files-in-this-project table
- `docs/how-to-use.md` — Files-in-this-project section + relevant step description in Step 4
- `docs/usage-guide.md` — If that file is mentioned in edge cases

### The git-crypt version or setup process changes
Update:
- `docs/how-to-use.md` — Tested versions table + Step 2 (unlock instructions)
- `README.md` — Setup section
- `platforms/gemini-cli/SETUP.md` — Unlock section
- `platforms/github-copilot/SETUP.md` — Unlock section

### The `.gitattributes` encryption scope changes (e.g. new paths encrypted)
Update:
- `docs/how-to-use.md` — Troubleshooting section if behaviour changes
- `README.md` — No direct mention, but note if it affects the setup flow

---

## Platforms and their router files

| Platform | Router file | Setup guide |
|----------|------------|-------------|
| Claude Cowork | (none — skills auto-detected from `.claude/skills/`) | `docs/how-to-use.md` Option A |
| Antigravity CLI / Gemini CLI | `GEMINI.md` | `platforms/gemini-cli/SETUP.md` |
| GitHub Copilot (VS Code) | `.github/copilot-instructions.md` | `platforms/github-copilot/SETUP.md` |

---

## Last verified

June 2026. Update this date whenever you do a version audit.
