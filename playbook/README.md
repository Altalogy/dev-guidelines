# Playbook

Step-by-step from "we're starting a new project" to "deployed and ready to iterate." Used by Claude Code via [START-HERE.md](../START-HERE.md), but also readable on its own.

## Step shape

Every step uses the same shape so Claude can drive it predictably:

- **Goal** — what we're achieving
- **Ask the user** — questions Claude poses first
- **Decide together** — what to confirm before acting
- **Actions** — concrete steps, with **Dev:** / **Designer:** forks where they differ
- **External actions** — "send this to your teammate" templates for access requests
- **Output** — what should exist when done
- **Compile into the project** — what gets baked into the new project's `AGENTS.md` / `guidelines.md`

## Steps

1. [Pick the stack](01-pick-stack.md) — 5-question wizard
2. [Scaffold the project](02-scaffold.md)
3. [Set up AI](03-setup-ai.md)
4. [Design handoff](04-design-handoff.md) *(stub)*
5. [Build features with AI](05-build-feature.md) *(stub)*
6. [Code review with AI](06-review.md) *(stub)*
7. [Deploy](07-deploy.md) *(stub)*

## Reference docs (used by the steps)

- [stack.md](../reference/stack.md) — framework comparison
- [cms.md](../reference/cms.md) — CMS comparison + defaults per framework
- [tech-stack.md](../reference/tech-stack.md) — toolbox + Default bundle
- [deployment.md](../reference/deployment.md) — Vercel / Cloudflare Pages / AWS / Webflow
- [scaffold.md](../reference/scaffold.md) — folder conventions per project type

## Notes for Claude

- One step at a time. Confirm before moving on.
- In step 1, lead with the wizard. Skip questions whose answer is determined by an earlier one.
- For stub steps, state what they will cover and ask the user whether to skip, improvise from today's best practices, or stop here.
- Don't blindly apply: if something looks outdated for the current date or chosen stack, flag it.
- Open items live in [../todo.md](../todo.md). When you stub something, add it there so it doesn't get lost.
