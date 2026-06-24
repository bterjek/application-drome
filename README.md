# CV Generator

A structured pipeline that takes your CV and a job description, tailors your application through four expert reviewer lenses, generates a matching cover letter, and prepares you for every interview stage.

The skill prompts in this repo are encrypted with [git-crypt](https://github.com/AGWA/git-crypt). You need a key from the repo owner to unlock them.

**New here? Read [`docs/how-to-use.md`](docs/how-to-use.md) — it covers everything from setup to a full session, step by step.**

*Maintainers: see [`docs/DEPENDENCIES.md`](docs/DEPENDENCIES.md) for which files to update when something changes.*

---

## How it works

You bring a CV and a job description. Three runbooks (one per platform) orchestrate 18 skills across two parallel pipelines:

```
Your CV ──► extract ──► JD ──► extract ──► clarifying questions ──► format & style
                                                                           │
                                              ┌────────────────────────────┤
                                              │                            │
                                         CV pipeline               Cover letter pipeline
                                              │                            │
                                    generate cv-v1              generate cl-v1
                                    recruiter → v2              recruiter → v2
                                    HR → v3                     HR → v3
                                    hiring mgr → v4             hiring mgr → v4
                                    technical → v5              technical → v5
                                              │                            │
                                              └────────────┬───────────────┘
                                                           │
                                                   interview prep
                                              (document-aware: uses
                                               CV and/or cover letter)
```

Each reviewer persona accumulates findings across sessions — the more you use it, the sharper the feedback gets.

---

## Platform support

This project runs on any AI tool with native read/write access to your local filesystem. Each platform gets its own runbook that orchestrates the full pipeline.

| Platform | Runbook | Cost | Setup guide |
|----------|---------|------|-------------|
| **Claude Cowork** | `CLAUDE.md` (auto-loaded) | Pro plan required ($20/mo) | `docs/how-to-use.md` Option A |
| **Antigravity CLI** *(replaces Gemini CLI)* | `GEMINI.md` | Free (generous limits) | `platforms/gemini-cli/SETUP.md` |
| **GitHub Copilot in VS Code** | `.github/copilot-instructions.md` | Free (50 agent req/mo) / Pro $10/mo | `platforms/github-copilot/SETUP.md` |

> **Gemini CLI users:** Google deprecated Gemini CLI for personal accounts on June 18, 2026 in favour of [Antigravity CLI](https://developers.googleblog.com/an-important-update-transitioning-gemini-cli-to-antigravity-cli/). The workflow is identical — substitute `antigravity` for `gemini`. The `GEMINI.md` runbook works with both.

Platforms that do **not** support this workflow: ChatGPT (no local filesystem access without MCP setup), Microsoft Copilot web (upload only, no write).

---

## Setup

### 1. Install git-crypt and unlock

```bash
brew install git-crypt
git-crypt unlock /path/to/cv-generator.key
```

You need `cv-generator.key` from the repo owner.

### 2. Choose your platform and follow its setup guide

- **Claude Cowork** — open this folder in Cowork. `CLAUDE.md` loads automatically.
- **Antigravity CLI** — see `platforms/gemini-cli/SETUP.md`
- **GitHub Copilot (VS Code)** — see `platforms/github-copilot/SETUP.md`

---

## Pipeline — 18 skills

### Shared foundation
| # | Skill | Output |
|---|-------|--------|
| 01 | CV Ingestion | `cv-source.md` |
| 02 | JD Ingestion | `jd-[company]-[role].md` |
| 03 | Clarifying Questions | `clarifications.md` |
| 04 | Format & Style Coach | `format-spec.md` |

### CV pipeline
| # | Skill | Output |
|---|-------|--------|
| 05 | CV Generation | `versions/cv-v1.html` |
| 06 | Recruiter Review | `versions/cv-v2.html` |
| 07 | HR Review | `versions/cv-v3.html` |
| 08 | Hiring Manager Review | `versions/cv-v4.html` |
| 09 | Technical Peer Review | `versions/cv-v5.html` |

### Cover letter pipeline (parallel — runs independently)
| # | Skill | Output |
|---|-------|--------|
| 14 | Cover Letter Generation | `versions/cover-letter-v1.html` |
| 15 | Cover Letter Recruiter Review | `versions/cover-letter-v2.html` |
| 16 | Cover Letter HR Review | `versions/cover-letter-v3.html` |
| 17 | Cover Letter Hiring Manager Review | `versions/cover-letter-v4.html` |
| 18 | Cover Letter Technical Review | `versions/cover-letter-v5.html` |

### Interview prep (document-aware — uses CV and/or cover letter)
| # | Skill | Output |
|---|-------|--------|
| 10 | Interview Prep: Recruiter | `interview-prep/questions-recruiter.md` |
| 11 | Interview Prep: HR | `interview-prep/questions-hr.md` |
| 12 | Interview Prep: Hiring Manager | `interview-prep/questions-hiring-manager.md` |
| 13 | Interview Prep: Technical Peer | `interview-prep/questions-technical-peer.md` |

---

## Files in this project

| File / Folder | What it contains | Persists? |
|---|---|---|
| `cv-source.md` | Your structured CV data | Yes — reused for every application |
| `jd-[company]-[role].md` | Extracted JD per application | Yes — one file per role |
| `clarifications.md` | Your answers to pre-generation questions | Per session |
| `format-spec.md` | Agreed CV and cover letter format | Per session (reusable) |
| `versions/` | All CV and cover letter versions, never overwritten | Yes |
| `findings/recruiter.md` | Recruiter persona observations, append-only | Yes |
| `findings/hr.md` | HR persona observations, append-only | Yes |
| `findings/hiring-manager.md` | Hiring manager observations, append-only | Yes |
| `findings/technical-peer.md` | Technical peer observations, append-only | Yes |
| `lessons-learned.md` | Cross-session lessons from all personas | Yes |
| `interview-prep/` | Questions and talking points per interview stage | Per session |

Nothing is sent externally. Everything stays in this folder.

---

## Notes

- The runbook (CLAUDE.md / GEMINI.md / copilot-instructions.md) detects your current state automatically and routes you to the right next step.
- You can re-enter the pipeline at any point — the runbook handles branching.
- CV and cover letter pipelines are independent. You can generate only one, or both.
- Interview prep is document-aware — it incorporates whichever documents you have.
- Reviewer findings are append-only and persist across applications, making feedback sharper over time.
