# CV Generator — Usage Guide

## What this project does

Takes your existing CV and a job description, then produces a tailored HTML CV through four distinct reviewer personas. Each persona accumulates knowledge across sessions — the more you use it, the better the feedback gets.

---

## Setup (first time only)

1. Open this project in Claude Cowork.
2. Move the contents of `skills/` into `.claude/skills/` — this makes the skills available to Claude in this project.
3. You're done. Open the README to start.

---

## Typical session flow

```
Upload CV → Extract (skill 01) → Upload JD → Extract (skill 02)
→ Clarifying questions (skill 03) → Generate v1 (skill 04)
→ Recruiter review → v2 (skill 05)
→ HR review → v3 (skill 06)
→ Hiring Manager review → v4 (skill 07)
→ Technical Peer review → v5 (skill 08) ← final CV
→ Interview prep (skills 09–12)
```

---

## Skills reference

| # | Skill | What it does | Output |
|---|-------|-------------|--------|
| 01 | cv-ingestion | Extracts CV to structured markdown | `cv-source.md` |
| 02 | jd-ingestion | Extracts JD signals to markdown | `jd-[company]-[role].md` |
| 03 | clarifying-questions | Asks up to 5 targeted questions | `clarifications.md` |
| 04 | cv-generation | Generates tailored HTML CV | `versions/cv-v1.html` |
| 05 | recruiter-review | Recruiter lens, ATS focus | `versions/cv-v2.html` + `findings/recruiter.md` |
| 06 | hr-review | Culture fit, career narrative | `versions/cv-v3.html` + `findings/hr.md` |
| 07 | hiring-manager-review | Evidence and impact focus | `versions/cv-v4.html` + `findings/hiring-manager.md` |
| 08 | technical-review | Domain depth and credibility | `versions/cv-v5.html` + `findings/technical-peer.md` |
| 09 | interview-prep-recruiter | Recruiter screen prep | `interview-prep/questions-recruiter.md` |
| 10 | interview-prep-hr | HR interview prep | `interview-prep/questions-hr.md` |
| 11 | interview-prep-hiring-manager | Hiring manager prep | `interview-prep/questions-hiring-manager.md` |
| 12 | interview-prep-technical | Technical peer prep | `interview-prep/questions-technical-peer.md` |

---

## Persistent files

| File | Written by | Purpose |
|------|-----------|---------|
| `cv-source.md` | Skill 01 | Your CV in structured markdown — reused across sessions |
| `clarifications.md` | Skill 03 | Your answers to clarifying questions |
| `lessons-learned.md` | All skills (append) | Accumulated knowledge across all sessions |
| `findings/recruiter.md` | Skill 05 (append) | Recruiter observations across sessions |
| `findings/hr.md` | Skill 06 (append) | HR observations across sessions |
| `findings/hiring-manager.md` | Skill 07 (append) | Hiring manager observations across sessions |
| `findings/technical-peer.md` | Skill 08 (append) | Technical peer observations across sessions |
| `versions/` | Skills 04–08 | All CV versions, never overwritten |
| `interview-prep/` | Skills 09–12 | Interview prep files per session |

**All files stay in this folder. Nothing is sent externally.**

---

## Continuing an existing session

If you already have a `cv-source.md` and a JD file, you can skip straight to any skill. Skills read from the files already present — they don't require a fresh upload each time.

---

## Interview prep (standalone)

If you have a final CV (v5) and want to prepare for interviews without re-running the review cycle, open the README and choose path C. Run skills 09–12 in any order.

---

## Notes

- CV versions are never overwritten. `cv-v1.html` through `cv-v5.html` are always available for comparison.
- Findings files are append-only. Past learnings inform future sessions automatically.
- If you apply to the same company twice, the skill will detect the existing JD file and ask whether to update it or create a new dated version.
