# CV Generator

A structured pipeline for tailoring your CV to any job description, refining it through four expert reviewer lenses, and preparing for every interview stage.

The skill prompts in this repo are encrypted with [git-crypt](https://github.com/AGWA/git-crypt). You need a key from the repo owner to unlock them.

**New here? Read [`docs/how-to-use.md`](docs/how-to-use.md) — it covers everything from setup to a full session, step by step.**

*Maintainers: see [`docs/DEPENDENCIES.md`](docs/DEPENDENCIES.md) for which files to update when something changes.*

---

## How it works

You bring a CV and a job description. The pipeline does the rest:

```
Your CV → extract → JD → extract → clarifying questions
        → generate v1 → recruiter review → v2
                      → HR review → v3
                      → hiring manager review → v4
                      → technical peer review → v5 (final)
                      → interview prep per persona
```

Each reviewer persona leaves behind a findings file that persists across sessions — the more you use the project, the sharper the feedback gets.

---

## Platform support

This project runs on any AI tool that has **native read/write access to your local filesystem**. Three platforms support this out of the box:

| Platform | File access | Cost | Package |
|----------|------------|------|---------|
| **Claude Cowork** | Native | Pro plan required ($20/mo) | Built-in — `.claude/skills/` |
| **Antigravity CLI** *(replaces Gemini CLI)* | Native | Free (generous limits) | `GEMINI.md` — see `platforms/gemini-cli/SETUP.md` |
| **GitHub Copilot in VS Code** | Native (agent mode) | Free (50 agent req/mo) / Pro $10/mo | `.github/copilot-instructions.md` — see `platforms/github-copilot/SETUP.md` |

> **Gemini CLI users:** Google deprecated Gemini CLI for personal accounts on June 18, 2026 in favour of [Antigravity CLI](https://developers.googleblog.com/an-important-update-transitioning-gemini-cli-to-antigravity-cli/). The workflow is identical — substitute `antigravity` for `gemini`. The `GEMINI.md` router file works with both.

Platforms that do **not** support this workflow: ChatGPT (no local filesystem access without MCP setup), Microsoft Copilot web (upload only, no write), Perplexity web.

---

## Setup

### 1. Install git-crypt and unlock

```bash
brew install git-crypt
git-crypt unlock /path/to/cv-generator.key
```

You need `cv-generator.key` from the repo owner. Send them your request — they'll share it securely.

### 2. Choose your platform and follow its setup guide

- **Claude Cowork** — open this folder in Cowork. Skills load automatically.
- **Gemini CLI** — see `platforms/gemini-cli/SETUP.md`
- **GitHub Copilot (VS Code)** — see `platforms/github-copilot/SETUP.md`

---

## Workflow steps

All platforms use the same 12 skill files. How you invoke them differs by platform — see the platform-specific guide or router file (`GEMINI.md` / `.github/copilot-instructions.md`).

| Step | What it does | Output |
|------|-------------|--------|
| 01 — cv-ingestion | Extract your CV into structured markdown | `cv-source.md` |
| 02 — jd-ingestion | Extract JD signals and requirements | `jd-[company]-[role].md` |
| 03 — clarifying-questions | Ask targeted questions to capture your narrative | `clarifications.md` |
| 04 — cv-generation | Generate a tailored HTML CV | `versions/cv-v1.html` |
| 05 — recruiter-review | Recruiter lens — ATS, clarity, first impression | `versions/cv-v2.html` |
| 06 — hr-review | HR lens — culture fit, values, career narrative | `versions/cv-v3.html` |
| 07 — hiring-manager-review | Hiring manager lens — outcomes, impact, credibility | `versions/cv-v4.html` |
| 08 — technical-review | Technical peer lens — depth, domain credibility | `versions/cv-v5.html` |
| 09 — interview-prep-recruiter | Questions + talking points for recruiter screen | `interview-prep/questions-recruiter.md` |
| 10 — interview-prep-hr | Questions + talking points for HR interview | `interview-prep/questions-hr.md` |
| 11 — interview-prep-hiring-manager | Questions + talking points for hiring manager | `interview-prep/questions-hiring-manager.md` |
| 12 — interview-prep-technical | Questions + talking points for technical interview | `interview-prep/questions-technical-peer.md` |

---

## Starting points

**New application** — run steps 1–8 in order. Steps 9–12 are optional interview prep once you have a final CV.

**Returning user, new JD** — skip step 1. Your `cv-source.md` is already there. Start at step 2.

**Interview prep only** — skip steps 1–8. Run steps 9–12 after confirming a final CV exists in `versions/`.

---

## Files in this project

| File / Folder | What it contains | Persists? |
|---|---|---|
| `cv-source.md` | Your structured CV data | Yes — reused for every application |
| `jd-[company]-[role].md` | Extracted JD per application | Yes — one file per role |
| `clarifications.md` | Your answers to pre-generation questions | Per session |
| `versions/` | All CV versions (v1–v5), never overwritten | Yes |
| `findings/recruiter.md` | Recruiter observations, append-only | Yes — grows over time |
| `findings/hr.md` | HR observations, append-only | Yes |
| `findings/hiring-manager.md` | Hiring manager observations, append-only | Yes |
| `findings/technical-peer.md` | Technical peer observations, append-only | Yes |
| `lessons-learned.md` | Cross-session lessons from all personas | Yes |
| `interview-prep/` | Questions and talking points per interview stage | Per session |

Nothing is sent externally. Everything stays in this folder.

---

## Notes

- CV versions are never overwritten. v1 through v5 are always available for comparison.
- Reviewer findings are append-only — past observations from previous applications inform the next session automatically.
- If you apply to the same company twice, step 02 will detect the existing JD file and ask whether to update it or create a new dated version.
- You can skip any reviewer step. They are independent — v3 does not require v2 to exist first.
