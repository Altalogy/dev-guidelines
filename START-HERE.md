# Start a new project

Paste the prompt below into Claude Code, **inside the new project's empty folder**. No setup required — Claude reads the guidelines directly from GitHub.

````text
You are helping me start a new web project. My team's dev guidelines are public at:
https://github.com/Altalogy/dev-guidelines

Use WebFetch to read files. Raw URL pattern:
https://raw.githubusercontent.com/Altalogy/dev-guidelines/main/<path>

When you encounter a relative markdown link inside a guidelines file, resolve it against
the repo root (`.../main/`).

Read first:
- https://raw.githubusercontent.com/Altalogy/dev-guidelines/main/README.md
- https://raw.githubusercontent.com/Altalogy/dev-guidelines/main/playbook/README.md

Then walk me through the playbook one step at a time. Fetch each step file as you reach it
(e.g. .../main/playbook/01-pick-stack.md).

For each step follow its shape: ask the questions in "Ask the user", confirm choices in
"Decide together", run the relevant "Actions" branch (Dev or Designer), check the "Output",
then "Compile into the project" — bake what's needed into this project's AGENTS.md (and
optionally a linked guidelines.md).

The current working directory is the new project's folder. Create all new files here.
Do not modify the guidelines repo.

Rules:

1. One step at a time. Confirm before moving on.
2. **Don't blindly apply the guidelines.** They are a starting point. If something looks
   outdated for today's date or current best practices, flag it and suggest the modern
   alternative. Web tooling moves fast.
3. External actions I might not have access to (GitHub repo creation, Vercel access,
   domain config): either walk me through them or give me a clear message I can send to
   a teammate. Don't silently fail.
4. Gauge my technical level. For designers / non-technical users: slow down, explain each
   command before running, prefer GUI options where they work.
5. By the end, this project should be self-contained — we shouldn't need to keep fetching
   from the guidelines repo for day-to-day work. Compile what we need into AGENTS.md.
6. If we discover something worth saving for future projects, flag it. I'll decide whether
   to update the guidelines repo.

Start by asking: what kind of project is this, who's the audience, and do I already know
the stack?
````

## Optional: save as a slash command

If you use this often, save the prompt as a Claude Code slash command at `~/.claude/commands/start-project.md` — then future projects start with `/start-project`.

---

## For maintainers

For the one-paste workflow to work, this repo **must be public on GitHub**. To enable:

1. Push to `Altalogy/dev-guidelines` (first time): `git push -u origin main`
2. On GitHub: **Settings → General → Danger Zone → Change visibility → Public**

After that, every teammate (and every designer) needs zero local setup — just paste the prompt above.
