# Build Plan

This is the working plan for the skills in this repo, started at 20, now ~30 after folding in security/backend hardening, anti-abuse, and frontend polish. The repo name (`20-anti-slop-skills`) is being kept as a brand name, not a literal cap; more skills will keep getting added over time. Review it skill-by-skill: nothing gets written in depth until its scope here is settled, so this is the place to push back before time goes into a draft.

## Goal

Every skill should be something a real, experienced developer would nod at, not a generic "best practices" listicle. Each one needs:

- **A clear stance.** Not just "add a favicon" but why sites ship without one, what breaks when they don't, and what "done right" actually looks like (sizes, formats, where it needs to appear).
- **Explicit anti-patterns.** The specific things that make a site read as AI-generated slop, named directly, so the agent recognizes them instead of quietly reproducing them.
- **A verification step.** Something concrete the agent can check (a file that must exist, a tag that must be present, a manual test to run), not just advice to "keep in mind."
- **No em dashes.** Em dashes are one of the most recognizable tells of AI-written text right now, so neither the skills themselves nor the output they produce should use them. This applies to every file in this repo, not just the anti-slop-design skill.

## Depth standard: every skill follows this shape

1. **Frontmatter.** `name` plus a "pushy" `description` that names concrete trigger phrases, per Anthropic's own skill-authoring guidance, so the skill actually fires instead of getting skipped.
2. **Why this matters.** The real-world consequence of getting it wrong (lost conversions, SEO penalty, users bouncing, looking untrustworthy).
3. **Do this.** The concrete, opinionated implementation standard. Code snippets where relevant (e.g. actual `<link rel="canonical">` syntax, actual `robots.txt` format).
4. **Never do this.** Named anti-patterns, especially the AI-slop tells specific to that area.
5. **Verification checklist.** How the agent (or the person reviewing its work) confirms it's actually done, not just claimed done.
6. Bundled `references/` files for anything long enough to blow the 500-line SKILL.md budget (e.g. full schema.org JSON-LD examples, a full pre-launch checklist as a standalone doc).

## The skills

Grouped by theme. Each entry lists the specific checklist items it absorbs from the full ~70-item list so nothing gets dropped or duplicated across skills.

### Design & build judgment

**1. `anti-ai-slop-design`** *(flagship, build first)*
The visual/UX judgment skill. What makes a site read as generic AI output (gradient hero sections, rainbow gradient headline text, the same 3-card feature grid with emoji icons, fake-feeling stock photography, overused glassmorphism/blob shapes, generic sans-serif plus purple/blue gradient palette, meaningless micro-copy, em dashes in the copy) and what a real designer does instead. This is the skill every other skill assumes is already in effect.

**2. `pre-launch-technical-audit`**
The pre-ship punch list: remove horizontal scrolling, find and fix broken links, fix broken buttons, fix mobile overflow, remove placeholder text (lorem ipsum, "Company Name", stock phone numbers), remove unused/dead nav items, fix page titles, add favicons, custom 404 page, fix footer lines, copyright year (and how to keep it from going stale with a dynamic year instead of a hardcoded one).

### Forms, navigation & interaction

**3. `form-ux-feedback`**
Success messages, error messages (inline, specific, not just "something went wrong"), required-field indication, validation timing (on blur vs on submit), password visibility toggle.

**4. `mobile-navigation-ux`**
Mobile menus (hamburger done right), clickable logos (always link home), clickable phone numbers (`tel:`), clickable email (`mailto:`), tap-to-call number placement, mobile optimization generally (touch targets, viewport meta, responsive breakpoints).

**5. `tooltips-microcopy-ux`**
Rich tooltips (accessible, not just `title=""`), modals (focus trapping, escape-to-close, not blocking scroll behind them), confirmation modals for destructive actions, empty states, helper text.

### Core technical SEO

**6. `on-page-seo`**
SEO page titles, meta descriptions, keyword-rich headings (proper H1 through H6 hierarchy, not just bold text), internal links, image alt text.

**7. `technical-seo-crawlability`**
sitemap.xml (as its own real page/file, submitted correctly), robots.txt (custom, not the default deny-all or allow-all), canonical tags, `llms.txt` (the emerging standard for AI-crawler access), Google Search Console setup and verification.

**8. `structured-data-schema`**
Organization schema, LocalBusiness schema, Service schema, FAQ schema, actual JSON-LD, not just "add schema" hand-waving. Bundled reference file with copy-paste-ready templates for each type, plus validation steps in Google's Rich Results Test (schema that's never validated is how broken markup ships).

**9. `breadcrumbs-internal-linking`**
Breadcrumb navigation (markup plus schema), internal linking strategy tying pages together, not just nav but contextual in-content links.

### Local & service-business SEO

**10. `local-service-seo`**
Service pages, location pages, local keywords, opening hours (marked up, not just in a footer image), NAP (name/address/phone) consistency.

### Trust, content & credibility

**11. `trust-and-about-content`**
About page plus real founder/company story (not generic "We are passionate about excellence"), visible contact email, social links.

**12. `review-testimonials-social-proof`**
Customer reviews (real, with schema markup where applicable), author bios (for blog/case-study content), guarantee statements: what makes them credible vs. what makes them read as fake.

**13. `case-studies-portfolio`**
Case studies, before/after galleries, portfolio pages: structure that actually demonstrates results rather than vague claims.

**14. `blog-content-seo`**
Custom blog content strategy (the "5 blog posts minimum before launch" baseline), related content sections, FAQ sections, local-keyword-aware content angles.

### Conversion

**15. `conversion-ctas`**
CTA above the fold, CTA placement and copy throughout a page, thank-you pages (post-form-submission), payment method clarity (clear pricing/payment options, no bait-and-switch).

### Legal & compliance

**16. `legal-compliance-pages`**
Privacy policy, Terms of Service page, cookie consent banner (real one, GDPR/CCPA-aware, not just decorative, covering both the simple banner case and the full consent-management case).

### Performance & accessibility

**17. `image-performance-optimization`**
Image compression, modern formats (WebP/AVIF), lazy loading, responsive `srcset`.

**18. `accessibility-basics`**
Contrast ratios, focus states, semantic HTML, alt text (cross-referenced with on-page-seo), keyboard navigation, skip-to-content link.

**19. `contact-page-standards`**
A real contact page: visible email, phone, map embed, hours, social links. Consolidates the "one clear way to reach you" requirement referenced across several other skills.

**20. `custom-error-pages`**
404 and 500 pages that keep the user oriented (nav intact, search box, link home) instead of a dead end. Separated out from the technical audit because it deserves its own depth (tone, humor calibration, actual recovery paths).

### Frontend polish & engagement

**21. `frontend-polish-microinteractions`**
Dark mode toggle (real one, respects `prefers-color-scheme`, persists choice, no flash-of-wrong-theme), loading states/skeletons (not just spinners), hover states that communicate affordance, scroll progress bar, copy-to-clipboard buttons, sticky header (with scroll-direction hide/show done well), scroll-to-top button, print stylesheet, expandable FAQ interaction pattern, floating contact button, last-updated date display, site search (client-side for small sites, real search index for content-heavy ones).

**22. `analytics-and-attribution-basics`**
UTM tracking conventions, conversion tracking hygiene (what to track, what's noise), keeping analytics privacy-respecting (cross-references `legal-compliance-pages`).

### Planning (build this before the others fire)

**23. `project-scoping-and-prd`**
Define the ICP (ideal customer profile) and value proposition before generating any copy or layout, write a lightweight PRD, export it to markdown. Exists because most "AI slop" isn't a technical failure, it's building generic output because nobody defined who the site is actually for. Other skills should treat this PRD as an input when it exists.

### Backend security & hardening

Everything here assumes the agent is not just decorating a frontend. It's shipping something with real user data, auth, or paid API usage behind it, and that thing needs to survive contact with the internet.

**24. `secrets-and-env-hardening`**
`.env` hygiene (never commit it, always in `.gitignore`), no API keys or secrets in client-side/frontend code, purging secrets that already leaked into git history, separating public-safe keys (e.g. publishable Stripe key) from private ones, key rotation after any suspected leak.

**25. `auth-and-session-security`**
Password hashing (bcrypt/argon2, never plaintext or raw MD5/SHA1), secure session cookies (`HttpOnly`, `Secure`, `SameSite`), CSRF tokens on state-changing requests, invalidating all sessions on password change, expiring password-reset links (short TTL, single-use), preventing user enumeration (identical responses for "email not found" vs "wrong password"), locking accounts after repeated failed logins, rate-limiting login and password-reset endpoints.

**26. `database-access-control`**
Row-level security (RLS) so users can only read/write their own rows, restricting database roles/permissions to least privilege, locking record access server-side (never trust a client-supplied user ID or record ID without an ownership check), blocking mass-assignment/field tampering (explicit allow-lists for what a client can update), encrypting sensitive fields at rest.

**27. `input-validation-and-injection-defense`**
Validate all input server-side (never trust client-side validation alone), parameterized queries/prepared statements (never string-concatenated SQL), escaping user-generated content before rendering (XSS defense), sanitizing input before storing it (not just before displaying it), and, specific to AI-backed features, defending against prompt injection in user-supplied text that reaches an LLM call.

**28. `api-abuse-and-rate-limiting`**
Rate limiting on every public endpoint (not just login), capping AI/LLM usage per user so nobody can drain your API credits, limiting request body/payload size, bot protection on forms and signup (CAPTCHA/Turnstile or equivalent), and specifically blocking scripted signup/login spam and free-tier credit farming. This is the "people can't just hit refresh on the free plan" skill.

**29. `file-upload-and-payment-integrity`**
Whitelisting upload file types and sizes (extension plus MIME plus magic-byte check, not just extension), never trusting a client-submitted price or total (compute and enforce pricing server-side), verifying payment webhook signatures before trusting a "payment succeeded" event.

**30. `transport-headers-and-monitoring`**
Forcing HTTPS everywhere, HSTS, a locked-down CORS policy (no `*` with credentials), standard security headers (CSP, `X-Frame-Options`, `X-Content-Type-Options`, `Referrer-Policy`), disabling directory listing, removing/renaming default admin routes, dependency vulnerability scanning as part of the build, and logging security-relevant events (failed logins, permission denials) so an incident is detectable at all.

## Coverage check against your original list

Every item you listed maps to exactly one skill above, flagged here so you can catch anything that got merged in a way you don't like:

- horizontal scrolling, broken links, broken buttons, mobile overflow, placeholder text, unused nav, page titles, favicons, 404 pages, footer lines, copyright year -> **2**
- mobile menus, clickable logo/phone/email, tap-to-call, mobile optimize -> **4**
- success/error messages -> **3**
- tooltips, modals -> **5**
- SEO titles, meta descriptions, keyword headings, internal links, alt text -> **6**
- sitemap.xml, robots.txt, canonical tags, llms.txt, Search Console -> **7**
- organization/local business/service/FAQ schema -> **8**
- breadcrumbs -> **9**
- service pages, location pages, local keywords, opening hours -> **10**
- about page plus story, visible contact email, social links -> **11**
- customer reviews, author bios, guarantee statement -> **12**
- case studies, before/after gallery -> **13**
- 5 blog posts, related content, FAQ section, custom blog content -> **14**
- CTA above the fold, thank-you page, clear payment method -> **15**
- privacy policy, ToS, cookie consent -> **16**
- compress images -> **17**
- (accessibility wasn't explicitly on your list but is implied by "mobile optimize" / "clickable" items and is table-stakes for a non-slop site) -> **18**
- visible contact email / social links (page) -> **19** (cross-referenced with 11)
- custom 404 -> also **20** (deeper treatment than the audit checklist version in **2**)

## Build order

1. `anti-ai-slop-design`: everything else assumes this baseline
2. `pre-launch-technical-audit`: highest item-density, most universally applicable
3. `secrets-and-env-hardening`, `auth-and-session-security`, `database-access-control`, `input-validation-and-injection-defense`, `api-abuse-and-rate-limiting`, `file-upload-and-payment-integrity`, `transport-headers-and-monitoring`: the security set, built as its own block since it's the highest-stakes category (a slop-but-secure site is annoying; a good-looking-but-hacked site is a disaster)
4. Remaining skills, roughly in the order listed above, one at a time with your review in between

## Resolved

Schema markup (`structured-data-schema`) will include Rich Results Test validation steps, not just JSON-LD templates. Confirmed.

## Future expansion (after the current ~30 are finished)

- Grow toward 50 to 100 skills total, covering both website and mobile app building, for every common project type, not just marketing sites.
- Full-stack depth skills to add: deployment/CI safety (env parity, zero-downtime deploys, rollback plans), database migration safety (no destructive migration without a backup/rollback path), a testing-before-ship skill (what actually needs a test vs. what doesn't), and observability/error-monitoring beyond the security-event logging already in `transport-headers-and-monitoring`.
- A new "industry-specific visual execution" skill, a companion to `anti-ai-slop-design`, covering how to build genuinely picture-perfect sites per industry/vertical: e.g. a landscaping site with real cinematic background video/imagery of actual work, a clean minimalist style for a professional-services site, and other vertical-specific visual treatments that go beyond generic anti-slop rules into "what does excellent actually look like for this specific kind of business."
- Mobile app equivalents of the web-focused skills where the concerns transfer (navigation patterns, forms, security, performance) plus mobile-specific ones (app store listing quality, permissions requests done right, offline states, push notification hygiene).

None of this gets built until the current ~30-skill batch is complete and reviewed.
