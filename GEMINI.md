# CV Generator — Gemini CLI

This project uses a 12-step skill pipeline to tailor CVs to job descriptions, refine them through four reviewer personas, and prepare for interviews. All workflow instructions live in `.claude/skills/` as individual markdown files.

## How to use this project

Open a terminal in this project folder and run `gemini`. Then tell Gemini which step you want to run. Gemini has full access to read and write files in this folder.

## Workflow steps

To run a step, ask Gemini to read the corresponding skill file and follow the instructions in it. Example:

> "Read `.claude/skills/01-cv-ingestion/SKILL.md` and follow the instructions."

| Step | Skill file | What it does |
|------|-----------|-------------|
| 1 | `.claude/skills/01-cv-ingestion/SKILL.md` | Extract CV into structured markdown |
| 2 | `.claude/skills/02-jd-ingestion/SKILL.md` | Extract job description signals |
| 3 | `.claude/skills/03-clarifying-questions/SKILL.md` | Ask targeted questions before generating |
| 4 | `.claude/skills/04-cv-generation/SKILL.md` | Generate tailored HTML CV (v1) |
| 5 | `.claude/skills/05-recruiter-review/SKILL.md` | Recruiter lens — produce v2 |
| 6 | `.claude/skills/06-hr-review/SKILL.md` | HR lens — produce v3 |
| 7 | `.claude/skills/07-hiring-manager-review/SKILL.md` | Hiring manager lens — produce v4 |
| 8 | `.claude/skills/08-technical-review/SKILL.md` | Technical peer lens — produce v5 |
| 9 | `.claude/skills/09-interview-prep-recruiter/SKILL.md` | Recruiter screen prep |
| 10 | `.claude/skills/10-interview-prep-hr/SKILL.md` | HR interview prep |
| 11 | `.claude/skills/11-interview-prep-hiring-manager/SKILL.md` | Hiring manager interview prep |
| 12 | `.claude/skills/12-interview-prep-technical/SKILL.md` | Technical interview prep |

## Starting points

**New application:** Start with step 1, then proceed in order through step 8. Steps 9–12 are optional interview prep after you have a final CV.

**Returning user (new JD, same CV):** Skip step 1. Start at step 2 with the new job description.

**Interview prep only:** Skip steps 1–8. Run steps 9–12 after confirming you have a final CV version in `versions/`.

## Notes

- Gemini operates within this project directory. All files it reads and writes stay local.
- You will be shown proposed file changes before they are applied.
- If a skill file appears as binary (encrypted), you need to unlock the repo with git-crypt first. See `README.md`.
