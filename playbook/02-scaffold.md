# 2. Scaffold the project

**Goal:** a working repo with the chosen stack — folders in place, libraries installed, builds locally. By the end of this step the project runs; AI tooling and design handoff come in steps 3 and 4.

Inputs from [01-pick-stack.md](01-pick-stack.md): project type, CMS, tech stack, name, hosting.

## Actions

### 1. Create the repo

- Initialize a git repo locally.
- Create the GitHub repo (gh CLI or web). Push `main`.
- Add a baseline `.gitignore` for the chosen stack.
- Add `.editorconfig`.

> Designer path: walk through `gh repo create` step by step, or do it in the GitHub web UI.

### 2. Run the framework scaffold

Based on Q1 from the wizard:

| Project type | Command |
| --- | --- |
| Website — Next.js | `pnpm create next-app@latest` |
| Website — Astro | `pnpm create astro@latest` |
| Website — Webflow | No code scaffold — create handoff folder structure (see scaffold ref) |
| Prototype — Next.js | `pnpm create next-app@latest` *(minimal template)* |
| Prototype — HTML/CSS/JS | Manual scaffold *(plan TBD — see [../todo.md](../todo.md))* |
| Tool | `pnpm init` + framework-specific bootstrap |

After the scaffold runs, reorganize to match [reference/scaffold.md](../reference/scaffold.md). Don't blindly accept the `create` output — move files into our folder conventions (`sections/`, `layouts/`, `components/text/`, `components/ui/`, etc.) before adding any code.

### 3. Install the tech stack

From Q3 (Default bundle or customized):

```bash
# Default bundle (Next.js example)
pnpm add -D typescript @types/node @types/react
pnpm add -D @biomejs/biome
pnpm add tailwindcss@latest
pnpm add zod
# Vitest if included in baseline:
pnpm add -D vitest
```

See [reference/tech-stack.md](../reference/tech-stack.md) for the full list and rationale.

CMS-specific installs (from Q2) — only when applicable:

- **Strapi** — set up Strapi separately (its own repo or workspace). Add `lib/strapi.ts` typed client.
- **Sanity** — `pnpm dlx sanity@latest init` for the studio.
- **Payload** — install in-repo (`pnpm add payload`).
- **MDX** — `pnpm add @next/mdx` + config in `next.config.ts`.

### 4. Configure baseline

- `tsconfig.json` — strict mode, `@/*` path alias.
- Tailwind 4 — `@import "tailwindcss"` and `@theme inline` in `app/globals.css`. No `tailwind.config.*`.
- Biome — `biome.json` with our default rules. *(Config still being trialed — see [../todo.md](../todo.md).)*
- Scripts in `package.json`: `dev`, `build`, `lint`, `typecheck`, optionally `test`.

### 5. Static code analysis + linters *(stubbed)*

> This step is intentionally stubbed for now. Tracked in [../todo.md](../todo.md):
>
> - Biome vs ESLint + Prettier — final call after a few projects.
> - Husky + lint-staged baseline config.
> - `tsc --noEmit` in CI.
> - GitHub Actions workflow template (lint, typecheck, build).
>
> Until those land: install Biome with the default config, add `lint` and `format` scripts, and **flag in the project's `AGENTS.md` that linter setup is a known TODO**.

### 6. First build + smoke run

```bash
pnpm dev      # confirm it starts
pnpm build    # confirm it builds clean
pnpm lint     # confirm lint passes
```

If anything fails, fix before moving on. Don't ship a broken scaffold to step 3.

### 7. Hosting connection *(if Q5 = Vercel or Cloudflare Pages)*

Don't deploy yet — just connect the repo so previews work as soon as we push real code.

- **Vercel** — connect via dashboard or `vercel link`. Framework preset auto-detected.
- **Cloudflare Pages** — connect via dashboard. Set build command + output directory.
- **AWS / CloudFront** — defer to step 7 ([07-deploy.md](07-deploy.md)); requires more setup.

See [reference/deployment.md](../reference/deployment.md).

## External actions

- **GitHub repo creation** — if the user doesn't have org access, give them a message to send to the org admin.
- **Vercel / Cloudflare account** — if the user isn't on the team, send them an invite request template.

## Output

A repo on `main` that:

- Matches the folder conventions in [reference/scaffold.md](../reference/scaffold.md)
- Builds cleanly (`pnpm build`)
- Lints cleanly (`pnpm lint`)
- Is connected to the chosen hosting (preview URLs working — or noted as a step-7 task for AWS)

Open TODOs (linter baseline, CI workflow, testing posture) noted in the project's local todo so they don't get lost.

## Compile into the project

Not yet — happens in step 3.

## Open items

See [../todo.md](../todo.md):

- Lock the linter / static analysis baseline.
- GitHub Actions template.
- Husky + lint-staged baseline.
- Per-stack starter scaffolds (do we maintain templates, or rely on `create-*`?).

Next: [03-setup-ai.md](03-setup-ai.md).
