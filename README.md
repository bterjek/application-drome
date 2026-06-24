# CV Generator

A Claude Cowork project that tailors your CV to any job description, refines it through four expert reviewer lenses, and prepares you for every stage of the interview process.

The skill prompts are encrypted with [git-crypt](https://github.com/AGWA/git-crypt). You need a key from the repo owner to unlock them.

---

## How it works

You bring a CV and a job description. The project runs them through a structured pipeline:

```
Your CV → extract → JD → extract → clarifying questions
       → generate v1 → recruiter review → v2
                     → HR review → v3
                     → hiring manager review → v4
                     → technical peer review → v5 (final)
                     → interview prep per persona
```

Each reviewer persona has a distinct focus and leaves behind a findings file. Those findings persist across sessions — the more you use the project, the sharper the feedback gets.

---

## Setup

### 1. Install git-crypt

```bash
brew install git-crypt
```

### 2. Clone the repo

```bash
git clone <repo-url>
cd cv-generator
```

### 3. Unlock with the key

You need `cv-generator.key` from the repo owner. Once you have it:

```bash
git-crypt unlock /path/to/cv-generator.key
```

The skill files decrypt in place. You only need to do this once per machine.

### 4. Open in Claude Cowork

Open the `cv-generator` folder in Cowork. Claude will pick up the skills automatically from `.claude/skills/`. No manual setup required.

---

## Starting a session

Tell Claude which path you want:

**A — New application**
You have a CV and a new job description. Claude will extract both, ask a few targeted questions, and generate a tailored CV from scratch.

**B — Continue an existing session**
You have a `cv-source.md` already. Provide a new JD and jump straight to generation — no need to re-upload your CV.

**C — Interview prep only**
You have a final CV (v5) and want to prepare for the interview. Run skills 09–12 in any order, one per interview stage.

---

## Skills reference

| # | Skill | What it does | Output |
|---|-------|-------------|--------|
| 01 | cv-ingestion | Extracts your CV into structured markdown | `cv-source.md` |
| 02 | jd-ingestion | Extracts JD signals and requirements | `jd-[company]-[role].md` |
| 03 | clarifying-questions | Asks up to 5 targeted questions to capture your narrative | `clarifications.md` |
| 04 | cv-generation | Generates a tailored HTML CV | `versions/cv-v1.html` |
| 05 | recruiter-review | Recruiter lens — ATS, clarity, first impression | `versions/cv-v2.html` + `findings/recruiter.md` |
| 06 | hr-review | HR lens — culture fit, values, career narrative | `versions/cv-v3.html` + `findings/hr.md` |
| 07 | hiring-manager-review | Hiring manager lens — outcomes, impact, credibility | `versions/cv-v4.html` + `findings/hiring-manager.md` |
| 08 | technical-review | Technical peer lens — depth, specifics, domain credibility | `versions/cv-v5.html` + `findings/technical-peer.md` |
| 09 | interview-prep-recruiter | Likely questions + talking points for recruiter screen | `interview-prep/questions-recruiter.md` |
| 10 | interview-prep-hr | Likely questions + talking points for HR interview | `interview-prep/questions-hr.md` |
| 11 | interview-prep-hiring-manager | Likely questions + talking points for hiring manager | `interview-prep/questions-hiring-manager.md` |
| 12 | interview-prep-technical | Likely questions + talking points for technical interview | `interview-prep/questions-technical-peer.md` |

---

## Files in this project

| File / Folder | What it contains | Persists across sessions? |
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
- Findings files are append-only. Past observations from previous applications automatically inform the next session.
- If you apply to the same company twice, skill 02 will detect the existing JD file and ask whether to update it or create a dated version.
- You can skip any reviewer if it's not relevant. The skills are independent — v3 doesn't require v2 to exist first.
