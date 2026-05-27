# 2. Scaffold the project

**Goal:** a working repo with the chosen stack — installed, building, deployed to a preview URL.

## Decisions

- **Package manager:** npm / pnpm / bun  *(TBD — pick a default)*
- **TypeScript:** yes
- **Linting / formatting:** ESLint + Prettier, or Biome  *(TBD)*
- **Git host:** GitHub

## Steps (TBD — to be filled in as we standardize)

- [ ] Create the GitHub repo
- [ ] Run the framework's `create` command (`npm create astro@latest`, `npx create-next-app`, …)
- [ ] Add Tailwind / styling baseline
- [ ] Configure TypeScript paths (`@/*` alias)
- [ ] Add lint + format scripts
- [ ] Set up Git hooks (pre-commit lint/format)
- [ ] First deploy to a preview URL

## Open questions

- Do we want a starter repo per stack (Astro starter, Next.js starter) instead of `create` scripts?
- Standardize on Biome or ESLint+Prettier?
- Which Husky / lint-staged baseline?

## Output

Repo on `main` that builds, deploys to a preview URL, and is ready for [03-setup-ai.md](03-setup-ai.md).
