# 6. Code review with AI

**Goal:** catch issues before merge using Claude as a first-pass reviewer.

## Current approach

The `/review` checklist lives in [`templates/AGENTS.md`](../templates/AGENTS.md) under "AI code review (`/review`)". It covers code quality, TypeScript, React/Next.js, Tailwind, performance, and security, and outputs a verdict (Approve / Approve with suggestions / Needs changes).

## To be filled in

- **`/review` vs `/ultrareview`** — when to reach for the cloud multi-agent review
- **PR conventions** — title, body, screenshots, test plan
- **Handling false positives** — how to push back on AI review noise
- **Human review handoff** — what AI catches vs what still needs a person

## Open questions

- Should `/review` always run before opening a PR, or only before merge?
- Do we standardize a PR template that mirrors the `/review` output sections?

Next: [07-deploy.md](07-deploy.md).
