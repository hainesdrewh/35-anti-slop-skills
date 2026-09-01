# 45-anti-slop-skills

A collection of Claude Code / agent skills for building and shipping real websites, not AI-slop demos.

Each skill in `skills/` is a self-contained `SKILL.md` (Claude Code skill format) that teaches an agent what a competent web developer actually does for that part of the job, including the mistakes that make a site scream "an AI built this." 

Please don't expect to be able to download these skills and instantly be able to have AI make you a perfect website in one prompt you yourself still needs some sort of taste to build something great, you'll need to prompt a few times before its "production ready." Maybe more than a few times if you've never built a site before but never the less these skills are perfect for backend and frontend no matter how much experience you have.

See [WHY.md](WHY.md) for the reasoning behind this repo.

## Examples

Real (working, local) sites built entirely with these skills, screenshots included:

- [Fieldstone Landscape Co.](examples/fieldstone-landscape-co): a local landscaping/hardscaping business site\
- Disclosr.info A site for finding local food and produce businesses. 

## Quick start

Paste this into Claude Code in any project where you want these skills available:

```
Clone https://github.com/Kryhr/45-anti-slop-skills.git into a temp
directory, copy every folder under its skills/ directory into this
project's .claude/skills/ directory (create .claude/skills/ if it doesn't
exist yet, and don't overwrite any skill folder already there with the
same name unless I confirm), then delete the temp clone and list which
skills are now installed.
```

Claude Code will pick up every installed skill automatically based on what you ask it to do; you don't need to invoke them by name.

## Status

All 45 skills are built and this repo is public. More skills are being added over time.

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
| 31 | `layout-spacing-and-alignment` | A real spacing scale, vertical rhythm, optical vs. mathematical alignment |
| 32 | `typography-craft` | Line length, line-height scaling, type scale, widow/orphan control, font loading |
| 33 | `component-detail-polish` | Every real interactive state (active, disabled, focus, loading), not just hover |
| 34 | `motion-system` | A coherent easing/duration system, reduced-motion handled everywhere |
| 35 | `industry-visual-execution` | Picture-perfect layout patterns per vertical: real estate, restaurants, home services, and more |
| 36 | `contrast-and-image-integrity-checks` | Scriptable contrast checks, and verifying an image actually matches what the copy claims |
| 37 | `data-grid-and-listing-pages` | Browsing/filtering UI: real estate listings, e-commerce category pages, job boards, directories |
| 38 | `ecommerce-layout-patterns` | Product pages, cart, checkout, honest pricing and stock/shipping information |
| 39 | `saas-marketing-pages` | Landing pages, pricing pages, and features pages that avoid the generic SaaS template |
| 40 | `portfolio-and-creative-showcase` | Portfolio sites where the work itself is the primary content |
| 41 | `editorial-and-blog-layout` | Reading-optimized layout for content-heavy and publication-style sites |
| 42 | `dashboard-and-app-ui` | Internal app UI: data tables, persistent nav, density for daily repeated use |
| 43 | `visual-style-directions` | Five named, fully-specified style systems, so not every site defaults to the same look |
| 44 | `advanced-motion-and-3d` | Scroll-driven animation, 3D transforms, and WebGL judgment, performance, and accessibility |
| 45 | `image-sourcing-and-generation` | Finding real stock photos or generating images that actually match the content |

## Using a single skill

Each `skills/<name>/SKILL.md` follows the standard Claude Code skill format (YAML frontmatter plus instructions). Copy an individual skill folder into your project's `.claude/skills/` directory if you only want one, rather than the full set from Quick Start above.

## License

MIT. See [LICENSE](LICENSE).
