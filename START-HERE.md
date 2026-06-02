# Start a new project

Paste the prompt below into Claude Code, **inside the new project's empty folder**. No setup required — Claude reads everything from GitHub.

```text
Let's start a new project. Use this as the starting point: https://raw.githubusercontent.com/Altalogy/dev-guidelines/main/kickoff.md (Repo: https://github.com/Altalogy/dev-guidelines)
```

The detailed instructions live in [kickoff.md](kickoff.md) — Claude fetches it and walks the playbook from there.

## Optional: save as a slash command

If you use this often, save the prompt as a Claude Code slash command at `~/.claude/commands/start-project.md` — then future projects start with `/start-project`.

---

## For maintainers

For the one-paste workflow to work, this repo **must be public on GitHub**. To enable:

1. Push to `Altalogy/dev-guidelines` (first time): `git push -u origin main`
2. On GitHub: **Settings → General → Danger Zone → Change visibility → Public**

After that, every teammate (and every designer) needs zero local setup — just paste the prompt above.
