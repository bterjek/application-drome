# Setup — GitHub Copilot (VS Code Agent Mode)

## What you need

- [VS Code](https://code.visualstudio.com/) (latest)
- A GitHub account
- GitHub Copilot (Free tier works; Individual $10/mo removes monthly limits)

## Install GitHub Copilot in VS Code

1. Open VS Code
2. Go to Extensions (`Cmd+Shift+X`)
3. Search for **GitHub Copilot** and install it
4. Sign in with your GitHub account when prompted

## Enable agent mode

1. Open the Copilot Chat panel (`Ctrl+Alt+I` / `Cmd+Alt+I`)
2. Click the mode selector at the top of the chat panel
3. Select **Agent**

Agent mode gives Copilot read/write access to your workspace files and the ability to run terminal commands.

## Unlock the repo

You need `cv-generator.key` from the repo owner.

```bash
brew install git-crypt
git-crypt unlock /path/to/cv-generator.key
```

## Open the project

```bash
code path/to/cv-generator
```

Or: File → Open Folder → select the `cv-generator` directory.

## Run the project

With agent mode active, use the workflow table in `.github/copilot-instructions.md`. Copilot will read this file automatically as repo-level context. Example prompt:

> "Read `.claude/skills/01-cv-ingestion/SKILL.md` and follow the instructions."

Copilot will propose file changes as diffs — accept or reject each one individually.

## Tier comparison

| Tier | Price | Agent mode |
|------|-------|-----------|
| Copilot Free | Free | Yes (limited completions/month) |
| Copilot Individual | $10/mo | Yes (unlimited) |
| Copilot Business | $19/mo per user | Yes (unlimited + org features) |

For personal CV work, Free or Individual is sufficient.
