# 30-anti-slop-skills

A collection of Claude Code / agent skills for building and shipping real websites, not AI-slop demos.

Each skill in `skills/` is a self-contained `SKILL.md` (Claude Code skill format) that teaches an agent what a competent web developer actually does for that part of the job, including the mistakes that make a site scream "an AI built this."

See [WHY.md](WHY.md) for the reasoning behind this repo.

## Quick start

Paste this into Claude Code in any project where you want these skills available:

```
Clone https://github.com/hainesdrewh/30-anti-slop-skills.git into a temp
directory, copy every folder under its skills/ directory into this
project's .claude/skills/ directory (create .claude/skills/ if it doesn't
exist yet, and don't overwrite any skill folder already there with the
same name unless I confirm), then delete the temp clone and list which
skills are now installed.
```

Claude Code will pick up every installed skill automatically based on what you ask it to do; you don't need to invoke them by name.

## Status

All 30 skills are built. Private while under review before going public.

## Roadmap

| # | Skill | Covers |
|---|-------|--------|
| 1 | `anti-ai-slop-design` (flagship) | Visual/UX judgment: what makes a site read as generic AI output, and the real alternatives |
| 2 | `pre-launch-technical-audit` | Broken links, horizontal scroll, mobile overflow, broken buttons, placeholder text, custom 404, favicon, page titles, footer/copyright year |
| 3 | `form-ux-feedback` | Form validation, error messages, success messages, required-field UX |
| 4 | `on-page-seo` | Titles, meta descriptions, header hierarchy, internal linking, image alt text |
| 5 | `technical-seo-crawlability` | sitemap.xml, robots.txt, llms.txt, canonical tags, Google Search Console setup |
| 6 | `structured-data-schema` | Organization, LocalBusiness, Service, FAQ, Article schema markup |
| 7 | `local-service-seo` | Location pages, service pages, NAP consistency, tap-to-call, opening hours, local keywords |
| 8 | `trust-and-about-content` | About/story page, visible contact info, credibility signals |
| 9 | `blog-content-seo` | Blog post structure, related content, internal linking within content |
| 10 | `conversion-ctas` | CTA placement above the fold, thank-you pages, payment clarity |
| 11 | `mobile-navigation-ux` | Mobile menu, clickable logo/phone/email, tap-to-call, mobile optimization |
| 12 | `legal-compliance-pages` | Privacy policy, ToS, cookie consent |
| 13 | `image-performance-optimization` | Compression, modern formats, lazy loading, responsive images |
| 14 | `accessibility-basics` | Contrast, focus states, semantic HTML, keyboard nav, skip-to-content |
| 15 | `contact-page-standards` | Visible email/phone, map, hours, social links |
| 16 | `review-testimonials-social-proof` | Real reviews, author bios, credible guarantee statements |
| 17 | `case-studies-portfolio` | Case study, before/after, and portfolio page structure |
| 18 | `tooltips-microcopy-ux` | Rich tooltips, modals, confirmation modals, empty states |
| 19 | `breadcrumbs-internal-linking` | Breadcrumb nav, internal link structure |
| 20 | `custom-error-pages` | 404/500 pages that keep users on-site |
| 21 | `frontend-polish-microinteractions` | Dark mode, loading states, sticky header, scroll-to-top, site search |
| 22 | `analytics-and-attribution-basics` | UTM tracking, privacy-respecting conversion tracking |
| 23 | `project-scoping-and-prd` | Define ICP/value prop, write a PRD, before building |
| 24 | `secrets-and-env-hardening` | .env hygiene, no client-exposed API keys, purging leaked secrets |
| 25 | `auth-and-session-security` | Password hashing, secure cookies, CSRF, session invalidation, account lockout |
| 26 | `database-access-control` | Row-level security, least-privilege DB roles, server-side ownership checks |
| 27 | `input-validation-and-injection-defense` | Server-side validation, parameterized queries, XSS/prompt-injection defense |
| 28 | `api-abuse-and-rate-limiting` | Rate limiting, capped AI usage, bot protection, anti signup/login spam |
| 29 | `file-upload-and-payment-integrity` | Upload whitelisting, server-side pricing, verified payment webhooks |
| 30 | `transport-headers-and-monitoring` | HTTPS/HSTS, CORS, security headers, dependency scanning, security logging |

## Using a single skill

Each `skills/<name>/SKILL.md` follows the standard Claude Code skill format (YAML frontmatter plus instructions). Copy an individual skill folder into your project's `.claude/skills/` directory if you only want one, rather than the full set from Quick Start above.

## License

TBD before going public.
