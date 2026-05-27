---
title: "Web Stack for Landing Pages + Blog (2026)"
description: "How we pick a stack for marketing sites with a blog: framework, content source, hosting."
updatedAt: "2026-05-27"
reviewedAt: "2026-05-27"
tags: ["astro", "nextjs", "webflow", "cms", "hosting", "cloudflare", "vercel"]
---

# Web Stack for Landing Pages + Blog (2026)

> **Scope:** Marketing sites, landing pages, blogs. Mostly static, some dynamic. Small-to-medium agency context.

A stack is **three independent choices**: how you **build** (framework), where the **content** lives, and where it **runs** (hosting). Pick each layer on its own merits — they recombine freely.

---

## TL;DR

| Stack                                                | Best when                                                                   | Cost/mo  |
| ---------------------------------------------------- | --------------------------------------------------------------------------- | -------- |
| **Astro + MDX + Cloudflare Pages**                   | Devs write content. Performance and cost matter. Default for content sites. | ~$0      |
| **Astro + Storyblok/Sanity + Cloudflare Pages**      | Non-dev editors. Still want top performance and cheap hosting.              | $0–$25   |
| **Next.js + Payload/Sanity + Vercel**                | Site will plausibly grow into an app. React-deep team.                      | $20–$100 |
| **Webflow**                                          | Designer-led, no dev capacity, client wants full visual control.            | $15–$49  |

**Default to Astro + Cloudflare Pages** for content sites. Reach for Next.js only when it'll grow into a real app. Webflow is for design-led work without devs.

---

## 1. Pick a framework

| Option      | Strengths                                                  | Weaknesses                                       | When it wins                                |
| ----------- | ---------------------------------------------------------- | ------------------------------------------------ | ------------------------------------------- |
| **Astro**   | Zero JS by default · top Lighthouse · framework-agnostic islands | Smaller ecosystem · weaker for app-like UIs      | Content sites, landing pages, blogs, docs   |
| **Next.js** | Massive React ecosystem · grows into an app · ISR          | Ships React runtime · hosting cost scales fast   | Sites destined to become apps; React teams  |
| **Webflow** | No-code · visual editor · CMS bundled                      | Vendor lock-in · limited logic · per-site fees   | Designer-led teams; clients wanting control |

**Heuristic:** primarily content → Astro. Will grow into an app → Next.js. No dev capacity → Webflow.

---

## 2. Pick a content source

| Option           | Strengths                              | Weaknesses                          | Best for                          |
| ---------------- | -------------------------------------- | ----------------------------------- | --------------------------------- |
| **MDX in repo**  | Free · Git-versioned · zero infra      | Editors need Markdown or Git UI     | Devs writing content              |
| **Tina** (Git)   | Visual editor on top of MDX            | Fiddlier setup than hosted CMS      | Many small clients, low cost      |
| **Sanity**       | Real-time · flexible schemas           | GROQ curve · pricey at scale        | Editorial teams, content-heavy    |
| **Storyblok**    | Best visual editor · component-based   | Pricing escalates with users        | Marketing teams, visual editing   |
| **Payload**      | TypeScript-native · self-hostable      | Younger · best DX still with Next   | Full ownership + type safety      |
| **Strapi**       | OSS · self-hosted · plugins            | Maintenance burden                  | Custom self-hosted backends       |
| **Webflow CMS**  | Bundled · fully visual                 | Locked to Webflow                   | All-in-one Webflow projects       |

**Heuristic:** devs write → MDX. Marketers write → Storyblok or Sanity. Everyone edits visually → Webflow. Many small clients → Tina.

---

## 3. Pick hosting

| Option               | Strengths                                  | Weaknesses                              | Best for                          |
| -------------------- | ------------------------------------------ | --------------------------------------- | --------------------------------- |
| **Cloudflare Pages** | **Unlimited free bandwidth** · 300+ edges  | Rougher Next.js story · CLI-driven      | Static, Astro, high-traffic sites |
| **Vercel**           | Best Next.js DX · polished previews        | $20/seat + usage · surprise bills       | Next.js with ISR / edge features  |
| **Netlify**          | Good DX for non-Next stacks                | Expensive bandwidth overages            | Vercel migration paths            |
| **AWS S3 + CF**      | Full control · predictable billing         | No previews · no Git workflow           | AWS-committed orgs                |
| **Webflow Hosting**  | Bundled · zero config                      | Locked in · per-site pricing            | Webflow sites only                |

**Heuristic:** static or Astro → Cloudflare Pages. Next.js with ISR/edge → Vercel. Traffic is unpredictable → Cloudflare.

---

## 4. Decision heuristics

Short-circuit the decision with these:

1. Client already uses a stack in other projects → **match it** (easier handoff, shared conventions, team familiarity often outweighs picking the "ideal" stack)
2. Stays content-focused → **Astro**
3. Will grow into an app → **Next.js**
4. Non-dev edits content daily → **Headless CMS** or **Webflow**
5. Devs write the content → **MDX in repo**
6. Bandwidth unpredictable or potentially viral → **Cloudflare Pages**
7. Uses Next.js ISR / edge middleware → **Vercel**
8. Design-led client, no dev capacity → **Webflow**
9. Many similar sites for different clients → **Code + shared template**

---

## 5. Things often forgotten

These are independent of the core stack:

- **Analytics:** Plausible, Umami, or Cloudflare Web Analytics. Skip GA unless required.
- **Forms:** Formspree, Basin, or CF Pages Functions. Resend for transactional email.
- **Search:** [Pagefind](https://pagefind.app) — client-side, few KB, no Algolia bill.
- **Images:** Astro `<Image>` works out of the box. Off-Vercel Next.js needs Cloudinary / Cloudflare Images.
- **A/B testing:** PostHog (1M events/mo free) or Vercel Edge Config.
- **Schema validation:** Astro content collections; `contentlayer` for Next.js.

---

## 6. Gotchas to know

- **`next-mdx-remote` archived (Apr 2026).** Use `@next/mdx` or `next-mdx-remote-client`.
- **Vercel ISR reads/writes** ($4/M) can quietly inflate bills on busy sites.
- **Webflow's legacy Editor sunsets Aug 4, 2026** — affects seat pricing on existing sites.
- **Next.js `output: 'export'`** produces static files — a viable escape hatch from Vercel without a rewrite.

---

## 7. The honest bottom line

- **Default to Astro + Cloudflare Pages.** Faster, cheaper, simpler than Next.js + Vercel for content sites.
- **Pick the CMS by who edits, not by technical preference.** Devs → MDX. Marketers → Storyblok/Sanity. Designers → Webflow.
- **Keep Next.js for apps, not sites.** Still the best React framework — just stop reaching for it by default on marketing sites.

The biggest mindset shift from a few years ago: "Next.js + headless CMS + Vercel" is no longer the obvious default. Pick each layer on its own merits.

---

## 8. AI sanity check

> Reviewed May 27, 2026 (Claude Opus 4.7)

All three main approaches still hold up:

- **Next.js + CMS + Vercel** ✅ Next.js 16 brought Cache Components and better Turbopack; the per-seat + bandwidth pricing still punishes content-only sites.
- **Astro + MDX + Cloudflare Pages** ✅ Stronger than a year ago. No serious contender has displaced it for marketing sites.
- **Webflow** ✅ Still valid in its niche. Framer is closing in on portfolios + landing pages at a lower price; worth a separate look.

**Watch list (next 6–12 months):**

- React `<ViewTransition>` going stable may narrow the "feel" gap between Next.js and Astro.
- Payload going framework-agnostic could make Astro + Payload a real combo.
- Cloudflare's Next.js support is improving — parity with Vercel would erode the Vercel premium.
- AI-assisted dev is weakening the "Webflow is faster" argument for simple landing pages.

**Re-review:** Q4 2026, or sooner if any watch-list item lands.
