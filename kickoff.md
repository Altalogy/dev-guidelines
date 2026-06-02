# Project Kickoff Instructions

> Pulled by Claude when a new project is started via the kickoff prompt. Not meant to be read by humans day-to-day.

You are helping me start a new web project. My team's dev guidelines are public at:
https://github.com/Altalogy/dev-guidelines

Use WebFetch to read files. Raw URL pattern:
https://raw.githubusercontent.com/Altalogy/dev-guidelines/main/<path>

When you encounter a relative markdown link inside a guidelines file, resolve it against
the repo root (`.../main/`).

## Read first

- https://raw.githubusercontent.com/Altalogy/dev-guidelines/main/README.md
- https://raw.githubusercontent.com/Altalogy/dev-guidelines/main/playbook/README.md

Then walk me through the playbook one step at a time. Fetch each step file as you reach it
(e.g. `.../main/playbook/01-pick-stack.md`).

## How to run each step

For each step, follow its shape:

1. Ask the questions in **"Ask the user"** (step 1 is a 5-question wizard — lead with it).
2. Confirm choices in **"Decide together"**.
3. Run the relevant **"Actions"** branch (Dev or Designer).
4. Check the **"Output"**.
5. **"Compile into the project"** — bake what's needed into this project's `AGENTS.md` (and optionally a linked `guidelines.md`).

The current working directory is the new project's folder. Create all new files here.
Do not modify the guidelines repo.

## Rules

1. **One step at a time.** Confirm before moving on.
2. **Don't blindly apply the guidelines.** They are a starting point. If something looks
   outdated for today's date or current best practices, flag it and suggest the modern
   alternative. Web tooling moves fast.
3. **External actions** I might not have access to (GitHub repo creation, Vercel access,
   domain config): either walk me through them or give me a clear message I can send to
   a teammate. Don't silently fail.
4. **Gauge my technical level.** For designers / non-technical users: slow down, explain
   each command before running, prefer GUI options where they work.
5. **End self-contained.** By the end, this project shouldn't need to keep fetching from
   the guidelines repo for day-to-day work. Compile what we need into `AGENTS.md`.
6. **Flag improvements.** If we discover something worth saving for future projects, flag
   it. I'll decide whether to update the guidelines repo.

## Start

Start with **Step 1** — the 5-question wizard in `playbook/01-pick-stack.md`. Lead with
Question 1 (project type).
