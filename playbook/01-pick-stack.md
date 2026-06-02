# 1. Pick the stack (wizard)

**Goal:** lock in project type, CMS, tech stack, name, and hosting — in **five short questions**. Skip questions whose answer is determined by an earlier one. Always offer a sensible default + an escape hatch ("decide later").

## Principle

The old flow asked many open questions up front. Users almost always know what they want. So:

1. Lead with the **highest-signal** question (project type).
2. Branch follow-ups conditionally — don't ask about CMS for Webflow, don't ask about hosting for a CLI tool.
3. Offer a **Default** option in every multi-choice question. The user should be able to take the defaults end-to-end and get a sensible scaffold.
4. Offer a **Skip — decide later** option where the decision can wait without blocking scaffolding (flag it in `AGENTS.md` and the project's todo).

## UI constraint

Claude Code's `AskUserQuestion` tool **caps options at 4** (plus an auto-added "Other"). Every question below stays within that cap. When a logical question would have more than 4 options, split it into a category + subtype pair (see Q1 → Q1a / Q1b).

---

## Question 1 — Project category

> "What kind of project are we starting?"

1. **Website**
2. **Prototype**
3. **Tool** *(e.g. asset generation, internal utility)*
4. **Help me decide**

Routing:

| Answer | Next |
| --- | --- |
| 1 (Website) | Q1a (framework) |
| 2 (Prototype) | Q1b (framework) |
| 3 (Tool) | Skip to Q3 (no CMS, no framework choice yet) |
| 4 (Help me decide) | "Help me decide" branch (below) → loop back to Q1 |

### Question 1a — Website framework *(only if Q1 = 1)*

> "Which framework?"

1. **Next.js** → continue to Q2 (CMS)
2. **Astro** → CMS auto = **inbuilt MDX** → skip to Q3
3. **Webflow** → CMS auto = **Webflow CMS** → skip to Q3

### Question 1b — Prototype framework *(only if Q1 = 2)*

> "Which prototype shape?"

1. **Next.js** → no CMS, skip to Q3
2. **Plain HTML/CSS/JS** *(handoff path: Webflow)* → no CMS, skip to Q3

### "Help me decide" branch

Stubbed — to be improved over time. For now ask:

- **Purpose?** (ship a marketing site, validate an idea, internal tool, design experiment, client deliverable)
- **For whom?** (dev / designer / internal team / external client / yourself)
- **Lifespan?** (one-off prototype / months / years)
- **Who will edit content?** (devs / marketers / nobody)

Map answers to one of options 1-6 (rules to formalize — see [../todo.md](../todo.md)), confirm with the user, then continue from Q2.

---

## Question 2 — CMS *(conditional)*

Triggered **only** by Q1a = 1 (Next.js website). Auto-set otherwise.

> "What's the content source?"

1. **Strapi** *(default)* — self-hosted, predictable bill, plugins cover most cases
2. **MDX in repo** — devs write content, Git-versioned
3. **Other hosted CMS** — drill in (Q2a)
4. **Skip — decide later** — scaffold without a CMS; flag in `AGENTS.md` and the project todo

### Question 2a — Hosted CMS *(only if Q2 = 3)*

> "Which hosted CMS?"

1. **Sanity** — editorial team, real-time, complex schemas
2. **Storyblok** — marketing team, visual editor
3. **Payload** — TypeScript-native, self-hostable

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

Skipped entirely when Q1a = Webflow (auto-set to Webflow Hosting) or Q1 = Tool + CLI (ships via npm, not hosting).

1. **Vercel** *(default for Next.js)*
2. **Cloudflare Pages** *(default for Astro / static)*
3. **AWS (CloudFront + S3)** — alternative when client requires AWS
4. **Skip — decide later**

Defaults applied based on project type:

| Project type | Default hosting |
| --- | --- |
| Website / Prototype — Next.js | Vercel |
| Website — Astro | Cloudflare Pages |
| Website — Webflow | Webflow Hosting (auto, skip Q5) |
| Prototype — HTML/CSS/JS | Cloudflare Pages |
| Tool — web | Vercel |
| Tool — CLI | npm (auto, skip Q5) |

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
