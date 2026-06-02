---
title: "CMS Choice for Website Projects (2026)"
description: "How we pick a content source: defaults per framework, comparison table, decision heuristics."
updatedAt: "2026-06-02"
reviewedAt: "2026-06-02"
tags: ["cms", "strapi", "sanity", "storyblok", "payload", "mdx", "tina"]
---

# CMS Choice for Website Projects (2026)

> **Scope:** What backs the content layer of a website built with Next.js, Astro, or Webflow. Not a survey of every CMS — only the options we actually reach for.

A CMS choice has two questions:

1. **Who edits content?** (devs / marketers / designers / nobody)
2. **What ships the content?** (Git repo / hosted API / bundled editor)

Everything else (schema flexibility, pricing, hosting model) follows from those two answers.

---

## Defaults per framework

| Framework | Default CMS | Why |
| --- | --- | --- |
| **Next.js (website)** | **Strapi** | Self-hosted, predictable bill, plugins cover most cases. Switch when team needs Sanity-style real-time collab or Storyblok-style visual editing. |
| **Next.js (prototype)** | None | Prototypes don't need a CMS; mock content inline. |
| **Astro** | **Inbuilt MDX** (content collections) | Devs writing content. Type-safe, zero infra, Git-versioned. |
| **Webflow** | **Webflow CMS** | Bundled and locked. No choice to make. |

If the user picks a Next.js website and **isn't sure yet**, the wizard offers "Skip — decide later" and scaffolds without a CMS, with a flag in `AGENTS.md` and an entry in the project's todo.

---

## TL;DR table

| CMS | Best when | Hosting | Editor experience | Cost shape |
| --- | --- | --- | --- | --- |
| **Strapi** | Self-host, plugin needs, predictable cost | Self-host (Node) or Strapi Cloud | Admin panel, decent | OSS free + your infra; Cloud from ~$15/mo |
| **MDX in repo** | Devs write content | None — files in repo | Markdown / Git UI | Free |
| **Tina** | Devs + occasional non-dev edits | Git-backed (no separate DB) | Visual editor on top of MDX | Free tier; paid for orgs |
| **Sanity** | Editorial team, complex schemas, real-time | Hosted | Studio (best-in-class for structured content) | Free tier; scales with usage |
| **Storyblok** | Marketing teams, visual editing | Hosted | Visual editor (best-in-class for page-builder feel) | Free tier; scales with seats |
| **Payload** | TypeScript-first, full-control teams | Self-host (Node + DB) or Payload Cloud | Admin panel, modern | OSS free + your infra; Cloud paid |
| **Webflow CMS** | Webflow project | Webflow | Webflow Designer | Bundled with site plan |

---

## When to pick each

### Strapi *(Next.js default)*

- You want a real database-backed CMS without per-seat pricing.
- Self-hosting is OK (or you'll use Strapi Cloud).
- You'll want plugins (i18n, SEO, media library) without writing them yourself.
- Watch: maintenance burden is real — upgrades, DB migrations, hosting.

### MDX in repo

- Content lives next to code. Devs write it. Everyone reviews via PRs.
- Astro's content collections + Zod schemas give you type-safe queries.
- Doesn't scale to non-dev editors. Don't try to make it.

### Tina

- You want MDX-in-repo but with a visual editor for occasional non-dev edits.
- Many small client sites where a hosted CMS bill per project is overkill.
- Setup is fiddlier than Sanity/Storyblok.

### Sanity

- Editors are full-time on content. Complex relationships, references, localization.
- GROQ has a learning curve; portable text is great but takes getting used to.
- Pricing climbs with usage — model it before committing on a large project.

### Storyblok

- Marketers want to drag blocks around and see the page update.
- Component-based — each editable block maps to a React/Astro component.
- Per-user pricing — watch the math on bigger teams.

### Payload

- TypeScript-native end-to-end. You own the database and admin UI.
- Pairs best with Next.js (same project) but going framework-agnostic.
- Younger ecosystem than Strapi/Sanity.

### Webflow CMS

- Only relevant when the framework is Webflow.
- Designers build the schema visually. Everything stays in Webflow.

---

## Heuristics

1. Devs write the content → **MDX** (Astro) or **MDX/Tina** (Next.js).
2. Marketing team owns the content → **Storyblok** (visual) or **Sanity** (structured).
3. Self-hosting is required → **Strapi** or **Payload**.
4. TypeScript-first, full ownership → **Payload**.
5. Predictable monthly cost is the priority → **Strapi** (you control the infra bill).
6. The project might pivot to a real app → match the framework's strength (Payload for Next.js).
7. Webflow-built site → **Webflow CMS**, no question.

---

## Things to confirm before locking the choice

- **Who creates accounts and resets passwords?** Hosted CMSes solve this; self-hosted (Strapi/Payload) need you to.
- **Preview URLs / draft mode** — Sanity, Storyblok, Payload all have first-class support. Strapi needs setup.
- **Localization** — Sanity and Strapi are strongest here.
- **Media handling** — large libraries? Storyblok and Sanity ship CDN-backed asset stores. Self-hosted needs S3 + CloudFront.
- **Webhooks for rebuilds** — every option supports them; confirm the build hook URL flow with your hosting choice.

---

## Open items

Tracked in [../todo.md](../todo.md):

- Validate Strapi-as-default for Next.js after a few project cycles.
- Compare Strapi Cloud vs self-host operational cost in practice.
- Add a "decision tree" diagram once the heuristics stabilize.

---

## AI sanity check

> Reviewed June 2, 2026 (Claude Opus 4.7)

The split between hosted-collab (Sanity, Storyblok), self-hosted (Strapi, Payload), and in-repo (MDX, Tina) still maps cleanly to who edits. Strapi-as-default for Next.js is a recent shift — historically we'd default to Sanity or Payload. The reasoning: predictable cost and plugin coverage outweigh DX wins from the hosted options on most agency projects. Re-validate after Q3 2026.
