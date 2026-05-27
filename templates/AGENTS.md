# NOTE:

This is initial draft taken from Muro - worth to templatize this so it easier to pull into any new project.
Todo:

- [] add prompt to README.md on how to pull this into new projects
- [] clear if anything is muro-specific
- [] add more sections: "ask AI to document larger features, eg. how animations are being built"

<!-- BEGIN:nextjs-agent-rules -->

# This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` before writing any code. Heed deprecation notices.

<!-- END:nextjs-agent-rules -->

# muro marketing site

## Stack

- Next.js 16 (App Router, Turbopack)
- React 19
- Tailwind 4 — `@import "tailwindcss"` and `@theme inline` in `app/globals.css`. No `tailwind.config.*`.
- MDX content via `next-mdx-remote` + `gray-matter` (`content/blog/`, `content/legal/`)
- TypeScript, ESLint

## Commands

```bash
npm run dev
npm run build
npm run lint
```

## Project structure

```
app/           # Route segments + root layout (html/body/fonts only)
components/    # Shared React components
  text/        # Text, Heading typography
  ui/          # Section, Container primitives (PascalCase.tsx)
config/        # Site config (nav, footer links)
content/       # MDX source files
  blog/
  legal/
layouts/       # MainLayout, Navbar, Footer
sections/      # Page sections (compose Section + Container inside)
lib/           # Utilities (cn, blog, legal, format)
public/        # Static assets
```

Import via `@/` alias. Do not use `../` across top-level folders.

## How pages are built

```
page
└── MainLayout          # navbar + <main> + footer
    └── sections        # named section components
        └── Section     # full-bleed band (100vw)
            └── Container   # max-width column + padding
                └── content
```

- **Pages** (`app/.../page.tsx`) — compose `MainLayout` + sections only. No layout logic in pages.
- **Root layout** (`app/layout.tsx`) — html, body, fonts, global CSS only.
- **Sections** (`sections/`) — one block per page region; always wrap content in `Section` then `Container`.
- **Config** (`config/site.ts`) — site name, nav, footer links.

## Brand & design system

Tokens in `app/globals.css` (`:root` + `@theme inline`). Extend tokens before adding arbitrary Tailwind values.

| Token                 | Tailwind                 | Usage           |
| --------------------- | ------------------------ | --------------- |
| `--background`        | `bg-background`          | Page background |
| `--foreground`        | `text-foreground`        | Primary text    |
| `--foreground-muted`  | `text-foreground-muted`  | Secondary copy  |
| `--foreground-subtle` | `text-foreground-subtle` | Captions, meta  |

**Typography:** Use `Text` and `Heading` from `components/text/`. Body sizes: `xsmall` … `xxxlarge`. Heading sizes: `medium`, `regular`, `large`, `xlarge`. One `h1` per page.

**Spacing:** `px-container`, `py-section`, `py-compact`, `py-footer`, `max-w-content`, `gap-container`, `gap-section`, `mt-stack-*` / `mb-stack-*` / `pb-stack-*`, `p-container` — defined as `@utility` in `globals.css`. Prefer these over raw `p-4`, `gap-6`, `mt-2`, etc.

## Conventions

- Prefer Server Components; `'use client'` only when needed.
- Tailwind: use design tokens from `@theme` in `globals.css` — no arbitrary values like `text-[#333]`.
- Typography and spacing via `Text` / `Heading` and layout utilities — not raw `text-lg` / `p-4` unless no token exists.
- No inline `style={...}` unless unavoidable (CSS variables for animation, etc.).
- File naming: PascalCase for components (`Section.tsx`, `HomeIntroSection.tsx`). Hooks: `useThing.ts`. Config/modules: lowercase (`site.ts`, `blog.ts`).

## AI code review (`/review`)

When asked to review or `/review` is triggered:

### 1. Gather context

```bash
git diff main...HEAD
git log main...HEAD --oneline
```

Use a different base branch if specified instead of `main`.

### 2. Review checklist

**Code quality** — clear naming; no dead code, commented blocks, or debug logs; no unnecessary complexity; reuse existing logic where possible.

**TypeScript** — no implicit `any`; no unjustified `as` assertions; sensible generics; Zod aligned with types when used.

**React / Next.js** — no unnecessary `'use client'`; correct list `key`s; memoization only where it matters; dynamic import for heavy client bundles.

**Tailwind** — design token classes only (no arbitrary values); no inline `style` unless justified; no redundant class stacks.

**Performance** — images via `next/image` with dimensions; avoid large client bundles; tree-shake heavy deps.

**Security** — no secrets in code; sanitize user input; auth checks where needed; avoid unsafe `dangerouslySetInnerHTML`.

### 3. Output format

- 2–3 sentence summary of what changed.
- Issues by severity: 🔴 Critical · 🟡 Warning · 🟢 Suggestion (file + line, problem, fix).
- Verdict: **Approve** / **Approve with suggestions** / **Needs changes**.

## Documenting new features

After a non-trivial feature ships, update this file (or add `docs/specs/<feature>.md` and link it here).

**Add under a `## Features` heading:** routes, new sections, content paths, new tokens, and one-line gotchas.

**Close-the-loop prompt:**

> Update `AGENTS.md` for {{feature}}: routes, sections, tokens, gotchas. Link `docs/specs/{{feature}}.md` if present. Do not remove existing rules.

See `docs/AI-WORKFLOW.md` for Figma → spec → code and SDD guidance.

## Features

| Route                | Sections                               | Notes                                        |
| -------------------- | -------------------------------------- | -------------------------------------------- |
| `/`                  | `HomeIntroSection`                     | One `h1` in intro                            |
| `/blog`              | `BlogHeaderSection`, `BlogListSection` | List `h1` in header                          |
| `/blog/[slug]`       | `BlogPostSection`                      | Post `h1` in header; MDX `#` renders as `h2` |
| `/terms`, `/privacy` | `LegalDocumentSection`                 | Same MDX heading rule as blog posts          |

MDX maps `h1` → `Heading as="h2"` so pages keep a single document `h1`.

## Related docs

- `CLAUDE.md` — Claude-specific behavior (`@AGENTS.md`)
- `docs/AI-WORKFLOW.md` — design handoff, prompting, SDD tiers
- `templates/` — reusable `AGENTS.template.md` / `CLAUDE.template.md` for new projects
