# Start a new project

Paste the prompt below into Claude Code, **inside the new project's empty folder** (not inside this repo).

Replace `<GUIDELINES_PATH>` with the path where you cloned or downloaded this repo (e.g. `~/dev-guidelines`).

````text
You are helping me start a new web project. My team's dev guidelines live at <GUIDELINES_PATH>.

Read first: <GUIDELINES_PATH>/README.md and <GUIDELINES_PATH>/playbook/README.md.
Then walk me through the playbook one step at a time.

For each step follow its shape: ask the questions in "Ask the user", confirm choices in
"Decide together", run the relevant "Actions" branch (Dev or Designer), check the "Output",
then "Compile into the project" — bake what's needed into this project's AGENTS.md (and
optionally a linked guidelines.md).

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
5. By the end, this project should be self-contained — we shouldn't need to keep reading
   the guidelines repo for day-to-day work.
6. If we discover something worth saving for future projects, flag it. I'll decide whether
   to update the guidelines repo.

Start by asking: what kind of project is this, who's the audience, and do I already know
the stack?
````

## One-time setup

**Developers**

```sh
gh repo clone <org>/dev-guidelines ~/dev-guidelines
```

**Designers / non-technical**

Use GitHub Desktop, or click "Code → Download ZIP" on the repo page and unzip to `~/dev-guidelines`.

Keep it current with an occasional `git pull` (or re-download the ZIP).

## Optional: install as a slash command

Once you've used the kickoff prompt a few times, you can save it as a Claude Code slash command (`~/.claude/commands/start-project.md`) so future projects start with just `/start-project`. Details to come.
