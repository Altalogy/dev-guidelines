---
title: "Tech Stack Toolbox (2026)"
description: "Useful libraries and tools we reach for, plus the 'Default bundle' the wizard suggests."
updatedAt: "2026-06-02"
reviewedAt: "2026-06-02"
tags: ["tooling", "default-bundle", "package-manager", "tailwind", "biome", "typescript"]
---

# Tech Stack Toolbox (2026)

> **Scope:** Tools that sit on top of the framework choice (Next.js / Astro / etc.). Not the framework itself — see [stack.md](stack.md) and [cms.md](cms.md) for those.

---

## Default bundle

When the user picks "Default" in the wizard's tech-stack question, this is what they get. Single set, sane choices, optimized for our common project shape (Next.js or Astro website with a small team).

| Layer | Default | Notes |
| --- | --- | --- |
| **Language** | TypeScript | Strict mode. No JS-only projects. |
| **Package manager** | pnpm | Faster installs, strict node_modules, monorepo-ready. |
| **Styling** | Tailwind 4 | `@import "tailwindcss"` + `@theme inline` in `globals.css`. No `tailwind.config.*`. |
| **Lint + format** | Biome | Single tool, fast. *(Trial — fall back to ESLint + Prettier if a project hits a Biome gap.)* |
| **Type checking** | `tsc --noEmit` in CI | Plus IDE live errors. |
| **Testing — unit** | Vitest | *(Default for Next.js and Astro. TBD: when to include by default vs add on demand — see [todo.md](../todo.md).)* |
| **Testing — e2e** | Playwright | *(Add on demand, not in baseline.)* |
| **Validation** | Zod | Schema-first. Used at API boundaries and content collections. |
| **Git hooks** | Husky + lint-staged | Pre-commit lint/format. *(TBD baseline — [todo.md](../todo.md).)* |
| **CI** | GitHub Actions | Lint, typecheck, build on PR. *(TBD baseline workflow.)* |

> The "Default bundle" is intentionally small. Don't add things "for completeness" — add when a project needs them.

---

## Toolbox — pick when "Customize"

### Package manager

| Option | When | Watch |
| --- | --- | --- |
| **pnpm** *(default)* | Almost always | Strict resolution can surprise people coming from npm |
| **npm** | Client requires it, or aligning with an existing repo | Slower, looser dep resolution |
| **bun** | Greenfield, want speed, OK with a younger ecosystem | Some packages still have edge cases on Bun |

### Styling

| Option | When | Watch |
| --- | --- | --- |
| **Tailwind 4** *(default)* | Almost always for our work | New CSS-first config (no `tailwind.config.*`) |
| **Vanilla CSS / CSS Modules** | Tiny site, strong preference, designer-led | Loses utility velocity |
| **CSS-in-JS** (styled-components, Emotion) | Rare — only if matching an existing codebase | Server Components friction in Next.js App Router |
| **UnoCSS** | Astro-heavy, want atomic CSS without Tailwind | Smaller community |

### Lint + format

| Option | When | Watch |
| --- | --- | --- |
| **Biome** *(default trial)* | Greenfield, want one tool | Plugin ecosystem smaller than ESLint |
| **ESLint + Prettier** | Project needs ESLint plugins Biome doesn't cover yet | Two tools, slower, more config |

> Decision still in trial — see [todo.md](../todo.md).

### Type checking

- **TypeScript strict** is always on. No exceptions.
- `tsc --noEmit` runs in CI even when Biome handles lint, because they catch different things.

### Testing

| Option | Layer | Default? |
| --- | --- | --- |
| **Vitest** | Unit / integration | Yes — included in default bundle for Next.js/Astro |
| **Playwright** | E2E | On demand |
| **Storybook** | Component dev | On demand — useful when component count grows |
| **MSW** | Network mocking for tests | On demand |

### Validation / schema

- **Zod** — default for runtime validation. Pairs with TypeScript.
- **Valibot** — lighter alternative; consider when bundle size matters.

### Content / data

- **Astro content collections** — for Astro + MDX.
- **`@next/mdx`** — for Next.js MDX. (Note: `next-mdx-remote` is archived — see [stack.md](stack.md#6-gotchas-to-know).)
- **gray-matter** — frontmatter parsing when not using a typed collection.

### Forms

- **React Hook Form** + **Zod resolver** — default for Next.js.
- **Astro form actions** — for Astro.
- **Formspree** / **Basin** / **CF Pages Functions** — submission backends.

### State (client)

- **Zustand** — small, focused client state.
- **TanStack Query** — server state / caching.
- Avoid Redux for new projects unless matching an existing codebase.

### Analytics

- **Plausible** / **Umami** / **Cloudflare Web Analytics** — pick by hosting and budget. Skip GA unless required.

### Email / transactional

- **Resend** — default. Clean API, generous free tier.

### Database / ORM *(when project goes beyond static)*

- **Drizzle** — TypeScript-first, default for new projects with a DB.
- **Prisma** — when matching an existing codebase.
- **PostgreSQL** — default. Supabase / Neon / RDS depending on hosting.

### Auth *(when project goes beyond static)*

- **Auth.js (NextAuth)** — default for Next.js.
- **Clerk** — when speed-to-market matters and budget allows.
- **Better Auth** — newer, worth a look for greenfield TS-first projects.

---

## Open items

Tracked in [../todo.md](../todo.md):

- Lock the "Default bundle" specifics (Biome vs ESLint+Prettier; Vitest in baseline yes/no).
- Settle Husky + lint-staged baseline config.
- Standardize the GitHub Actions starter workflow.
- Decide testing posture per project type (prototype vs website vs tool).

---

## AI sanity check

> Reviewed June 2, 2026 (Claude Opus 4.7)

pnpm + Tailwind 4 + TypeScript-strict + Zod are uncontested defaults right now. Biome-as-default is the live question — it's fast and one tool, but ESLint's plugin ecosystem (Next.js, React hooks, a11y) is still richer. Trial Biome on the next 2-3 projects and re-decide. Re-review Q4 2026.
