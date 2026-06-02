# Dev Guidelines

Our guidelines — and your sidekick — for developing websites. Covers tech stack choices, project setup, AI workflows, and conventions.

## Getting started

Paste this into Claude Code inside the new project's empty folder:

```text
Let's start a new project. Use this as the starting point: https://raw.githubusercontent.com/Altalogy/dev-guidelines/main/kickoff.md (Repo: https://github.com/Altalogy/dev-guidelines)
```

Claude reads [kickoff.md](kickoff.md), walks the playbook with you, and bakes the result into the new project. See [START-HERE.md](START-HERE.md) for slash-command setup.

## How this works

This repo is a long-term **wiki**. When you start a new project, Claude Code reads the playbook directly from GitHub (no clone required) and **compiles what's needed into the new project** (`AGENTS.md`, optionally a linked `guidelines.md`). After setup, the new project is self-contained — you don't need to keep looking back. Return here for:

- generic, cross-project aid (e.g. "how do I share the codebase with a designer?")
- updating the guidelines when you learn something new on a project

Treat the contents as a **starting point, not a rulebook**. AI tooling moves fast — verify against today's best practices before applying.

## Starting a new project

→ **[START-HERE.md](START-HERE.md)** — paste one prompt into Claude Code. Zero setup.

## Playbook (what Claude walks through)

1. [Pick the stack](playbook/01-pick-stack.md) — 5-question wizard (type → CMS → tech stack → name → hosting)
2. [Scaffold the project](playbook/02-scaffold.md)
3. [Set up AI](playbook/03-setup-ai.md)
4. [Design handoff](playbook/04-design-handoff.md) *(stub)*
5. [Build features with AI](playbook/05-build-feature.md) *(stub)*
6. [Code review with AI](playbook/06-review.md) *(stub)*
7. [Deploy](playbook/07-deploy.md) *(stub)*

## Reference

- [stack.md](reference/stack.md) — Framework comparison (Astro / Next.js / Webflow).
- [cms.md](reference/cms.md) — CMS comparison + defaults per framework.
- [tech-stack.md](reference/tech-stack.md) — Toolbox (package manager, styling, lint, etc.) + the Default bundle.
- [deployment.md](reference/deployment.md) — Vercel default, CloudFront alternative, Cloudflare Pages, Webflow.
- [scaffold.md](reference/scaffold.md) — Folder conventions per project type.

## Templates

- [AGENTS.md](templates/AGENTS.md) — Drop-in template for the new project's `AGENTS.md`.

## In progress

- [todo.md](todo.md) — Open items across the wizard, scaffold, references, and playbook stubs.

## Contributing back

Learn something during a project that future projects would benefit from? Add it here. Keep entries compact — link out for depth rather than inlining.

> **Note:** this repo must be **public on GitHub** for the one-paste setup to work. See [START-HERE.md](START-HERE.md#for-maintainers).
