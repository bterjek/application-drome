# JD Ingestion

## What this skill does
Extracts structured signals from a Job Description and saves them to `jd-[company]-[role].md`. This file feeds the CV generation and all reviewer personas.

## Instructions

1. Ask the user to paste the Job Description.

2. Read it in full before extracting.

3. Extract into `jd-[company]-[role].md` (derive company and role from the JD):

```markdown
# Job Description: [Role] — [Company]
*Ingested: [date]*

## Role basics
- Title:
- Company:
- Location / remote policy:
- Seniority level:

## Company signals
[What can be inferred about the company's culture, values, stage, priorities from the JD language]

## Must-have requirements
[Hard requirements explicitly stated]

## Nice-to-have requirements
[Stated as preferred / bonus / desirable]

## What success looks like in this role
[Inferred from responsibilities and any stated outcomes]

## Keywords and phrases to reflect in the CV
[ATS-relevant terms, repeated phrases, specific technologies or methodologies named]

## Red flags or unusual requirements
[Anything that stands out as atypical or worth addressing in the CV]

## Tone of the JD
[Formal / casual / technical / startup / corporate — affects CV tone]
```

4. Show the extracted output. Ask: "Does this look right? Anything to add or correct about this role?"

5. Apply corrections, save the file.

6. Confirm: "JD saved. Run the Clarifying Questions skill next to prepare for CV generation."

## Rules
- Do not generate a CV yet
- Preserve the company and role name in the filename exactly as written in the JD
- If multiple JDs exist in the folder, do not overwrite — create a new file each time
