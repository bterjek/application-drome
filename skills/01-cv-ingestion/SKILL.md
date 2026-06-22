# CV Ingestion

## What this skill does
Extracts structured information from an existing CV and saves it to `cv-source.md` in the project folder. This becomes the source of truth for all future CV generations.

## Instructions

1. Ask the user to paste their CV text or confirm the file has been uploaded.

2. Read the entire CV before extracting anything.

3. Extract into `cv-source.md` using this exact structure:

```markdown
# CV Source Data
*Last updated: [date]*

## Personal
- Name:
- Location:
- Email:
- Phone:
- LinkedIn:
- Other links:

## Professional Summary
[2-4 sentences capturing the candidate's overall professional identity]

## Experience
### [Job Title] — [Company] ([Start] – [End])
- Key responsibilities:
- Notable achievements (quantified where possible):
- Technologies / tools / methods used:

[repeat for each role, most recent first]

## Skills
### Technical:
### Domain / Industry:
### Languages:
### Tools & Platforms:

## Education
### [Degree] — [Institution] ([Year])

## Certifications
- [Certification] — [Body] — [Year]

## Other
[Awards, publications, volunteering, anything else notable]
```

4. Show the extracted output and ask: "Does this capture everything correctly? Anything missing or to correct?"

5. Apply corrections, then save final version to `cv-source.md`.

6. Confirm: "Your CV data is saved. Run the JD Ingestion skill to continue."

## Rules
- Extract faithfully — do not summarise or paraphrase
- Do not discard anything from the original
- Do not generate a CV yet — that comes after JD ingestion and clarifying questions
