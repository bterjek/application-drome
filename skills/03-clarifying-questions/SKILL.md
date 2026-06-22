# Clarifying Questions

## What this skill does
Asks targeted questions before CV generation to capture narrative, tone, and specific experiences that cannot be extracted from the CV or JD alone. Saves answers to `clarifications.md`.

## Instructions

1. Read `cv-source.md` and the most recent `jd-[company]-[role].md` in full before asking anything.

2. Also read `lessons-learned.md` if it exists — past sessions may have flagged narrative gaps worth asking about.

3. Identify the gaps between the CV and the JD: what experiences, achievements, or narratives from the CV are most relevant to this role but may need emphasis or reframing?

4. Ask no more than 5 questions per session. Prioritise:
   - Narrative questions: "How would you describe your impact in [X role] in your own words?"
   - Reframing questions: "The JD emphasises [Y]. Which of your experiences best demonstrates this?"
   - Gap questions: "The JD asks for [Z] but your CV doesn't mention it directly. Is there experience there?"
   - Tone questions: "The JD reads as [formal/startup/technical]. Do you want the CV to match that tone or establish your own?"
   - Preference questions: "Is there anything you want to make sure is prominent in this version?"

5. Wait for all answers before proceeding.

6. Save answers to `clarifications.md`:

```markdown
# Clarifications
*Session: [date] — JD: [company]-[role]*

## Q: [question]
**A:** [answer]

[repeat for each Q&A]
```

7. Confirm: "Thank you — this is enough to generate your tailored CV. Run the CV Generation skill when ready."

## Rules
- Never skip this step even if the CV and JD seem like an obvious match
- Do not ask questions answerable from the CV or JD directly — only ask what is genuinely missing
- Maximum 5 questions — if more gaps exist, prioritise the ones that most affect the narrative
