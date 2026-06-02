# 1. Pick the stack (wizard)

**Goal:** lock in project type, CMS, tech stack, name, and hosting — in **five short questions**. Skip questions whose answer is determined by an earlier one. Always offer a sensible default + an escape hatch ("decide later").

## Principle

The old flow asked many open questions up front. Users almost always know what they want. So:

1. Lead with the **highest-signal** question (project type).
2. Branch follow-ups conditionally — don't ask about CMS for Webflow, don't ask about hosting for a CLI tool.
3. Offer a **Default** option in every multi-choice question. The user should be able to take the defaults end-to-end and get a sensible scaffold.
4. Offer a **Skip — decide later** option where the decision can wait without blocking scaffolding (flag it in `AGENTS.md` and the project's todo).

---

## Question 1 — Project type

> "What kind of project are we starting?"

1. **Website — Next.js** *(with or without CMS — asked next)*
2. **Website — Astro**
3. **Website — Webflow**
4. **Prototype — Next.js**
5. **Prototype — plain HTML/CSS/JS** *(handoff path: Webflow)*
6. **Tool** *(e.g. asset generation, internal utility)*
7. **Help me decide**

Routing:

| Answer | Next |
| --- | --- |
| 1 (Next.js website) | Q2 (CMS) |
| 2 (Astro) | CMS auto = **inbuilt MDX** → skip to Q3 |
| 3 (Webflow) | CMS auto = **Webflow CMS** → skip to Q3 |
| 4 (Prototype — Next.js) | No CMS → skip to Q3 |
| 5 (Prototype — HTML/CSS/JS) | No CMS → skip to Q3 |
| 6 (Tool) | No CMS → skip to Q3 |
| 7 (Help me decide) | Enter "Help me decide" branch (below), then loop back to Q1 |

### "Help me decide" branch

Stubbed — to be improved over time. For now ask:

- **Purpose?** (ship a marketing site, validate an idea, internal tool, design experiment, client deliverable)
- **For whom?** (dev / designer / internal team / external client / yourself)
- **Lifespan?** (one-off prototype / months / years)
- **Who will edit content?** (devs / marketers / nobody)

Map answers to one of options 1-6 (rules to formalize — see [../todo.md](../todo.md)), confirm with the user, then continue from Q2.

---

## Question 2 — CMS *(conditional)*

Triggered **only** by Q1 = 1 (Next.js website). Auto-set otherwise.

> "What's the content source?"

- **Strapi** *(default)* — self-hosted, predictable bill, plugins cover most cases
- **MDX in repo** — devs write content, Git-versioned
- **Sanity** — editorial team, real-time, complex schemas
- **Storyblok** — marketing team, visual editor
- **Payload** — TypeScript-native, self-hostable
- **Skip — decide later** — scaffold without a CMS; flag in `AGENTS.md` and the project todo

See [reference/cms.md](../reference/cms.md) for the comparison and heuristics.

---

## Question 3 — Tech stack

> "Pick the toolchain — or take the default bundle."

- **Default bundle** *(recommended)* — pnpm + TypeScript-strict + Tailwind 4 + Biome + Vitest + Zod. See [reference/tech-stack.md](../reference/tech-stack.md).
- **Customize** — confirm each layer in turn:
  - Package manager (default **pnpm**; alt: npm, bun)
  - Styling (default **Tailwind 4**; alt: vanilla CSS, CSS Modules, UnoCSS)
  - Lint + format (default **Biome**; alt: ESLint + Prettier)
  - Unit tests (default **Vitest**; or none in baseline)
  - Extras: Playwright, Storybook, Drizzle, Auth.js — add on demand

See [reference/tech-stack.md](../reference/tech-stack.md) for the full toolbox.

---

## Question 4 — Project identity

> "What's the project called?" *(required)*
> "One-sentence description?" *(optional)*

These land in `package.json`, `README.md`, and `AGENTS.md`.

Naming: kebab-case for the repo / package name (`acme-marketing`). Display name can be free-form ("Acme Marketing Site").

---

## Question 5 — Hosting

> "Where will this deploy?"

- **Vercel** *(default for Next.js)*
- **Cloudflare Pages** *(default for Astro / static)*
- **AWS (CloudFront + S3)** — alternative when client requires AWS
- **Webflow Hosting** *(auto when Q1 = 3)*
- **Skip — decide later**

Defaults applied based on Q1:

| Q1 | Default hosting |
| --- | --- |
| 1, 4 (Next.js) | Vercel |
| 2 (Astro) | Cloudflare Pages |
| 3 (Webflow) | Webflow Hosting (auto) |
| 5 (HTML/CSS/JS) | Cloudflare Pages |
| 6 (Tool — web) | Vercel |
| 6 (Tool — CLI) | npm (not hosting) |

See [reference/deployment.md](../reference/deployment.md).

---

## Confirm summary

Echo all five answers back as a single block before continuing:

```
Type:       Website — Next.js
CMS:        Strapi
Stack:      Default bundle (pnpm + Tailwind 4 + Biome + Vitest + TypeScript)
Name:       acme-marketing  ("Acme Marketing Site")
Desc:       Landing page + blog for Acme.
Hosting:    Vercel
```

User confirms (or amends a single line) → continue to [02-scaffold.md](02-scaffold.md).

---

## Output

The five answers, captured as working state. They drive:

- The scaffold commands and folder layout in step 2
- The `AGENTS.md` content in step 3
- The `README.md` `## Stack` section in step 3
- The deploy walkthrough in step 7

## Compile into the project

Not yet — captured at the end of step 3 ([03-setup-ai.md](03-setup-ai.md)).

## Open items

See [../todo.md](../todo.md):

- Formalize the "Help me decide" mapping rules.
- Lock the Default bundle specifics (Biome trial, Vitest in baseline).
- Flesh out the Prototype HTML/CSS/JS and Tool paths.

Next: [02-scaffold.md](02-scaffold.md).
