# CV Generation

## What this skill does
Generates a tailored HTML CV (v1) based on the ingested CV data, JD signals, and clarification answers. Saves to `versions/cv-v1.html`.

## Instructions

1. Read in full before generating:
   - `cv-source.md`
   - The most recent `jd-[company]-[role].md`
   - `clarifications.md`
   - `lessons-learned.md` (if exists — apply any prior lessons relevant to this role type)

2. Generate a tailored CV that:
   - Leads with a professional summary rewritten for this specific role
   - Reorders and reframes experience entries to foreground what this JD values most
   - Reflects the JD's keywords naturally (not stuffed)
   - Matches the tone of the JD where appropriate
   - Incorporates the narrative and framing from clarifications
   - Is truthful — does not invent experience or achievements

3. Output as clean, well-structured HTML saved to `versions/cv-v1.html`. Use this structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>[Name] — CV</title>
  <style>
    body { font-family: Georgia, serif; max-width: 800px; margin: 40px auto; color: #1a1a1a; line-height: 1.6; }
    h1 { font-size: 2em; margin-bottom: 0; }
    h2 { border-bottom: 1px solid #ccc; padding-bottom: 4px; margin-top: 32px; }
    h3 { margin-bottom: 4px; }
    .meta { color: #555; font-size: 0.9em; }
    ul { margin-top: 4px; }
  </style>
</head>
<body>
  <!-- Name, contact, links -->
  <!-- Summary -->
  <!-- Experience -->
  <!-- Skills -->
  <!-- Education -->
  <!-- Certifications -->
  <!-- Other -->
</body>
</html>
```

4. After saving, confirm: "CV v1 is saved to `versions/cv-v1.html`. Run the Recruiter Review skill to begin the refinement cycle."

5. Do NOT show the full HTML in the chat — confirm the file is saved and tell the user where to find it.

## Rules
- Do not invent anything not present in cv-source.md or clarifications.md
- Every version must be a complete, standalone HTML file
- v1 is the starting point — do not attempt to make it perfect, the reviewer cycle will refine it
