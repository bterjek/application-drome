# How to Use CV Generator — Complete Guide

This guide takes you from "I just got a link to this repo" to having a tailored CV and cover letter ready for a specific job. No assumptions about prior experience.

---

## Tested versions

This guide was last verified in **June 2026**.

| Component | Tested version | Notes |
|-----------|---------------|-------|
| git-crypt | 0.8.0 | Install via `brew install git-crypt` |
| Claude Desktop (Cowork) | Current — check [claude.ai/download](https://claude.ai/download) | Requires Pro plan ($20/mo). macOS 10.15+ or Windows 10 22H2+ |
| Antigravity CLI | 0.1.x+ | Google's replacement for Gemini CLI — see note below |
| Node.js (for Antigravity CLI) | 18 or later | Check with `node --version` |
| VS Code | 1.109+ (Jan 2026 release) | Earlier versions may not support agent mode fully |
| GitHub Copilot extension | Latest from VS Code Marketplace | Agent mode: Free (50 req/mo) or Pro ($10/mo) |

> **Gemini CLI → Antigravity CLI:** Google deprecated Gemini CLI on June 18, 2026 for personal Google accounts. The replacement is [Antigravity CLI](https://developers.googleblog.com/an-important-update-transitioning-gemini-cli-to-antigravity-cli/), which keeps the same file read/write capabilities and workflow. If you already have Gemini CLI installed and it still works for your account (e.g. via a Gemini Code Assist enterprise licence), the workflow is identical.

---

## What is this?

CV Generator is a project folder that turns an AI assistant into a structured application coach. It contains 19 encrypted skills — instructions that tell the AI how to:

1. Extract and structure your existing CV
2. Extract what a specific job description actually requires
3. Ask targeted questions before generating anything
4. Agree on the right format, length, and visual style for this application
5. Generate a tailored CV and cover letter — matched to the role, not generic
6. Refine both through four expert reviewer lenses
7. Prepare you for every stage of the interview process
8. Archive each completed application and maintain a searchable log

A **runbook** sits above all of this — it reads your project folder at the start of every session, works out where you are in the pipeline, and routes you to the right next step. You never have to remember what comes next.

**Multiple people can share the same repo on the same machine.** Each person gets their own isolated profile under `users/[name]/` — your CV, JDs, generated documents, and application history never mix with anyone else's.

---

## Before you start

You need two things from whoever shared this repo with you:

- **The repository** — a URL to clone, or the folder directly
- **The key file** — a file called `cv-generator.key`, sent separately (never in the repo)

---

## Step 1 — Get the repo onto your computer

```bash
git clone <repo-url> cv-generator
cd cv-generator
```

If you were given the folder directly, skip `git clone` and navigate to it.

---

## Step 2 — Unlock the skill files

The skills are encrypted. Install git-crypt and unlock:

```bash
brew install git-crypt
git-crypt unlock /path/to/cv-generator.key
```

If you don't have Homebrew:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

You only need to do this once per machine.

---

## Step 3 — Choose your AI platform and follow its setup

### Decision matrix

**1. How do you plan to use this?**

| | Claude Cowork | Antigravity CLI | Copilot (VS Code) |
|---|:---:|:---:|:---:|
| One-off — just need a CV for one application | ✓ Best | ✓ Good | ✓ Good |
| Recurring — multiple applications over time | ✓ Best | ✓ Best | ✓ Good |
| Developing — want to edit skills, build on this | ✗ Limited | ✓ Good | ✓ Best |

**2. What's your existing setup?**

| | Claude Cowork | Antigravity CLI | Copilot (VS Code) |
|---|:---:|:---:|:---:|
| Already use Claude / have a Claude account | ✓ Zero extra setup | — | — |
| Already use VS Code | — | — | ✓ Zero extra setup |
| Already use Google / have a Google account | — | ✓ Zero extra setup | — |
| Starting from scratch | ✓ Easiest | ✓ Easy | ~ Moderate |

**3. How comfortable are you with a terminal?**

| | Claude Cowork | Antigravity CLI | Copilot (VS Code) |
|---|:---:|:---:|:---:|
| Not at all — I prefer apps with a GUI | ✓ Best | ✗ Needs terminal | ~ A little terminal |
| Comfortable with basic commands | ✓ Good | ✓ Best | ✓ Good |
| Developer — I live in the terminal / IDE | ✓ Good | ✓ Best | ✓ Best |

**4. What matters most on cost?**

| | Claude Cowork | Antigravity CLI | Copilot (VS Code) |
|---|:---:|:---:|:---:|
| Free, no strings | ✗ Paid only ($20/mo) | ✓ Best (generous free tier) | ✓ Free (50 agent req/mo) |
| Happy to pay a small amount | ✓ Pro $20/mo | — | ✓ Pro $10/mo |
| Already paying for something | ✓ if you have Claude Pro | ✓ already free | ✓ if you have Copilot |

### Quick recommendation

**"I just want to try this once with minimum fuss"** → GitHub Copilot (VS Code) if you have it; Antigravity CLI if you're comfortable with a terminal.

**"I'll use this regularly"** → Claude Cowork (most conversational) or Antigravity CLI (fastest for experienced users).

**"I want to tweak the skills or build on this"** → GitHub Copilot in VS Code or Antigravity CLI.

**"I already pay for GitHub Copilot / use VS Code daily"** → GitHub Copilot in VS Code — zero incremental cost.

**"I don't want to touch a terminal"** → Claude Cowork — the only pure GUI option (requires paid Claude plan, $20/mo).

---

## Option A — Claude Cowork

### What you need
- The [Claude desktop app](https://claude.ai/download)
- A Claude **Pro, Max, Team, or Enterprise** subscription ($20/mo minimum — Cowork is not available on the free tier)
- macOS 10.15 (Catalina) or later, or Windows 10 22H2 or later

### Setup
1. Open the Claude desktop app
2. Switch to **Cowork mode**
3. Click **Open folder** and select your `cv-generator` folder
4. Claude reads `CLAUDE.md` automatically — the runbook is live, no further setup needed

### How it works
Just tell Claude what you want to do. The runbook handles the rest:

> "I want to start a new CV session."
> "I have a job description — let's go."
> "Where did I leave off?"

---

## Option B — Antigravity CLI

> If you have an existing Gemini CLI install that still works, substitute `gemini` for `antigravity` — the workflow is identical.

### What you need
- [Node.js](https://nodejs.org/) version 18 or later
- A Google account

### Setup

```bash
npm install -g @google/antigravity-cli
antigravity auth login
```

### How it works

```bash
cd path/to/cv-generator
antigravity
```

The CLI starts with `GEMINI.md` as its runbook. It reads the folder state and tells you where you are. To run a step explicitly:

> "Read `.claude/skills/01-cv-ingestion/SKILL.md` and follow the instructions."

See `GEMINI.md` in the project root for the full pipeline map. (The file is named GEMINI.md for compatibility but works identically with Antigravity CLI.)

---

## Option C — GitHub Copilot in VS Code

### What you need
- [VS Code](https://code.visualstudio.com/) version 1.109 or later (January 2026 release)
- A GitHub account
- GitHub Copilot: **Free tier** (50 agent-mode interactions/month) or **Pro** ($10/mo, unlimited)

### Setup

1. Open VS Code → Extensions (`Cmd+Shift+X`) → install **GitHub Copilot** → sign in
2. Open the project: `code path/to/cv-generator`
3. Open Copilot Chat (`Cmd+Alt+I`) → click the mode selector → choose **Agent**

`.github/copilot-instructions.md` loads automatically as the runbook.

### How it works

In the Agent mode chat panel, Copilot reads the folder state and routes you. To run a step explicitly:

> "Read `.claude/skills/01-cv-ingestion/SKILL.md` and follow the instructions."

Copilot proposes file changes as diffs — accept or reject each one individually.

---

## Step 4 — Run a session

Once your platform is set up, the runbook does the navigation. Here is what each skill does.

### First time? The runbook will ask your name

The first thing the runbook does is check the `users/` folder. If it's empty, it asks for your name and creates `users/[yourname]/`. If someone else has already used the tool on this machine, it will list the existing profiles and ask who you are. From there, all your files are stored under your own folder.

### What to have ready
- Your current CV (text, Word doc, or PDF you can copy from)
- The job description you are applying to (full text from the job posting)

---

### Shared foundation (runs once per application)

**Skill 01 — CV Ingestion**
Extracts your CV into `cv-source.md`. This is your persistent profile — reused for every future application without re-uploading.

**Skill 02 — JD Ingestion**
You paste the job description. The AI extracts what the role actually requires — beyond the surface keywords — into a structured file.

**Skill 03 — Clarifying Questions**
Up to 5 targeted questions about narrative, framing, and gaps between your CV and the JD. Your answers go into `clarifications.md`.

**Skill 04 — Format & Style Coach**
A recruitment coach recommends length, layout, density, visual style, and template based on the company, country, market segment, and role customs. Saves the agreed specification to `format-spec.md`, which all generation skills use as their design brief.

---

### CV pipeline

**Skill 05 — CV Generation**
Generates `versions/cv-v1.html` — a tailored CV following the format spec exactly. Open in a browser to see it.

**Skill 06 — Recruiter Review → v2**
Recruiter persona: ATS compatibility, first impression, red flags, clarity. Produces `cv-v2.html`.

**Skill 07 — HR Review → v3**
HR persona: culture fit, values alignment, career narrative. Produces `cv-v3.html`.

**Skill 08 — Hiring Manager Review → v4**
Hiring manager persona: evidence of impact, autonomy, direct relevance to the role. Produces `cv-v4.html`.

**Skill 09 — Technical Peer Review → v5**
Technical peer persona: domain depth, credibility of claims, currency. Produces `cv-v5.html` — the final CV.

---

### Cover letter pipeline (parallel — can run independently)

**Skill 14 — Cover Letter Generation**
Generates `versions/cover-letter-v1.html`. Can run with or without a CV. Visually matched to the CV via the format spec.

**Skills 15–18 — Cover Letter Reviews → v2–v5**
Same four reviewer personas as the CV pipeline, each producing an improved version. Cover letter v5 is the final version.

---

### Interview prep (run after you have a final CV and/or cover letter)

Each prep skill checks which documents exist and asks whether to use both or CV only.

**Skill 10 — Recruiter screen prep** → `interview-prep/questions-recruiter.md`
**Skill 11 — HR interview prep** → `interview-prep/questions-hr.md`
**Skill 12 — Hiring manager prep** → `interview-prep/questions-hiring-manager.md`
**Skill 13 — Technical interview prep** → `interview-prep/questions-technical-peer.md`

Each produces 8–10 likely questions with suggested talking points and coaching on what to avoid.

---

### Application Tracker (closing step)

**Skill 19 — Application Tracker**
Runs at the end of any session where you have a final CV or cover letter. Copies the JD, final CV, and cover letter into `users/[name]/applications/[company]-[role]-[date]/`, creates a `notes.md` for outcome tracking, and appends a row to `users/[name]/applications/log.md`.

You can also run it standalone to update the status of a previous application (screening, interview, offer, rejected, withdrawn).

---

## Returning to a session

The runbook detects your state automatically. Just open your AI platform with this folder and tell it:

> "Where am I?" or "Continue where we left off."

It will read the files present and tell you exactly what has been done and what comes next.

---

## Re-entry options

- **New JD, same CV** — skip skill 01. Start at skill 02 with the new JD.
- **Cover letter only** — branch directly to skill 14. No CV required.
- **Interview prep only** — run skills 10–13. The runbook will check which documents exist.
- **Redo a review step** — jump to that skill directly. A new version is created; nothing is overwritten.
- **Update an application status** — run skill 19 standalone and choose an existing entry from the log.

---

## Troubleshooting

**Skill files look like garbled text / binary**
You have not unlocked the repo. Run `git-crypt unlock /path/to/cv-generator.key`.

**The AI says it cannot find a file**
Check that the file exists. If `cv-source.md` is missing, run skill 01. If `format-spec.md` is missing, run skill 04 before attempting generation.

**The generated CV looks generic**
The clarifying questions in skill 03 and the format spec in skill 04 are the most important inputs. Re-run both with more detail, then regenerate from skill 05.

**I want to start completely fresh**
Delete everything inside `users/[yourname]/` except `findings/` (which you may want to keep — it contains accumulated reviewer knowledge). Or delete the whole `users/[yourname]/` folder for a total reset.

**Someone else wants to use this on my machine**
Nothing to configure — just open the tool and when asked "Who are you?", enter a different name. A new profile is created automatically.

---

## Files after a full session

```
cv-generator/
└── users/
    └── yourname/
        ├── cv-source.md                      ← your CV in structured form
        ├── jd-acme-engineer.md               ← extracted job description
        ├── clarifications.md                 ← your answers to pre-generation questions
        ├── format-spec.md                    ← agreed format for CV and cover letter
        ├── versions/
        │   ├── cv-v1.html → cv-v5.html       ← CV drafts (v5 = final)
        │   └── cover-letter-v1.html → v5     ← cover letter drafts (v5 = final)
        ├── findings/
        │   ├── recruiter.md                  ← reviewer notes (grow across sessions)
        │   ├── hr.md
        │   ├── hiring-manager.md
        │   └── technical-peer.md
        ├── lessons-learned.md
        ├── interview-prep/
        │   ├── questions-recruiter.md
        │   ├── questions-hr.md
        │   ├── questions-hiring-manager.md
        │   └── questions-technical-peer.md
        └── applications/
            ├── log.md                        ← master application table
            └── acme-engineer-2026-06-24/
                ├── jd.md
                ├── cv-final.html
                ├── cover-letter-final.html
                └── notes.md
```

Everything stays on your machine. Nothing is sent anywhere. The entire `users/` folder is gitignored.
