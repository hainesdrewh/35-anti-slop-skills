# 20-anti-slop-skills

A collection of Claude Code / agent skills for building and shipping real websites — not AI-slop demos.

Each skill in `skills/` is a self-contained `SKILL.md` (Claude Code skill format) that teaches an agent what a competent web developer actually does for that part of the job, including the mistakes that make a site scream "an AI built this."

## Why this exists

Most AI-generated sites share the same tells: gradient hero sections, rainbow-gradient headline text, generic hover-lift cards, three feature cards with an emoji icon, a fake testimonial carousel, no real favicon, no 404 page, broken mobile nav, missing meta tags, and zero actual SEO structure. These skills exist to close that gap — covering both the "don't do this" anti-patterns and the concrete "do this" checklist a real launch needs.

## Status

Private during development. Skills are being built and reviewed one at a time; see the roadmap below for progress.

## Plan

See [PLAN.md](PLAN.md) for the full build plan: depth standard, what each skill covers, and how every item from the original checklist maps to a skill.

## Roadmap

| # | Skill | Covers | Status |
|---|-------|--------|--------|
| 1 | `anti-ai-slop-design` (flagship) | Visual/UX judgment: what makes a site read as generic AI output, and the real alternatives | 🚧 |
| 2 | `pre-launch-technical-audit` | Broken links, horizontal scroll, mobile overflow, broken buttons, placeholder text, custom 404, favicon, page titles, footer/copyright year | 🚧 |
| 3 | `form-ux-feedback` | Form validation, error messages, success messages, required-field UX | ⬜ |
| 4 | `on-page-seo` | Titles, meta descriptions, header hierarchy, internal linking, image alt text | ⬜ |
| 5 | `technical-seo-crawlability` | sitemap.xml, robots.txt, llms.txt, canonical tags, Google Search Console setup | ⬜ |
| 6 | `structured-data-schema` | Organization, LocalBusiness, Service, FAQ, Article schema markup | ⬜ |
| 7 | `local-service-seo` | Location pages, service pages, NAP consistency, tap-to-call, opening hours, local keywords | ⬜ |
| 8 | `trust-and-about-content` | About/story page, visible contact info, credibility signals | ⬜ |
| 9 | `blog-content-seo` | Blog post structure, related content, internal linking within content | ⬜ |
| 10 | `conversion-ctas` | CTA placement above the fold, thank-you pages, modals | ⬜ |
| 11 | `mobile-navigation-ux` | Mobile menu, sticky nav, clickable logo/phone/email | ⬜ |
| 12 | `legal-compliance-pages` | Privacy policy, ToS, cookie consent | ⬜ |
| 13 | `image-performance-optimization` | Compression, lazy loading, Core Web Vitals basics | ⬜ |
| 14 | `accessibility-basics` | Contrast, focus states, semantic HTML, alt text | ⬜ |
| 15 | `contact-page-standards` | Visible email, social links, map, hours | ⬜ |
| 16 | `review-testimonials-social-proof` | Collecting and displaying real reviews/testimonials | ⬜ |
| 17 | `case-studies-portfolio` | Case study and portfolio page structure | ⬜ |
| 18 | `custom-error-pages` | 404/500 pages that keep users on-site | ⬜ |
| 19 | `breadcrumbs-internal-linking` | Breadcrumb nav, internal link structure | ⬜ |
| 20 | `tooltips-microcopy-ux` | Tooltips, helper text, empty states | ⬜ |

## Using a skill

Each `skills/<name>/SKILL.md` follows the standard Claude Code skill format (YAML frontmatter + instructions). Point Claude Code at this repo, or copy an individual skill folder into your project's `.claude/skills/` directory.

## License

TBD before going public.
