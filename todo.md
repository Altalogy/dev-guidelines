# Todo

Running list of items that need further work. Anything stubbed in the playbook or reference files should land here so it doesn't get lost.

## Wizard (`playbook/01-pick-stack.md`)

- [ ] **"Help me decide" branch** — define the orienting questions (purpose, audience, lifespan, who edits content) and the rules that map answers back to one of the concrete options. Right now it's a freeform branch.
- [ ] **Prototype — plain HTML/CSS/JS path** — full plan for the Webflow-handoff prototype (folder layout, build tool, asset conventions, how the handoff actually works). *Next focus per Tom.*
- [ ] **Tool path** — define what "Tool" means in practice (CLI? Electron? web app for asset gen?) and pick a default scaffold.
- [ ] **Prototype — Next.js path** — confirm whether it shares the website-Next.js scaffold or diverges.

## Scaffold (`playbook/02-scaffold.md`)

- [ ] **Static code analysis / linter setup** — currently stubbed. Pick a baseline (Biome vs ESLint+Prettier), husky/lint-staged config, EditorConfig, `tsc --noEmit` in CI.
- [ ] **Testing baseline** — Vitest? Playwright? What ships in the "Default bundle"?
- [ ] **Git hooks** — pre-commit lint/format, commit-msg conventional commits?
- [ ] **CI baseline** — GitHub Actions workflow (lint, typecheck, build) — standardize once and template it.
- [ ] **Starter repos vs `create-*` scripts** — decide whether to maintain per-stack starters or always run framework scaffold commands.

## Reference docs

- [ ] **`reference/cms.md`** — periodic refresh (quarterly). Validate Strapi-as-default for Next.js still holds.
- [ ] **`reference/tech-stack.md`** — lock the "Default bundle" specifics. Currently lists candidates with TBDs.
- [ ] **`reference/deployment.md`** — flesh out CloudFront flow (S3 + CloudFront + ACM + Route 53 step-by-step). Add Cloudflare Pages section parity with Vercel.
- [ ] **`reference/scaffold.md`** — fill in per-stack folder conventions beyond Next.js (Astro, Webflow handoff, prototype, tool).
- [ ] **`reference/stack.md`** — already exists; cross-link with the new reference files and slim where it overlaps with `cms.md`.

## Playbook gaps

- [ ] **`03-setup-ai.md`** — keep; minor pass once defaults are locked.
- [ ] **`04-design-handoff.md`** — fill in. Figma → spec workflow, SDD tiers, Figma MCP usage, asset export.
- [ ] **`05-build-feature.md`** — fill in. Plan mode, subagents, tests, mid-flow review, close-the-loop AGENTS.md updates.
- [ ] **`06-review.md`** — `/review` vs `/ultrareview`, PR conventions, handling false positives.
- [ ] **`07-deploy.md`** — per-hosting steps for Vercel / Cloudflare Pages / Webflow / CloudFront.

## Meta

- [ ] **AGENTS.md template** — strip Muro-specific bits, make it stack-aware (different scaffolding per Next/Astro/etc.).
- [ ] **Slash command** — package the kickoff prompt as `/start-project` and document install steps.
- [ ] **Re-review cadence** — note in each reference doc when it was last reviewed; schedule quarterly sanity pass.
