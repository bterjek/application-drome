# File Dependencies

This file tracks which documentation files depend on which, so that when one thing changes, you know everything else that needs updating too.

---

## Dependency map

```
README.md
├── links to → docs/how-to-use.md
├── links to → docs/DEPENDENCIES.md
├── mirrors → Platform support table (costs, platform names, runbook files)
├── mirrors → Pipeline / skills table (all 18 skills)
└── mirrors → Files-in-this-project table

CLAUDE.md
├── IS the runbook for Claude Cowork
├── mirrors → Pipeline tables (all 18 skills, file paths)
├── mirrors → State detection logic
└── references → .claude/skills/*/SKILL.md (all 18 paths)

GEMINI.md
├── IS the runbook for Antigravity CLI / Gemini CLI
├── mirrors → Pipeline tables (all 18 skills, file paths)
├── mirrors → State detection logic
└── references → .claude/skills/*/SKILL.md (all 18 paths)

.github/copilot-instructions.md
├── IS the runbook for GitHub Copilot (VS Code agent mode)
├── mirrors → Pipeline tables (all 18 skills, file paths)
├── mirrors → State detection logic
└── references → .claude/skills/*/SKILL.md (all 18 paths)

docs/how-to-use.md
├── mirrors → Platform support table (costs, platform names, availability)
├── mirrors → Decision matrix (platform names, costs, capabilities)
├── mirrors → Pipeline / skills (steps 01–18, what each does, output files)
├── references → CLAUDE.md
├── references → GEMINI.md
├── references → .github/copilot-instructions.md
├── references → platforms/gemini-cli/SETUP.md
└── references → platforms/github-copilot/SETUP.md

docs/usage-guide.md
└── references → README.md ("See README.md for setup...")

platforms/gemini-cli/SETUP.md
└── references → GEMINI.md

platforms/github-copilot/SETUP.md
└── references → .github/copilot-instructions.md
```

---

## What to update when things change

### A platform is added or removed
- `README.md` — Platform support table
- `docs/how-to-use.md` — Platform summary, decision matrix (all four sub-tables + quick recommendations), setup sections
- Add or remove platform runbook (`CLAUDE.md`, `GEMINI.md`, `.github/copilot-instructions.md`)
- Add or remove `platforms/[platform]/SETUP.md`

### A platform's cost, tier, or version changes
- `README.md` — Platform support table
- `docs/how-to-use.md` — Tested versions table + decision matrix cost section + platform setup "What you need" + quick recommendations
- `platforms/[platform]/SETUP.md` — Tier comparison table if present

### A skill is added, removed, or renamed
- `CLAUDE.md` — Pipeline tables
- `GEMINI.md` — Pipeline tables
- `.github/copilot-instructions.md` — Pipeline tables
- `README.md` — Pipeline / skills table
- `docs/how-to-use.md` — Pipeline section (Step 4)
- `docs/usage-guide.md` — If that skill's edge case behaviour is documented

### The user isolation model changes (e.g. `users/` path prefix changes)
- `CLAUDE.md` — Step 0 user detection + all file paths in pipeline tables + state detection
- `GEMINI.md` — Step 0 user detection + all file paths
- `.github/copilot-instructions.md` — Step 0 user detection + all file paths
- `README.md` — Files-in-this-project table
- `docs/how-to-use.md` — "What is this?" section + Step 4 intro + Files section
- `.gitignore` — `users/` entry

### A skill's output file changes
- `README.md` — Files-in-this-project table
- `docs/how-to-use.md` — Files section + relevant step description
- `CLAUDE.md`, `GEMINI.md`, `.github/copilot-instructions.md` — Pipeline tables

### The state detection logic changes (e.g. new pipeline branch added)
- `CLAUDE.md` — State detection table
- `GEMINI.md` — State detection table
- `.github/copilot-instructions.md` — State detection table

### The git-crypt version or setup process changes
- `docs/how-to-use.md` — Tested versions table + Step 2 (unlock instructions)
- `README.md` — Setup section
- `platforms/gemini-cli/SETUP.md` — Unlock section
- `platforms/github-copilot/SETUP.md` — Unlock section

### The .gitattributes encryption scope changes
- `docs/how-to-use.md` — Troubleshooting section if behaviour changes

---

## Platforms and their runbooks

| Platform | Runbook | Setup guide |
|----------|---------|-------------|
| Claude Cowork | `CLAUDE.md` (auto-loaded) | `docs/how-to-use.md` Option A |
| Antigravity CLI / Gemini CLI | `GEMINI.md` | `platforms/gemini-cli/SETUP.md` |
| GitHub Copilot (VS Code) | `.github/copilot-instructions.md` | `platforms/github-copilot/SETUP.md` |

---

## Skill directory structure

```
.claude/skills/
├── 01-cv-ingestion/
├── 02-jd-ingestion/
├── 03-clarifying-questions/
├── 04-format-style-coach/         ← NEW: produces format-spec.md
├── 05-cv-generation/
├── 06-recruiter-review/
├── 07-hr-review/
├── 08-hiring-manager-review/
├── 09-technical-review/
├── 10-interview-prep-recruiter/   ← document-aware (CV + cover letter)
├── 11-interview-prep-hr/
├── 12-interview-prep-hiring-manager/
├── 13-interview-prep-technical/
├── 14-cover-letter-generation/    ← parallel pipeline starts here
├── 15-cover-letter-recruiter-review/
├── 16-cover-letter-hr-review/
├── 17-cover-letter-hiring-manager-review/
├── 18-cover-letter-technical-review/
└── 19-application-tracker/        ← closing step; archives CVs/JDs/cover letters + maintains log
```

All SKILL.md files are encrypted via `.gitattributes` using the pattern `.claude/skills/**/*.md`.

---

## Last verified

June 2026. Update this date whenever you do a version audit.
