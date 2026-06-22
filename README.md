# CV Generator

A Claude Cowork project that helps you tailor your CV to any job description, refine it through four expert reviewer lenses, and prepare for the interview — all within your own project folder.

The skill prompts in this repo are encrypted with [git-crypt](https://github.com/AGWA/git-crypt). You need a key from the repo owner to unlock them.

---

## What this project does

1. **Ingests your existing CV** and stores the key information in a structured format
2. **Ingests a Job Description** and extracts what the role actually requires
3. **Asks clarifying questions** to capture your narrative before generating
4. **Generates a tailored CV (v1)** matched to the JD
5. **Refines it through four reviewer perspectives:**
   - v2 — Recruiter review (clarity, formatting, ATS signals)
   - v3 — HR review (culture fit, role alignment)
   - v4 — Hiring Manager review (outcomes, impact, credibility)
   - v5 — Technical Peer review (depth, specifics, credibility in the domain)
6. **Prepares you for the interview** with likely questions and talking points per persona

All versions are saved as HTML files. All reviewer findings are recorded and improve future sessions.

---

## Setup (first time only)

### 1. Install git-crypt

```bash
brew install git-crypt
```

### 2. Unlock the repo

You need the key file (`cv-generator.key`) from the repo owner. Once you have it:

```bash
cd cv-generator
git-crypt unlock /path/to/cv-generator.key
```

The skill files will decrypt automatically. You only need to do this once per machine.

### 3. Register the skills with Claude

Open this folder in Claude Cowork. The `.claude/skills/` folder is already in the right place — Claude will pick them up automatically.

---

## First time here?

Tell Claude which of these you want to do:

**A — New CV session**
Start fresh. You'll upload or paste your CV, then provide a Job Description, answer a few clarifying questions, and receive your first tailored CV.

**B — Continue an existing session**
Pick up where you left off. Claude will load your existing CV data and the current JD, and show you where you are in the review cycle.

**C — Interview prep**
You have a final CV version and want to prepare for the interview. Claude will load your CV and generate questions and talking points from each reviewer's perspective.

---

## Returning user?

Just tell Claude what you want to do next and it will orient itself from the files in this folder.

---

## Files in this project

| File / Folder | What it contains |
|---|---|
| `cv-source.md` | Your structured CV data (extracted on first ingestion) |
| `jd-[company]-[role].md` | Extracted Job Description data |
| `clarifications.md` | Your answers to pre-generation questions |
| `versions/cv-v1.html` → `cv-v5.html` | All CV versions |
| `findings/recruiter.md` | Recruiter persona's accumulated findings |
| `findings/hr.md` | HR persona's accumulated findings |
| `findings/hiring-manager.md` | Hiring Manager persona's accumulated findings |
| `findings/technical-peer.md` | Technical Peer persona's accumulated findings |
| `interview-prep/` | Questions and talking points per persona |
| `lessons-learned.md` | Accumulated lessons from past sessions |

---

*See `docs/usage-guide.md` for detailed instructions.*
