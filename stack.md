---
title: "Web Stack Comparison for Landing Pages + Blog (2026)"
description: "A pragmatic comparison of frameworks, CMS choices, and hosting for marketing sites with a blog."
updatedAt: "2026-05-27"
reviewedAt: "2026-05-27"
tags: ["astro", "nextjs", "webflow", "cms", "hosting", "cloudflare", "vercel"]
---

# Web Stack Comparison for Landing Pages + Blog (2026)

> **Updated:** May 27, 2026
> **Scope:** Marketing sites and landing pages with a blog. Some dynamic content, mostly static. Small-to-medium agency context.

The decision splits into three independent layers: **core tech** (how you build), **content source** (where copy lives), and **hosting** (where it runs). This document covers all three, plus Webflow as a fourth all-in-one option.

---

## TL;DR — Three Most Common Approaches

Before getting into individual layers, here are the three stacks that cover ~90% of real-world landing-page-plus-blog projects in 2026.

### 1. Next.js + Headless CMS (Sanity / Strapi / Payload) on Vercel

**Pros:**

- Massive React ecosystem and hiring pool
- Easy to grow into a full app later (auth, dashboards, e-commerce)
- ISR (Incremental Static Regeneration) — mostly-static pages that refresh without full rebuilds
- Best-in-class DX on Vercel: previews, instant rollbacks, edge functions
  **Cons:**
- Ships React runtime by default → heavier bundles, lower Lighthouse out of the box
- Hosting cost scales fast (Vercel $20/seat + usage; surprise bandwidth bills on viral traffic)
- Two systems to maintain (frontend + CMS), each with their own auth, updates, deploys
- ISR reads/writes can quietly inflate Vercel bills
  **Way to go when:**
- The site will plausibly grow into an app
- Your team is already React-deep
- A non-technical team edits content daily and needs a polished CMS UI

---

### 2. Astro + MDX (in-repo content) on Cloudflare Pages

**Pros:**

- Near-zero JavaScript shipped by default → top Lighthouse scores out of the box
- Content lives in Git: versioned, reviewable, branch-previewable
- No CMS server to maintain, no API at runtime, no separate database
- Hosting effectively free on Cloudflare Pages (unlimited bandwidth)
- Astro components can use React/Vue/Svelte for the interactive bits
  **Cons:**
- Non-technical editors need Markdown or a Git-based UI (Tina, Decap)
- Every content change requires a rebuild + redeploy
- Less elegant for content with rich relations (categories, authors as entities)
- Smaller ecosystem than React
  **Way to go when:**
- Devs (or comfortable editors) write the content
- Performance and hosting cost matter
- You maintain multiple similar sites and want minimal infrastructure

---

### 3. Webflow (all-in-one)

**Pros:**

- No code — designers build and ship directly
- Polished CMS, hosting, and editor UI bundled
- Fast turnaround for typical marketing sites
- Clients can edit everything without developer involvement
  **Cons:**
- Vendor lock-in; migration away is painful
- Limited custom logic (animations, integrations, A/B tests hit walls fast)
- Per-site recurring cost ($15–$49+/month) that multiplies across clients
- Performance is decent but not best-in-class
- Code export exists but is limited
  **Way to go when:**
- Designer-led team with no dev capacity (or you want to avoid the dev bottleneck)
- Clients demand visual control of every element
- The site is unlikely to need custom logic or grow into an app

---

### These three aren't the only options

You can mix and match further. Astro + Sanity, Next.js + MDX, Astro + Payload, or even Webflow's CMS API consumed by an Astro frontend — all valid combinations. The three layers (framework, content source, hosting) are largely independent. The full comparison tables below cover the rest.

---

## 1. Layer-by-Layer Comparison Tables

### Frameworks / Core Tech

| Option      | Pros                                                                   | Cons                                                           | When it wins                                             |
| ----------- | ---------------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------- |
| **Astro**   | Zero JS by default, fastest perf, framework-agnostic islands, great DX | Smaller ecosystem than React, less ideal for app-like UIs      | Content sites, landing pages, blogs, docs                |
| **Next.js** | Huge React ecosystem, easy to grow into an app, ISR, mature tooling    | Ships React runtime, heavier bundles, hosting cost scales fast | Sites that will grow into apps; React-heavy teams        |
| **Webflow** | No-code, visual editor, designer-friendly, hosted CMS included         | Vendor lock-in, limited custom logic, per-site recurring cost  | Designer-led teams; clients who want full visual control |

### Content Source / CMS

| Option                   | Pros                                                | Cons                                          | When it wins                                              |
| ------------------------ | --------------------------------------------------- | --------------------------------------------- | --------------------------------------------------------- |
| **MDX in repo**          | Free, versioned in Git, no infra, devs love it      | Editors must learn Markdown or Git-based UI   | Dev-written content, technical blogs                      |
| **Tina CMS** (Git-based) | Visual editor + Git workflow, no server             | Setup is fiddlier than hosted CMS             | Small clients who want editor UX without ongoing CMS cost |
| **Sanity**               | Real-time, flexible schemas, polished editor        | GROQ learning curve, gets pricey at scale     | Content-heavy sites with editorial teams                  |
| **Storyblok**            | Best-in-class visual editor, component-based        | Pricing escalates quickly with users/spaces   | Marketing teams that want visual editing                  |
| **Payload**              | TypeScript-native, self-hostable, no vendor lock-in | Younger ecosystem, best DX still with Next.js | Teams that want full ownership + type safety              |
| **Strapi**               | Open source, self-hosted, plugin ecosystem          | Maintenance burden, plugin quality varies     | Self-hosted needs with custom backend logic               |
| **Webflow CMS**          | Built into Webflow, fully visual                    | Locked to Webflow frontend                    | All-in-one Webflow projects                               |

### Hosting

| Option                    | Pros                                                             | Cons                                                   | When it wins                                    |
| ------------------------- | ---------------------------------------------------------------- | ------------------------------------------------------ | ----------------------------------------------- |
| **Vercel**                | Best Next.js DX, polished previews, edge functions               | Expensive at scale, surprise bandwidth bills, $20/seat | Next.js apps with advanced features             |
| **Cloudflare Pages**      | Unlimited free bandwidth, 300+ edge locations, cheapest at scale | Less polished Next.js integration, rougher CLI         | Static sites, Astro, high-traffic landing pages |
| **Netlify**               | Good DX, Vercel-like flow for non-Next stacks                    | Expensive bandwidth overages ($55/100GB)               | Vercel migration path; non-Next stacks          |
| **Webflow Hosting**       | Bundled with platform, zero config                               | Locked in, per-site pricing                            | Webflow sites only                              |
| **AWS (S3 + CloudFront)** | Full control, predictable AWS billing                            | No previews, no Git workflow, manual setup             | AWS-committed orgs; specific compliance needs   |

---

## 2. Stack-by-Stack Comparisons

### 2.1 Astro vs Next.js

The big question for most agencies. Both can do static sites, both can do dynamic content, both work with any CMS.

| Dimension               | Astro                                               | Next.js                                 |
| ----------------------- | --------------------------------------------------- | --------------------------------------- |
| **Default JS shipped**  | Zero (islands hydrate on demand)                    | React runtime always included           |
| **Lighthouse scores**   | Near-perfect out of the box                         | Good, but requires work for top scores  |
| **Build speed**         | Fast                                                | Slower (especially with many MDX files) |
| **Component model**     | Astro components + any framework (React/Vue/Svelte) | React only                              |
| **Routing**             | File-based, simple                                  | File-based, App Router (RSC-aware)      |
| **Dynamic features**    | Endpoints + integrations                            | Full server, API routes, server actions |
| **Image optimization**  | Built-in `<Image>` component                        | `next/image` (optimal on Vercel)        |
| **MDX support**         | First-class, content collections built-in           | `@next/mdx` or `next-mdx-remote-client` |
| **Hosting flexibility** | Any static host or Node                             | Best on Vercel; static export possible  |
| **Learning curve**      | Low if you know HTML/CSS                            | Medium-high (React + Next concepts)     |
| **Ecosystem**           | Growing fast                                        | Massive                                 |

**Verdict:** For landing pages + blog, Astro wins on performance, simplicity, and hosting cost. Pick Next.js when the site will clearly grow into a React app (dashboards, auth flows, complex client state).

### 2.2 MDX in Repo vs Headless CMS

| Dimension                     | MDX in Repo                      | Headless CMS                             |
| ----------------------------- | -------------------------------- | ---------------------------------------- |
| **Editor experience**         | Markdown or Git UI (Tina, Decap) | Polished web UI, previews, media library |
| **Cost**                      | Free                             | $0–$500+/month depending on CMS and tier |
| **Versioning**                | Native Git history               | CMS-specific (varies in quality)         |
| **Publishing speed**          | Requires rebuild + deploy        | Webhook-triggered or instant via ISR     |
| **Relations (tags, authors)** | Manual via frontmatter           | Native, structured                       |
| **Media management**          | Files in repo or external        | Built-in DAM                             |
| **Offline editing**           | Yes (it's just files)            | No                                       |
| **Backup/portability**        | Trivial (Git clone)              | Export-dependent, often lossy            |
| **Best for**                  | Dev-written or technical content | Marketing/editorial teams                |

**Hybrid option worth knowing:** Tina CMS gives editors a visual UI but writes back to MDX files in Git. Combines most of both worlds.

### 2.3 Vercel vs Cloudflare Pages

| Dimension               | Vercel                             | Cloudflare Pages                              |
| ----------------------- | ---------------------------------- | --------------------------------------------- |
| **Free tier bandwidth** | 100 GB/month                       | Unlimited                                     |
| **Bandwidth overage**   | ~$15/100 GB                        | None (free)                                   |
| **Edge locations**      | ~100+                              | 300+                                          |
| **Next.js support**     | First-class (it's their framework) | Works but needs adapter, some features tricky |
| **Astro/static sites**  | Works fine                         | Excellent, often a better fit                 |
| **Preview deployments** | Best-in-class                      | Good                                          |
| **Edge functions**      | Vercel Edge Functions              | Cloudflare Workers                            |
| **Pricing model**       | $20/seat/month + usage             | $5/month base (Workers Paid), generous limits |
| **Surprise bills risk** | Real (viral traffic)               | Very low                                      |
| **DX polish**           | Highest in the industry            | Improving fast; CLI-driven                    |

**Verdict:** For static sites and Astro, Cloudflare Pages is the better economic choice — full stop. For Next.js with ISR or advanced features, Vercel is still the smoothest experience.

### 2.4 Code-Based Stack vs Webflow

| Dimension              | Astro / Next.js                              | Webflow                                        |
| ---------------------- | -------------------------------------------- | ---------------------------------------------- |
| **Who builds it**      | Developers                                   | Designers (no-code)                            |
| **Output**             | Standard HTML/CSS/JS, fully owned            | Webflow-rendered, partial code export only     |
| **CMS**                | Bring your own (MDX, Sanity, etc.)           | Webflow CMS bundled                            |
| **Hosting**            | Your choice                                  | Webflow hosting only (for the full experience) |
| **Custom logic**       | Unlimited                                    | Limited; needs custom code embeds              |
| **Animations**         | Any library (Motion, GSAP, View Transitions) | Webflow Interactions (visual)                  |
| **Performance**        | Excellent (especially Astro)                 | Decent but not best-in-class                   |
| **Per-site cost**      | Hosting only (often $0)                      | $15–$49+/month per site                        |
| **Editor for clients** | Depends on CMS chosen                        | Built-in, polished                             |
| **Vendor lock-in**     | None                                         | High                                           |
| **Migration away**     | Easy (it's just code)                        | Painful                                        |
| **AI tooling fit**     | Excellent (Claude, Cursor work great)        | Limited                                        |

**Where Webflow wins:**

- Designer-led teams without dev resources
- Clients who insist on visual control of every element
- Tight timelines with no custom backend needs
- Marketing teams that publish frequently and want zero developer involvement
  **Where code wins:**
- Custom interactions, animations, or logic
- Performance-critical sites
- Long-term cost (Webflow's per-site fees add up)
- Multiple sites sharing a design system
- Anything that might grow into an app

---

## 3. Recommended Stacks by Scenario

### Scenario A: Agency landing page with blog, client edits content

**Stack:** Astro + Storyblok (or Sanity) + Cloudflare Pages
**Why:** Editor gets a polished UI, you get top performance, hosting is essentially free.
**Estimated monthly cost:** $0–$25 (CMS tier dependent)

### Scenario B: Dev-team blog or technical content site

**Stack:** Astro + MDX in repo + Cloudflare Pages
**Why:** Content lives with code, full Git workflow, no external dependencies, $0 hosting.
**Estimated monthly cost:** $0

### Scenario C: Marketing site that will grow into a SaaS app

**Stack:** Next.js + Payload (self-hosted) + Vercel
**Why:** Keeps React ecosystem, Payload scales with the app, Vercel's Next.js DX pays off when complexity grows.
**Estimated monthly cost:** $20–$100+ depending on traffic

### Scenario D: Designer-led, no dev resources, fast turnaround

**Stack:** Webflow (all-in-one)
**Why:** Eliminates the dev bottleneck. Client can edit everything.
**Estimated monthly cost:** $15–$49 per site

### Scenario E: Small clients on retainer, you maintain many sites

**Stack:** Astro + Tina CMS (Git-based) + Cloudflare Pages
**Why:** Zero recurring CMS costs across many sites, editor UX is decent, you own everything.
**Estimated monthly cost:** $0 per site

---

## 4. Decision Heuristics

A few rules of thumb to short-circuit the decision:

1. **Will the site stay primarily content?** → Astro.
2. **Will it grow into an app?** → Next.js.
3. **Will a non-dev edit content daily?** → Headless CMS or Webflow.
4. **Will devs write the content?** → MDX in repo.
5. **Is bandwidth unpredictable or potentially viral?** → Cloudflare Pages.
6. **Are advanced Next.js features (ISR, edge middleware) used?** → Vercel.
7. **Is the client design-led with no dev capacity?** → Webflow.
8. **Multiple similar sites for different clients?** → Code-based with a shared template.

---

## 5. Things Often Forgotten

These are independent of the core stack but worth deciding up front:

- **Analytics:** Plausible, Umami, or Cloudflare Web Analytics (privacy-friendly, GDPR-safe). Skip Google Analytics unless required.
- **Forms:** Formspree, Basin, or Cloudflare Pages Functions. Resend for transactional email.
- **Search:** Pagefind for static sites (client-side, ~few KB of JS, no Algolia subscription).
- **Image optimization:** Astro's built-in `<Image>` is great. Off-Vercel Next.js needs Cloudinary, imgix, or Cloudflare Images.
- **A/B testing:** PostHog (1M events/month free) or Vercel Edge Config.
- **Content schema validation:** Astro content collections natively; `contentlayer` for Next.js.

---

## 6. Migration Notes

Worth flagging since these come up in real decisions:

- **`next-mdx-remote` archived April 2026.** Use `@next/mdx` or `next-mdx-remote-client` instead.
- **Next.js `output: 'export'`** produces static files like Astro does — viable if you want to leave Vercel without rewriting.
- **Webflow's legacy Editor sunsets August 4, 2026.** Affects editor seat pricing on existing Webflow sites.
- **Vercel ISR costs** (reads/writes at $4/M) can quietly inflate bills on busy Next.js sites.

---

## 7. The Honest Bottom Line

For typical agency landing-page-plus-blog work in 2026:

- **Default to Astro + Cloudflare Pages.** It's faster, cheaper, and simpler than the Next.js + Vercel combo for content sites.
- **Pick a CMS based on who edits, not on technical preference.** Devs write? MDX. Marketers write? Storyblok/Sanity. Designers run everything? Webflow.
- **Keep Next.js for apps, not sites.** It's still the best React framework for actual applications — just stop reaching for it by default for marketing sites.
- **Cloudflare's economics are genuinely hard to beat** for anything static, and that includes most landing pages.
  The biggest mindset shift from a few years ago: the "Next.js + headless CMS + Vercel" stack is no longer the obvious default. Pick each layer independently based on the actual job.

---

## 8. AI Stack Review

> **Reviewed:** May 27, 2026 (Claude Opus 4.7)

Brief sanity-check of whether the three main approaches above still hold up at review date:

- **Next.js + Headless CMS on Vercel** — ✅ Still valid. Next.js 16 (Oct 2025) introduced Cache Components and improved Turbopack; the stack remains the default for React-heavy or app-shaped projects. The main caveat is unchanged: Vercel's per-seat + bandwidth pricing punishes content-only sites.
- **Astro + MDX on Cloudflare Pages** — ✅ Still valid, and arguably stronger than a year ago. Astro continues to win head-to-head perf comparisons for content sites, and Cloudflare Pages' unlimited-bandwidth free tier remains unmatched. No major contender has displaced this combo for marketing sites.
- **Webflow** — ✅ Still valid in its niche. The May 13, 2026 pricing update and the August 4, 2026 legacy Editor sunset are real but don't fundamentally change the value proposition. Framer is gaining ground for portfolios and landing pages at lower price points and worth a separate look if Webflow feels too heavy.
  **Watch list (things that might shift the picture in the next 6–12 months):**
- React's `<ViewTransition>` becoming stable could close some of the perceived "feel" gap between Next.js and Astro.
- Payload's framework-agnostic push may make Astro + Payload a stronger combo than it is today.
- Cloudflare's Next.js support is improving; if it reaches parity with Vercel's, the Vercel premium becomes harder to justify.
- AI-assisted development is making the "Webflow is faster" argument weaker — Claude/Cursor can scaffold an Astro landing page in minutes.
  **Re-review this document in:** Q4 2026, or sooner if any of the watch-list items land.
