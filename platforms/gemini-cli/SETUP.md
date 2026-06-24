# Setup — Gemini CLI

## What you need

- A Google account
- Node.js 18 or later

## Install Gemini CLI

```bash
npm install -g @google/gemini-cli
```

## Authenticate

```bash
gemini auth login
```

This opens a browser to sign in with your Google account. The free tier gives you generous usage limits (1,500 requests/day with Gemini 2.5 Pro as of 2026).

## Unlock the repo

You need `cv-generator.key` from the repo owner.

```bash
brew install git-crypt
git-crypt unlock /path/to/cv-generator.key
```

## Run the project

```bash
cd path/to/cv-generator
gemini
```

Gemini CLI starts in the project directory with full read/write access to all files. See `GEMINI.md` at the project root for the workflow and how to invoke each step.

## Tips

- Gemini will show you a diff before writing any file. Press `y` to confirm or `n` to reject.
- If you want to give Gemini broader context, run with `gemini --include-all-files` — it will index everything in the directory.
- Your CV data, JD files, and generated CVs never leave your machine unless you explicitly share them.
