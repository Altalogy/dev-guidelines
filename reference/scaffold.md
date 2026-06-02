---
title: "Project Scaffold Conventions (2026)"
description: "Folder layouts and starter files per project type. What Claude creates after the wizard."
updatedAt: "2026-06-02"
reviewedAt: "2026-06-02"
tags: ["scaffold", "folder-structure", "nextjs", "astro", "prototype", "tool"]
---

# Project Scaffold Conventions (2026)

> **Scope:** Folder structure and starter files Claude creates after the wizard locks the answers. One section per project type.

The goal is **boring, predictable layouts** — any teammate (or future Claude session) can drop into any project and know where things live.

---

## Common to every project

These files exist in every scaffold, regardless of type:

```
.
├── AGENTS.md              # Claude rules for this project
├── CLAUDE.md              # Single line: @AGENTS.md
├── README.md              # Stack section + how to run
├── .gitignore
├── .editorconfig
├── package.json
└── .github/
    └── workflows/
        └── ci.yml         # Lint + typecheck + build
```

---

## Website — Next.js

> Mirrors [templates/AGENTS.md](../templates/AGENTS.md), which was extracted from a real Next.js project.

```
.
├── app/                   # Route segments + root layout (html/body/fonts only)
├── components/            # Shared React components
│   ├── text/              # Text, Heading typography
│   └── ui/                # Section, Container primitives (PascalCase.tsx)
├── config/                # Site config (nav, footer links)
├── content/               # MDX source files (if CMS = MDX)
│   ├── blog/
│   └── legal/
├── layouts/               # MainLayout, Navbar, Footer
├── sections/              # Page sections (compose Section + Container)
├── lib/                   # Utilities (cn, blog, legal, format)
├── public/                # Static assets
├── docs/
│   └── specs/             # Feature specs (per 04-design-handoff.md)
└── (top-level files)
```

**Import alias:** `@/` → repo root. No `../` across top-level folders.

**Page composition:**

```
page
└── MainLayout          # navbar + <main> + footer
    └── sections        # named section components
        └── Section     # full-bleed band (100vw)
            └── Container   # max-width column + padding
```

**CMS-specific additions:**

- **Strapi** — add `lib/strapi.ts` (typed client), `.env.local` with `STRAPI_URL` + `STRAPI_TOKEN`.
- **Sanity** — add `sanity/` (studio config) + `lib/sanity.ts`.
- **Payload** — Payload lives in-repo; add `payload.config.ts` + `collections/`.
- **MDX** — `content/` directory as above; `@next/mdx` config in `next.config.ts`.

---

## Website — Astro

```
.
├── src/
│   ├── components/        # .astro components
│   ├── content/           # Content collections (typed)
│   │   ├── blog/
│   │   └── config.ts      # Zod schemas
│   ├── layouts/
│   ├── pages/             # Routes (.astro and .mdx)
│   └── styles/
│       └── global.css     # Tailwind imports + tokens
├── public/                # Static assets
├── astro.config.mjs
└── (top-level files)
```

**Content collections** are the default content source. Define schemas in `src/content/config.ts` with Zod.

---

## Website — Webflow

Webflow projects don't have a code repo in the same shape. Instead the project root holds **handoff artifacts**:

```
.
├── README.md              # Webflow project URL, editor seats, custom code map
├── custom-code/
│   ├── head.html          # Embeds, fonts, analytics
│   └── body.html          # Pre-</body> scripts
├── assets/                # Source files exported from Figma
├── docs/
│   ├── design-system.md   # Tokens, components, naming
│   └── content-model.md   # CMS collections, fields, references
└── AGENTS.md              # Claude rules (mostly design-handoff focus)
```

> Stubbed — fill in as Webflow projects come through. See [../todo.md](../todo.md).

---

## Prototype — Next.js

Same shape as Website — Next.js, with the following differences:

- **No CMS.** Mock content in `content/mock.ts` or inline.
- **No `docs/specs/`** — prototypes are exploratory.
- **`README.md`** explicitly labels this as a prototype + sunset criteria.
- Looser conventions — okay to inline styles, skip Section/Container hierarchy.

> Decision: do prototypes share the Website — Next.js scaffold exactly, or diverge more aggressively? Tracked in [../todo.md](../todo.md).

---

## Prototype — plain HTML/CSS/JS *(Webflow handoff path)*

> **Next focus** — full plan to be written after the structural pass. See [../todo.md](../todo.md).

Sketch:

```
.
├── index.html
├── styles/
│   └── main.css
├── scripts/
│   └── main.js
├── assets/
│   ├── images/
│   └── fonts/
├── README.md              # How to preview locally; handoff notes for Webflow team
└── AGENTS.md
```

Open questions to settle in the dedicated plan:

- Build tool? (none / Vite / esbuild)
- Local preview? (`npx serve` / Vite dev server / live-server)
- How does the HTML/CSS map to Webflow components on handoff?
- Asset conventions matching Webflow's expectations.

---

## Tool

Generic shape — concrete defaults TBD per tool type.

```
.
├── src/                   # Source (TypeScript)
├── bin/                   # CLI entry (if applicable)
├── tests/
├── README.md              # What the tool does, how to run
├── package.json           # `bin` field for CLI tools
└── AGENTS.md
```

Open: CLI (commander / cleye) vs Electron vs web tool — each needs its own scaffold sketch. Tracked in [../todo.md](../todo.md).

---

## Naming conventions (all project types)

- **Components:** PascalCase (`Section.tsx`, `HomeIntroSection.tsx`).
- **Hooks:** `useThing.ts`.
- **Config / modules:** lowercase (`site.ts`, `blog.ts`).
- **Utilities:** lowercase, single responsibility per file (`lib/format.ts`, `lib/cn.ts`).
- **Routes:** match the framework's convention (Next.js `app/`, Astro `src/pages/`).

---

## Open items

Tracked in [../todo.md](../todo.md):

- Flesh out Webflow handoff scaffold from real project examples.
- Define the prototype HTML/CSS/JS plan (Webflow handoff path) — next focus.
- Define Tool scaffolds per sub-type (CLI / desktop / web tool).
- Decide whether prototypes diverge from website scaffolds or stay identical.

---

## AI sanity check

> Reviewed June 2, 2026 (Claude Opus 4.7)

Next.js scaffold is well-trodden from the Muro project. Astro scaffold is conventional and matches what `npm create astro` produces. The prototype HTML/CSS/JS path and Tool path are the most under-defined — flag them when picked in the wizard so Claude knows it's improvising. Re-review Q4 2026.
