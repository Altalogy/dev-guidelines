# Dev Guidelines

Internal wiki for tech stack choices, project setup, AI workflows, and conventions.

## How this works

This repo is a long-term **wiki**. When you start a new project, Claude Code reads the playbook directly from GitHub (no clone required) and **compiles what's needed into the new project** (`AGENTS.md`, optionally a linked `guidelines.md`). After setup, the new project is self-contained — you don't need to keep looking back. Return here for:

- generic, cross-project aid (e.g. "how do I share the codebase with a designer?")
- updating the guidelines when you learn something new on a project

Treat the contents as a **starting point, not a rulebook**. AI tooling moves fast — verify against today's best practices before applying.

## Starting a new project

→ **[START-HERE.md](START-HERE.md)** — paste one prompt into Claude Code. Zero setup.

## Playbook (what Claude walks through)

1. [Pick the stack](playbook/01-pick-stack.md)
2. [Scaffold the project](playbook/02-scaffold.md) *(stub)*
3. [Set up AI](playbook/03-setup-ai.md)
4. [Design handoff](playbook/04-design-handoff.md) *(stub)*
5. [Build features with AI](playbook/05-build-feature.md) *(stub)*
6. [Code review with AI](playbook/06-review.md) *(stub)*
7. [Deploy](playbook/07-deploy.md) *(stub)*

## Reference

- [stack.md](reference/stack.md) — Web stack comparison for landing pages + blog.

## Templates

- [AGENTS.md](templates/AGENTS.md) — Drop-in template for the new project's `AGENTS.md`.

## Contributing back

Learn something during a project that future projects would benefit from? Add it here. Keep entries compact — link out for depth rather than inlining.

> **Note:** this repo must be **public on GitHub** for the one-paste setup to work. See [START-HERE.md](START-HERE.md#for-maintainers).
