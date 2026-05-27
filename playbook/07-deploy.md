# 7. Deploy

**Goal:** the site is live on production hosting with previews on every PR.

## To be filled in (per hosting choice)

- **Cloudflare Pages** — repo connection, build settings, env vars, custom domain, Pages Functions
- **Vercel** — Git integration, env vars, custom domain, ISR config, edge functions
- **Webflow** — publishing, custom code embeds, domain setup

## Cross-cutting topics

- Preview deployments on PRs
- Branch protection rules (require checks, require review)
- Analytics setup (Plausible / Cloudflare Web Analytics)
- Forms (Formspree / Basin / CF Pages Functions)
- Production checklist — Lighthouse, `og:image`s, `sitemap.xml`, `robots.txt`, 404 page

## Open questions

- Do we want a single "production readiness" checklist that lives here, or one per stack?
- CI: GitHub Actions baseline (lint, typecheck, build) — standardize?

Done — back to [playbook/](README.md).
