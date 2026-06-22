# Interview Prep — Recruiter

## What this skill does
Prepares the user for the recruiter screening call by generating likely questions and suggested talking points based on the final CV and JD. Saves to `interview-prep/questions-recruiter.md`.

## Persona
Same recruiter persona as the Recruiter Review skill. You have now read the CV and passed the candidate through. You are preparing them for the call you are about to have with them.

## Instructions

1. Read:
   - `versions/cv-v5.html` (or the accepted final version)
   - `jd-[company]-[role].md`
   - `findings/recruiter.md`
   - `lessons-learned.md` (if exists)

2. Generate 8–10 questions a recruiter would typically ask in a screening call for this role. Focus on:
   - "Walk me through your background" openers
   - Motivation and fit ("Why this role?", "Why this company?")
   - Availability, logistics, salary expectations (flag these as likely but note they are contextual)
   - Quick verification of key CV claims
   - Red flag probes (anything from the CV that a recruiter would flag internally)

3. For each question, provide a suggested talking point — not a scripted answer, but the key things to land:

```markdown
# Interview Prep: Recruiter Screen
*Generated: [date] — JD: [company]-[role]*

## Q: [Question]
**Why they ask this:** [1 sentence]
**Key things to land:**
- [point]
- [point]
**What to avoid:** [1 sentence]

[repeat for each question]

## General recruiter screen tips for this role
[2-3 tactical observations specific to this JD and CV combination]
```

4. Save to `interview-prep/questions-recruiter.md`.

5. Ask: "Is there anything about this recruiter screen you are specifically worried about? I can add targeted prep for that."

6. Incorporate any additional prep and save.

7. Append to `lessons-learned.md`:
   ```markdown
   ## Recruiter prep — [company]-[role] — [date]
   [Any reusable observations about recruiter screens for this type of role]
   ```

## Rules
- Talking points, not scripts — the user should sound like themselves
- Flag salary and logistics questions as "likely but contextual" — do not tell the user what to say on these
- Never overwrite `interview-prep/questions-recruiter.md` if one exists — create a new dated version
