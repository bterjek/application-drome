# How to Use CV Generator — Complete Guide

This guide takes you from "I just got a link to this repo" to having a tailored CV ready for a specific job. No assumptions about prior experience.

---

## What is this?

CV Generator is a project folder that turns an AI assistant into a structured CV coach. It contains a set of instructions (called skills) that tell the AI exactly how to:

1. Read your existing CV and understand it deeply
2. Read a job description and extract what the employer actually wants
3. Ask you the right questions before writing anything
4. Write a tailored CV — not a generic rewrite, a version genuinely shaped for that role
5. Review that CV through four different professional lenses and improve it each time
6. Prepare you for the interview with likely questions and talking points

The skills are encrypted, so only people with the key file can use them.

---

## Before you start

You need two things from whoever shared this repo with you:

- **The repository** — a link to clone it, or the folder directly
- **The key file** — a file called `cv-generator.key`, sent to you separately (not in the repo)

Keep the key file safe. Do not put it in the repo folder or share it further without permission.

---

## Step 1 — Get the repo onto your computer

Open a terminal (on Mac: press `Cmd+Space`, type `Terminal`, press Enter) and run:

```bash
git clone <repo-url> cv-generator
cd cv-generator
```

Replace `<repo-url>` with the link you were given. This downloads the project into a folder called `cv-generator`.

If you were given the folder directly (not a URL), skip the `git clone` step and just navigate to it:

```bash
cd path/to/cv-generator
```

---

## Step 2 — Unlock the skill files

The skills are encrypted. You need `git-crypt` to unlock them.

**Install git-crypt** (one-time):

```bash
brew install git-crypt
```

If you don't have Homebrew, install it first:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**Unlock the repo** using the key file:

```bash
git-crypt unlock /path/to/cv-generator.key
```

Replace `/path/to/cv-generator.key` with wherever you saved the key file. For example, if it's in your Downloads folder:

```bash
git-crypt unlock ~/Downloads/cv-generator.key
```

You only need to do this once per machine. After this, the skill files are permanently unlocked on your computer (but stay encrypted for anyone who doesn't have the key).

---

## Step 3 — Choose your AI platform

### Decision matrix

Answer these four questions to find your best fit:

**1. How do you plan to use this?**

| | Claude Cowork | Gemini CLI | Copilot (VS Code) |
|---|:---:|:---:|:---:|
| One-off — just need a CV for one application | ✓ Best | ✓ Good | ✓ Good |
| Recurring — will use this for multiple applications over time | ✓ Best | ✓ Best | ✓ Good |
| Developing — want to edit skills, experiment, build on this | ✗ Limited | ✓ Good | ✓ Best |

**2. What's your existing setup?**

| | Claude Cowork | Gemini CLI | Copilot (VS Code) |
|---|:---:|:---:|:---:|
| I already use Claude / have a Claude account | ✓ Zero extra setup | — | — |
| I already use VS Code | — | — | ✓ Zero extra setup |
| I already use Google / have a Google account | — | ✓ Zero extra setup | — |
| I'm starting from scratch | ✓ Easiest | ✓ Easy | ~ Moderate |

**3. How comfortable are you with a terminal?**

| | Claude Cowork | Gemini CLI | Copilot (VS Code) |
|---|:---:|:---:|:---:|
| Not at all — I prefer apps with a GUI | ✓ Best | ✗ Needs terminal | ~ A little terminal |
| Comfortable with basic commands | ✓ Good | ✓ Best | ✓ Good |
| Developer — I live in the terminal / IDE | ✓ Good | ✓ Best | ✓ Best |

**4. What matters most on cost?**

| | Claude Cowork | Gemini CLI | Copilot (VS Code) |
|---|:---:|:---:|:---:|
| Free, no strings | ✓ (with limits) | ✓ Best (1,500 req/day) | ✓ (with limits) |
| Happy to pay a small amount for a better experience | ✓ Claude Pro | — | ✓ $10/mo |
| Already paying for something | ✓ if you have Pro | ✓ already free | ✓ if you have Copilot |

---

### Quick recommendation

**"I just want to try this once with minimum fuss"**
→ Claude Cowork if you have a Claude account. Gemini CLI if you're comfortable with a terminal and want no cost ceiling.

**"I'll use this regularly for job applications"**
→ Claude Cowork or Gemini CLI. Both handle recurring sessions cleanly. Cowork is more conversational; Gemini CLI is faster for experienced users.

**"I want to understand how it works, tweak the skills, or build on this"**
→ GitHub Copilot in VS Code. You'll be editing files directly in an IDE, which makes tinkering natural. Gemini CLI is a close second if you prefer the terminal.

**"I already pay for GitHub Copilot / use VS Code daily"**
→ GitHub Copilot in VS Code — zero incremental cost or setup.

**"I don't want to touch a terminal at all"**
→ Claude Cowork. It's the only option here with a pure GUI.

---

Jump to the setup section for your chosen platform:

- [Claude Cowork setup](#option-a--claude-cowork)
- [Gemini CLI setup](#option-b--gemini-cli)
- [GitHub Copilot in VS Code setup](#option-c--github-copilot-in-vs-code)

---

## Option A — Claude Cowork

### What you need
- The [Claude desktop app](https://claude.ai/download)
- A Claude account (free tier works to start)

### Setup
1. Open the Claude desktop app
2. Switch to **Cowork mode** (look for the mode selector in the app)
3. Click **Open folder** and select your `cv-generator` folder
4. Claude will detect the skills automatically — no further setup needed

### How to run a step
Just tell Claude what you want to do in plain language:

> "I want to start a new CV session."

> "Run the CV ingestion skill."

> "I have a job description ready — let's extract it."

Claude will know which skill to run and guide you through it.

---

## Option B — Gemini CLI

### What you need
- [Node.js](https://nodejs.org/) version 18 or later
- A Google account

### Setup

**Install Gemini CLI:**

```bash
npm install -g @google/gemini-cli
```

**Sign in:**

```bash
gemini auth login
```

This opens your browser. Sign in with your Google account. The free tier gives you 1,500 requests per day with Gemini 2.5 Pro — more than enough.

### How to run a step

Navigate to the project folder and start Gemini:

```bash
cd path/to/cv-generator
gemini
```

You'll see a prompt. To run a step, tell Gemini to read the skill file for that step:

> "Read `.claude/skills/01-cv-ingestion/SKILL.md` and follow the instructions."

Gemini will read the file and take you through the step. Before writing any file, it shows you exactly what it plans to write and asks for your confirmation.

See `GEMINI.md` in the project root for the full list of skill file paths.

---

## Option C — GitHub Copilot in VS Code

### What you need
- [VS Code](https://code.visualstudio.com/) (download and install if you don't have it)
- A GitHub account

### Setup

**Install the GitHub Copilot extension:**

1. Open VS Code
2. Press `Cmd+Shift+X` to open Extensions
3. Search for **GitHub Copilot** and click Install
4. When prompted, sign in with your GitHub account

**Open the project:**

```bash
code path/to/cv-generator
```

Or use File → Open Folder and select the `cv-generator` folder.

**Switch to Agent mode:**

1. Press `Cmd+Alt+I` to open Copilot Chat
2. At the top of the chat panel, click the mode selector
3. Choose **Agent**

Agent mode gives Copilot read/write access to all files in the folder.

### How to run a step

In the Agent mode chat panel:

> "Read `.claude/skills/01-cv-ingestion/SKILL.md` and follow the instructions."

Copilot will propose file changes as diffs. You accept or reject each one individually.

---

## Step 4 — Run your first session

Once your platform is set up, here is the full workflow for a new CV application.

### What to have ready before you start

- Your current CV (as a text file, Word doc, or PDF you can copy from)
- The job description you're applying to (the full text — copy it from the job posting)

### The pipeline

**Step 01 — Ingest your CV**

Trigger: say you want to start a new CV session, or explicitly ask to run step 01.

What happens: the AI asks you to paste or upload your CV. It extracts everything into a structured file called `cv-source.md`. This file becomes the source of truth for all future sessions — you won't need to upload your CV again unless something major changes.

What you do: paste your CV text, confirm the extracted version looks right, correct anything that's missing or wrong.

---

**Step 02 — Ingest the job description**

Trigger: run step 02, or say "I have a job description ready."

What happens: you paste the job description text. The AI extracts what the role actually requires — beyond the surface keywords — and saves it to a file named after the company and role.

What you do: paste the JD text and confirm the extraction.

---

**Step 03 — Clarifying questions**

Trigger: run step 03, or proceed naturally after step 02.

What happens: the AI asks you up to five targeted questions. These are not generic ("describe your strengths") — they are specific to gaps between your CV and this JD, or narrative choices that will shape the CV. Your answers are saved to `clarifications.md`.

What you do: answer the questions honestly. This is the step where you inject things that aren't on your CV — context, motivations, stories that support your application.

---

**Step 04 — Generate the first CV**

Trigger: run step 04, or proceed after step 03.

What happens: the AI generates a tailored HTML CV as `versions/cv-v1.html`. Open it in a browser to see it. This is version 1 — a solid starting point, not the final product.

What you do: open the file in your browser. Read it. You don't need to edit it manually — the reviewer steps will improve it.

---

**Steps 05–08 — Four reviewer passes**

Each step simulates a different person reviewing your CV and improving it:

- **Step 05 (Recruiter)** — the first screener. Focuses on clarity, ATS compatibility, whether you'd get to the next round. Produces `cv-v2.html`.
- **Step 06 (HR)** — culture fit, career narrative, values alignment. Produces `cv-v3.html`.
- **Step 07 (Hiring Manager)** — would you actually do the job well? Outcomes, evidence, impact. Produces `cv-v4.html`.
- **Step 08 (Technical Peer)** — do your technical or domain claims hold up? Depth and credibility. Produces `cv-v5.html`.

After each step, open the new version in your browser to see what changed. You can also ask the AI to summarise the changes if you'd rather not read the diff.

`cv-v5.html` is your final CV. Open it in a browser and print to PDF when you're ready to submit.

---

**Steps 09–12 — Interview prep (optional)**

Run these after you have a final CV and have been invited to interview.

- **Step 09** — recruiter screen prep (usually a 15–30 min call)
- **Step 10** — HR interview prep
- **Step 11** — hiring manager interview prep
- **Step 12** — technical interview prep

Each step produces a file with likely questions and suggested talking points based on your specific CV and JD. They're independent — run only the ones relevant to your interview process.

---

## Returning to a session

If you've already ingested your CV (`cv-source.md` exists) and want to apply for another role:

- Skip step 01. Your CV data is already there.
- Run step 02 with the new job description.
- Proceed from step 03.

If you're picking up mid-session on the same application:

- Just tell the AI where you left off: "I've done steps 01–04, I want to run the recruiter review."
- The AI will read the existing files and continue.

---

## Troubleshooting

**The skill files look like garbled text / binary**
You haven't unlocked the repo. Go back to Step 2 and run `git-crypt unlock`.

**`git-crypt` says "not a git-crypt repo"**
You're not in the right folder, or the `.gitattributes` file is missing. Make sure you're in the `cv-generator` directory.

**The AI says it can't find a file**
Check that the file exists in the folder. If you're mid-session and `cv-source.md` is missing, run step 01 first. If `clarifications.md` is missing, run step 03.

**The generated CV looks wrong or generic**
The clarifying questions in step 03 are the most important input. Go back, re-run step 03 with more detailed answers, then re-run steps 04–08.

**I want to start completely fresh**
Delete `cv-source.md`, `clarifications.md`, `jd-*.md`, and the `versions/` folder. Keep the `findings/` folder if you want to preserve accumulated reviewer knowledge, or delete it too for a total reset.

---

## Files you'll see after a full session

```
cv-generator/
├── cv-source.md               ← your CV in structured form
├── jd-acme-engineer.md        ← the job description (example name)
├── clarifications.md          ← your answers to the pre-gen questions
├── versions/
│   ├── cv-v1.html             ← generated CV
│   ├── cv-v2.html             ← after recruiter review
│   ├── cv-v3.html             ← after HR review
│   ├── cv-v4.html             ← after hiring manager review
│   └── cv-v5.html             ← final CV (submit this one)
├── findings/
│   ├── recruiter.md           ← reviewer notes (grow over sessions)
│   ├── hr.md
│   ├── hiring-manager.md
│   └── technical-peer.md
└── interview-prep/
    ├── questions-recruiter.md
    ├── questions-hr.md
    ├── questions-hiring-manager.md
    └── questions-technical-peer.md
```

Everything stays on your machine. Nothing is sent anywhere.
