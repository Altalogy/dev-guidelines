# 1. Pick the stack

**Goal:** decide framework, content source, and hosting before writing any code.

## Ask the user

- What kind of site is this? (marketing site, blog, app, prototype)
- Will non-devs edit content? How often?
- Will it grow into an app, or stay a content site?
- Does the client already use a stack in other projects? *(matching usually wins)*
- Any constraint on hosting (existing Vercel/Cloudflare org, billing setup)?

## Decide together

A stack is three independent choices — confirm each:

1. **Framework** — Astro / Next.js / Webflow
2. **Content source** — MDX in repo / headless CMS / none
3. **Hosting** — Cloudflare Pages / Vercel / Webflow

See [reference/stack.md](../reference/stack.md) for the full comparison and decision heuristics.

## Quick defaults

- Marketing site + blog → **Astro + MDX + Cloudflare Pages**
- Non-dev edits content → **Astro + Storyblok/Sanity + Cloudflare Pages**
- Will grow into an app → **Next.js + Payload/Sanity + Vercel**
- Designer-led, no dev capacity → **Webflow**

## Actions

**Dev:** confirm the three choices with the user. No commands run yet.

**Designer:** if unsure, take the matching quick default above. **Astro + MDX + Cloudflare Pages** is the safest default for marketing-style work.

## External actions

None at this step.

## Output

Chosen stack noted somewhere (Claude's working memory or scratch file). It will land in `AGENTS.md` and the new project's `README.md` in step 3.

## Compile into the project

Not yet — captured in step 3 ([Set up AI](03-setup-ai.md)).

Next: [02-scaffold.md](02-scaffold.md).
