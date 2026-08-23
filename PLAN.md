# Build Plan

This is the working plan for the 20 skills in this repo. Review it skill-by-skill — nothing gets written in depth until its scope here is settled, so this is the place to push back before time goes into a draft.

## Goal

Every skill should be something a real, experienced developer would nod at — not a generic "best practices" listicle. Each one needs:

- **A clear stance.** Not just "add a favicon" but why sites ship without one, what breaks when they don't, and what "done right" actually looks like (sizes, formats, where it needs to appear).
- **Explicit anti-patterns.** The specific things that make a site read as AI-generated slop, named directly, so the agent recognizes them instead of quietly reproducing them.
- **A verification step.** Something concrete the agent can check (a file that must exist, a tag that must be present, a manual test to run) — not just advice to "keep in mind."

## Depth standard — every skill follows this shape

1. **Frontmatter** — `name` + a "pushy" `description` that names concrete trigger phrases, per Anthropic's own skill-authoring guidance, so the skill actually fires instead of getting skipped.
2. **Why this matters** — the real-world consequence of getting it wrong (lost conversions, SEO penalty, users bouncing, looking untrustworthy).
3. **Do this** — the concrete, opinionated implementation standard. Code snippets where relevant (e.g. actual `<link rel="canonical">` syntax, actual `robots.txt` format).
4. **Never do this** — named anti-patterns, especially the AI-slop tells specific to that area.
5. **Verification checklist** — how the agent (or the person reviewing its work) confirms it's actually done, not just claimed done.
6. Bundled `references/` files for anything long enough to blow the 500-line SKILL.md budget (e.g. full schema.org JSON-LD examples, a full pre-launch checklist as a standalone doc).

## The 20 skills

Grouped by theme. Each entry lists the specific checklist items it absorbs from the full ~70-item list so nothing gets dropped or duplicated across skills.

### Design & build judgment

**1. `anti-ai-slop-design`** *(flagship — build first)*
The visual/UX judgment skill. What makes a site read as generic AI output (gradient hero sections, rainbow gradient headline text, the same 3-card feature grid with emoji icons, fake-feeling stock photography, overused glassmorphism/blob shapes, generic sans-serif + purple/blue gradient palette, meaningless micro-copy) and what a real designer does instead. This is the skill every other skill assumes is already in effect.

**2. `pre-launch-technical-audit`**
The pre-ship punch list: remove horizontal scrolling, find and fix broken links, fix broken buttons, fix mobile overflow, remove placeholder text (lorem ipsum, "Company Name", stock phone numbers), remove unused/dead nav items, fix page titles, add favicons, custom 404 page, fix footer lines, copyright year (and how to keep it from going stale — dynamic year, not hardcoded).

### Forms, navigation & interaction

**3. `form-ux-feedback`**
Success messages, error messages (inline, specific, not just "something went wrong"), required-field indication, validation timing (on blur vs on submit).

**4. `mobile-navigation-ux`**
Mobile menus (hamburger done right), clickable logos (always link home), clickable phone numbers (`tel:`), clickable email (`mailto:`), tap-to-call number placement, mobile optimization generally (touch targets, viewport meta, responsive breakpoints).

**5. `tooltips-microcopy-ux`**
Rich tooltips (accessible, not just `title=""`), modals (focus trapping, escape-to-close, not blocking scroll behind them), empty states, helper text.

### Core technical SEO

**6. `on-page-seo`**
SEO page titles, meta descriptions, keyword-rich headings (proper H1–H6 hierarchy, not just bold text), internal links, image alt text.

**7. `technical-seo-crawlability`**
sitemap.xml (as its own real page/file, submitted correctly), robots.txt (custom, not the default deny-all or allow-all), canonical tags, `llms.txt` (the emerging standard for AI-crawler access), Google Search Console setup and verification.

**8. `structured-data-schema`**
Organization schema, LocalBusiness schema, Service schema, FAQ schema — actual JSON-LD, not just "add schema" hand-waving. Bundled reference file with copy-paste-ready templates for each type.

**9. `breadcrumbs-internal-linking`**
Breadcrumb navigation (markup + schema), internal linking strategy tying pages together (not just nav — contextual in-content links).

### Local & service-business SEO

**10. `local-service-seo`**
Service pages, location pages, local keywords, opening hours (marked up, not just in a footer image), NAP (name/address/phone) consistency.

### Trust, content & credibility

**11. `trust-and-about-content`**
About page + real founder/company story (not generic "We are passionate about excellence"), visible contact email, social links.

**12. `review-testimonials-social-proof`**
Customer reviews (real, with schema markup where applicable), author bios (for blog/case-study content), guarantee statements — what makes them credible vs. what makes them read as fake.

**13. `case-studies-portfolio`**
Case studies, before/after galleries, portfolio pages — structure that actually demonstrates results rather than vague claims.

**14. `blog-content-seo`**
Custom blog content strategy (the "5 blog posts minimum before launch" baseline), related content sections, FAQ sections, local-keyword-aware content angles.

### Conversion

**15. `conversion-ctas`**
CTA above the fold, CTA placement and copy throughout a page, thank-you pages (post-form-submission), payment method clarity (clear pricing/payment options, no bait-and-switch).

### Legal & compliance

**16. `legal-compliance-pages`**
Privacy policy, Terms of Service page, cookie consent banner (real one, GDPR/CCPA-aware, not just decorative).

### Performance & accessibility

**17. `image-performance-optimization`**
Image compression, modern formats (WebP/AVIF), lazy loading, responsive `srcset`.

**18. `accessibility-basics`**
Contrast ratios, focus states, semantic HTML, alt text (cross-referenced with on-page-seo), keyboard navigation.

**19. `contact-page-standards`**
A real contact page: visible email, phone, map embed, hours, social links — consolidating the "one clear way to reach you" requirement referenced across several other skills.

**20. `custom-error-pages`**
404 and 500 pages that keep the user oriented (nav intact, search box, link home) instead of a dead end — separated out from the technical audit because it deserves its own depth (tone, humor calibration, actual recovery paths).

## Coverage check against your original list

Every item you listed maps to exactly one skill above — flagged here so you can catch anything that got merged in a way you don't like:

- horizontal scrolling, broken links, broken buttons, mobile overflow, placeholder text, unused nav, page titles, favicons, 404 pages, footer lines, copyright year → **2**
- mobile menus, clickable logo/phone/email, tap-to-call, mobile optimize → **4**
- success/error messages → **3**
- tooltips, modals → **5**
- SEO titles, meta descriptions, keyword headings, internal links, alt text → **6**
- sitemap.xml, robots.txt, canonical tags, llms.txt, Search Console → **7**
- organization/local business/service/FAQ schema → **8**
- breadcrumbs → **9**
- service pages, location pages, local keywords, opening hours → **10**
- about page + story, visible contact email, social links → **11**
- customer reviews, author bios, guarantee statement → **12**
- case studies, before/after gallery → **13**
- 5 blog posts, related content, FAQ section, custom blog content → **14**
- CTA above the fold, thank-you page, clear payment method → **15**
- privacy policy, ToS, cookie consent → **16**
- compress images → **17**
- (accessibility wasn't explicitly on your list but is implied by "mobile optimize" / "clickable" items and is table-stakes for a non-slop site) → **18**
- visible contact email / social links (page) → **19** (cross-referenced with 11)
- custom 404 → also **20** (deeper treatment than the audit checklist version in **2**)

## Build order

1. `anti-ai-slop-design` — everything else assumes this baseline
2. `pre-launch-technical-audit` — highest item-density, most universally applicable
3. Remaining 18, roughly in the order listed above, one at a time with your review in between

## Open question for you

Should schema markup (`structured-data-schema`) ship as JSON-LD templates only, or also include the step-by-step for validating them in Google's Rich Results Test? Leaning toward including validation since "add schema" that's never checked is a classic way to ship broken markup.
