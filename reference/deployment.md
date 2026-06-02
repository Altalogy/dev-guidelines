---
title: "Deployment Choice (2026)"
description: "Where projects ship. Vercel default, CloudFront as AWS alternative, Cloudflare Pages for static."
updatedAt: "2026-06-02"
reviewedAt: "2026-06-02"
tags: ["deployment", "vercel", "cloudfront", "aws", "cloudflare-pages", "webflow"]
---

# Deployment Choice (2026)

> **Scope:** Where the project actually runs in production. Hosting choice has knock-on effects (preview URLs, env vars, edge features, billing model) — surface them up front.

---

## Defaults per project type

| Project type | Default | Why |
| --- | --- | --- |
| **Website — Next.js** | **Vercel** | Best Next.js DX, ISR/edge work without config, preview URLs per PR. |
| **Website — Astro** | **Cloudflare Pages** | Unlimited bandwidth, global edge, free for our scale. |
| **Website — Webflow** | **Webflow Hosting** | Bundled. Not a separate choice. |
| **Prototype — Next.js** | **Vercel** | Free hobby tier, instant preview URLs. |
| **Prototype — HTML/CSS/JS** | **Cloudflare Pages** *(or Vercel static)* | Fastest path to a public URL. |
| **Tool** | Depends — CLI ships via npm; web tool → **Vercel**. | |

**AWS alternative:** when a client mandates AWS, default to **CloudFront + S3** (static) or **CloudFront + Lambda@Edge / Amplify** (SSR). See below.

---

## TL;DR table

| Host | Strengths | Weaknesses | Cost shape |
| --- | --- | --- | --- |
| **Vercel** *(default)* | Best Next.js DX, preview URLs, edge runtime, image opt | $20/seat + usage; ISR reads/writes add up | Free hobby; Pro from $20/seat/mo + usage |
| **Cloudflare Pages** | Unlimited bandwidth, 300+ edge locations, generous free tier | Next.js story rougher than Vercel; CLI-driven | Free tier covers most; paid for advanced features |
| **AWS (CloudFront + S3)** | Full control, predictable bill, AWS-native | No preview URLs, no Git workflow out of the box | Pay per request + bandwidth |
| **Webflow Hosting** | Bundled, zero config | Locked in, per-site pricing | Site plan from ~$15/mo |
| **Netlify** | Good DX for non-Next stacks | Bandwidth overages get expensive | Free tier; paid for usage |

---

## Vercel *(default)*

**Use when:** Next.js website, or any project where preview URLs and zero-config matter.

**Setup:**

1. Connect GitHub repo via Vercel dashboard.
2. Set framework preset (auto-detected for Next.js).
3. Add environment variables (production + preview).
4. Add custom domain → Vercel handles cert.
5. Branch protection: require Vercel preview check on PRs.

**Watch:**

- **Per-seat pricing** — Pro is $20/seat/mo. Adds up on bigger teams.
- **ISR reads/writes** — $4/M can quietly inflate the bill on busy sites.
- **Image optimization** — counts against monthly quota.
- **Function bandwidth** — separate meter from static bandwidth.

**Escape hatch:** Next.js with `output: 'export'` produces static files — deployable anywhere. Useful when leaving Vercel without a rewrite.

---

## CloudFront + S3 *(AWS alternative)*

**Use when:** client requires AWS, or org already has AWS billing/SSO and wants one bill.

**Static-site flow (S3 + CloudFront + ACM + Route 53):**

1. Build site locally (or in CI) → upload to S3 bucket.
2. CloudFront distribution in front of the bucket (Origin Access Control, not legacy OAI).
3. ACM cert in `us-east-1` for the domain.
4. Route 53 alias record → CloudFront.
5. GitHub Actions: build → `aws s3 sync` → `aws cloudfront create-invalidation`.

**SSR / Next.js on AWS:**

- **Amplify Hosting** — closest to Vercel DX on AWS. Connect repo, gets previews + SSR. Watch: less mature than Vercel for Next.js 16 features.
- **OpenNext** — adapts Next.js to Lambda@Edge + CloudFront. Self-managed; more setup but more control.

**Watch:**

- **No preview URLs out of the box** — build it in CI (PR → ephemeral CloudFront distro) or use Amplify.
- **Cache invalidation** — `/*` invalidation is free first 1,000/month, then per path. Plan deployments accordingly.
- **ACM cert must be in us-east-1** for CloudFront, even if everything else is in your region.
- **Cold-start latency** on Lambda@Edge can surprise people coming from Vercel edge.

> Stubbed sections to flesh out — see [../todo.md](../todo.md): step-by-step S3 + CloudFront + ACM + Route 53 setup; OpenNext vs Amplify decision tree; CI workflow template.

---

## Cloudflare Pages

**Use when:** Astro, static sites, anything where bandwidth is unpredictable.

**Setup:**

1. Connect GitHub repo via Cloudflare dashboard.
2. Set build command + output directory (Astro auto-detected).
3. Env vars per environment (production + preview).
4. Custom domain via Cloudflare DNS (cert automatic).
5. Pages Functions for serverless endpoints if needed.

**Watch:**

- **Next.js support** — workable via `@cloudflare/next-on-pages`, but expect more rough edges than Vercel.
- **Build minutes** — free tier has limits; busy repos can hit them.

---

## Webflow Hosting

**Use when:** the project itself is a Webflow project.

- Publishing is one click in Webflow.
- Custom domain managed in Webflow.
- No CI/CD — Webflow IS the workflow.
- Custom code via embeds.

Not a real choice — auto-applied when the framework is Webflow.

---

## Cross-cutting topics

These apply regardless of host:

- **Preview deployments on PRs** — Vercel/Cloudflare Pages auto; AWS needs custom CI.
- **Branch protection** — require checks (lint, typecheck, build, preview) before merge.
- **Environment variables** — split production vs preview vs development. Never commit secrets.
- **Analytics** — Plausible / Cloudflare Web Analytics / Umami. Skip GA unless mandated.
- **Forms** — Formspree, Basin, or host-native (CF Pages Functions / Vercel API routes).
- **Production checklist** — Lighthouse pass, `og:image`s, `sitemap.xml`, `robots.txt`, 404 page, redirect rules.

---

## Heuristics

1. Next.js website → **Vercel** unless client mandates AWS.
2. Static / Astro → **Cloudflare Pages**.
3. Client mandates AWS → **CloudFront + S3** (static) or **Amplify** (SSR, simpler) or **OpenNext** (SSR, more control).
4. Webflow → **Webflow Hosting**.
5. Unpredictable / potentially viral bandwidth → **Cloudflare Pages**.
6. Using Next.js ISR / edge middleware heavily → stay on **Vercel**.
7. Tool / CLI → ship via **npm**, not hosting.

---

## Open items

Tracked in [../todo.md](../todo.md):

- Full step-by-step CloudFront + S3 + ACM + Route 53 walkthrough.
- OpenNext vs Amplify Hosting decision for Next.js on AWS.
- CI workflow templates per host.
- Cloudflare Pages parity section (depth-match the Vercel section).

---

## AI sanity check

> Reviewed June 2, 2026 (Claude Opus 4.7)

Vercel-as-default for Next.js still holds — DX is unmatched. Cloudflare Pages is the right call for static/Astro. The AWS-alternative path is the most under-documented here and the most likely to come up on enterprise client work — prioritize filling it in. Re-review Q4 2026.
