# CV Generator — Usage Guide

See `README.md` for setup, session flow, skills reference, and file layout.

This file covers edge cases and less-obvious behaviour.

---

## Skipping steps

Skills are independent. If you already have `cv-source.md` from a previous session, skip skill 01. If you want to jump straight to a specific reviewer, that's fine — each skill reads from whatever files are present and states what it needs if something is missing.

## Multiple applications in parallel

Each JD gets its own file (`jd-[company]-[role].md`). When starting a new application, run skill 02 with the new JD. Skills 03–08 will ask which JD to use if more than one is present.

## Applying to the same company again

Skill 02 detects existing JD files for the same company and asks whether to update or create a new dated version (e.g. `jd-acme-engineer-2025-09.md`). The findings files for that company are still available and will inform the new session.

## The findings files

`findings/recruiter.md`, `findings/hr.md`, `findings/hiring-manager.md`, and `findings/technical-peer.md` are append-only. Each reviewer skill adds a dated entry after every session. Over time, these files accumulate pattern observations — things you consistently do well, things that keep getting flagged — and the reviewer personas use them to give sharper feedback.

You can read and edit these files directly. If a past observation is no longer relevant, delete it.

## Lessons learned

`lessons-learned.md` is written by any skill that notices something worth carrying forward — a framing that worked particularly well, a type of role that needs a different approach, a formatting choice that keeps getting flagged. It's read at the start of every generation and review step.

## CV versions

v1 through v5 are never overwritten. If you re-run a reviewer after making manual edits, the skill will create a new version (e.g. `cv-v3b.html`) rather than replacing the original.

## Interview prep

Skills 09–12 are independent of each other and can be run in any order. They read from the final CV version and the current JD. Run them after you have a CV you're happy with, not necessarily after completing all four reviewer steps.
