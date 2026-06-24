# CV Generator

A structured pipeline that takes your CV and a job description, tailors your application through four expert reviewer lenses, generates a matching cover letter, and prepares you for every interview stage.

The skill prompts in this repo are encrypted with [git-crypt](https://github.com/AGWA/git-crypt). You need a key from the repo owner to unlock them.

**New here? Read [`docs/how-to-use.md`](docs/how-to-use.md) — it covers everything from setup to a full session, step by step.**

*Maintainers: see [`docs/DEPENDENCIES.md`](docs/DEPENDENCIES.md) for which files to update when something changes.*

---

## How it works

You bring a CV and a job description. Three runbooks (one per platform) orchestrate 19 skills across two parallel pipelines. Multiple users on the same machine each get their own isolated profile under `users/[name]/` — gitignored, never shared.

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
                                                           │
                                                   application tracker
                                              (archives CVs, JDs, cover letters
                                               + maintains application log)
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

## Pipeline — 19 skills

### Shared foundation
| # | Skill | Output |
|---|-------|--------|
| 01 | CV Ingestion | `users/[name]/cv-source.md` |
| 02 | JD Ingestion | `users/[name]/jd-[company]-[role].md` |
| 03 | Clarifying Questions | `users/[name]/clarifications.md` |
| 04 | Format & Style Coach | `users/[name]/format-spec.md` |

### CV pipeline
| # | Skill | Output |
|---|-------|--------|
| 05 | CV Generation | `users/[name]/versions/cv-v1.html` |
| 06 | Recruiter Review | `users/[name]/versions/cv-v2.html` |
| 07 | HR Review | `users/[name]/versions/cv-v3.html` |
| 08 | Hiring Manager Review | `users/[name]/versions/cv-v4.html` |
| 09 | Technical Peer Review | `users/[name]/versions/cv-v5.html` |

### Cover letter pipeline (parallel — runs independently)
| # | Skill | Output |
|---|-------|--------|
| 14 | Cover Letter Generation | `users/[name]/versions/cover-letter-v1.html` |
| 15 | Cover Letter Recruiter Review | `users/[name]/versions/cover-letter-v2.html` |
| 16 | Cover Letter HR Review | `users/[name]/versions/cover-letter-v3.html` |
| 17 | Cover Letter Hiring Manager Review | `users/[name]/versions/cover-letter-v4.html` |
| 18 | Cover Letter Technical Review | `users/[name]/versions/cover-letter-v5.html` |

### Interview prep (document-aware — uses CV and/or cover letter)
| # | Skill | Output |
|---|-------|--------|
| 10 | Interview Prep: Recruiter | `users/[name]/interview-prep/questions-recruiter.md` |
| 11 | Interview Prep: HR | `users/[name]/interview-prep/questions-hr.md` |
| 12 | Interview Prep: Hiring Manager | `users/[name]/interview-prep/questions-hiring-manager.md` |
| 13 | Interview Prep: Technical Peer | `users/[name]/interview-prep/questions-technical-peer.md` |

### Closing
| # | Skill | Output |
|---|-------|--------|
| 19 | Application Tracker | `users/[name]/applications/log.md` + per-application archive |

---

## Files in this project

All personal data lives under `users/[name]/` and is gitignored. The repo itself contains only encrypted skills, runbooks, and documentation.

| File / Folder | What it contains | Persists? |
|---|---|---|
| `users/[name]/cv-source.md` | Structured CV data | Yes — reused for every application |
| `users/[name]/jd-[company]-[role].md` | Extracted JD per application | Yes — one file per role |
| `users/[name]/clarifications.md` | Answers to pre-generation questions | Per session |
| `users/[name]/format-spec.md` | Agreed CV and cover letter format | Per session (reusable) |
| `users/[name]/versions/` | All CV and cover letter HTML versions | Yes — never overwritten |
| `users/[name]/findings/` | Reviewer persona observations, append-only | Yes — grow across sessions |
| `users/[name]/lessons-learned.md` | Cross-session lessons | Yes |
| `users/[name]/interview-prep/` | Questions and talking points per stage | Per session |
| `users/[name]/applications/` | Archive of submitted applications + log | Yes |

Nothing is sent externally. Everything stays in this folder.

---

## Notes

- The runbook detects the active user and your current pipeline state automatically at the start of every session.
- Multiple people can use the same repo on the same machine — each gets their own isolated `users/[name]/` folder.
- CV and cover letter pipelines are independent. You can generate only one, or both.
- Interview prep is document-aware — it incorporates whichever documents you have.
- Reviewer findings are append-only and persist across applications, making feedback sharper over time.
- Skill 19 (Application Tracker) archives each completed application and maintains a searchable log.
