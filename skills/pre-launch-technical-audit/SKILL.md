---
name: pre-launch-technical-audit
description: 'Run this skill before calling any website "done," "finished," "ready to launch," or "ready to deploy," and whenever a user asks to "audit the site," "check for issues," "find bugs," or "review before going live." It catches the specific, boring, embarrassing defects that ship in AI-generated and rushed sites: horizontal scroll on mobile, broken links, dead buttons, leftover placeholder text, framework-default favicons and page titles, a generic 404, and a stale copyright year. These are cheap to fix and expensive to be caught by a visitor, so treat this as mandatory before declaring launch-readiness, not an optional nice-to-have pass.'
---

# Pre-Launch Technical Audit

## Why this matters

Each item below is individually small. Together, they are the difference between a site that reads as "someone actually checked this before shipping" and one that reads as "this was generated and never opened on a phone." A visitor does not need to consciously notice a broken link to lose trust; a handful of these defects compound into a general sense that the site (and the business behind it) is not to be trusted with anything more important, like a payment or a contact form submission. Run this after [`anti-ai-slop-design`](../anti-ai-slop-design/SKILL.md), as a check on execution, not a substitute for it.

## Do this

### Horizontal scrolling

Test at 320px viewport width (iPhone SE), not just a resized desktop browser window; that width surfaces overflow that wider "mobile" breakpoints hide.

- Set `box-sizing: border-box` globally so padding and borders don't push elements past their intended width.
- Every image, video, and iframe needs `max-width: 100%; height: auto;` unless intentionally full-bleed.
- Watch for fixed pixel widths on containers, negative margins that extend past the viewport edge, and `100vw` used inside a container that already has padding (`100vw` ignores the scrollbar and parent padding, and reliably causes a few pixels of horizontal overflow).
- To find the exact offending element, run this in the browser console: it outlines every element wider than the viewport in red.

```js
document.querySelectorAll('*').forEach(el => {
  if (el.scrollWidth > document.documentElement.clientWidth) {
    el.style.outline = '2px solid red';
    console.log(el);
  }
});
```

### Broken links

Check every internal link, outbound link, and anchor (`#section`) link, not just the main nav. Broken anchors (linking to a `#section` that no longer exists after a content edit) are the most commonly missed case.

- Crawl the whole site with a link checker rather than clicking through manually. `npx linkinator https://example.com --recurse` or `lychee` (Rust-based, fast, handles large sites) both work well and report every dead link with its source page.
- Confirm every `tel:` and `mailto:` link has a real, correctly formatted number/address (see [`mobile-navigation-ux`](../mobile-navigation-ux/SKILL.md) and [`contact-page-standards`](../contact-page-standards/SKILL.md)), not just that it's clickable.
- Check outbound links open correctly and don't point to a competitor by copy-paste accident from a template.

### Broken buttons

- Every button and link needs a real destination or handler; a button with no `href`, no `onClick`, and no form association is a dead click waiting to be found by a real visitor.
- Check disabled states: a submit button left permanently disabled by leftover development logic, or a button that only becomes clickable after a form is fully valid but gives no indication why it's currently disabled (see [`form-ux-feedback`](../form-ux-feedback/SKILL.md)).
- Check for overlapping elements (a decorative absolutely-positioned element sitting on top of a real button, intercepting clicks) by opening dev tools and confirming the button is actually the topmost element at its coordinates.

### Mobile overflow

Distinct from horizontal scrolling: this is content that's technically contained but unusable on a small screen. Check tables (should scroll within their own container, not force the whole page wider), long unbreakable strings like URLs or emails (`word-break: break-word` or `overflow-wrap: anywhere`), and fixed-width modals/cards that don't shrink below their pixel width on a narrow screen.

### Placeholder text

Search the entire codebase and rendered output for these before launch:

- `lorem ipsum`, `Company Name`, `Your Company`, `Business Name`, `example@example.com`, `555-555-5555` / `123-456-7890`, `#` as an `href`, `TODO`, `FIXME`, `Lorem`, `John Doe`, `Sample Text`, generic alt text like `alt="image"` or `alt=""` on meaningful images.
- Run a repo-wide search for these terms before every deploy: `grep -rEi "lorem ipsum|your company|example\.com|555-555|todo:|fixme|john doe" .` (adjust for the actual project's exclusions like `node_modules`).

### Unused/dead nav

Every nav item should point to a real, finished page. Remove links to pages that were scaffolded but never built, duplicate links to the same destination under different labels, and nav items copied from a template that don't apply to this business (a "Careers" link with no jobs, a "Blog" link to an empty blog).

### Page titles

- Every page needs a unique, real `<title>`. Framework defaults left in place (`React App`, `Document`, `Vite + React`, `create-next-app`) are one of the fastest ways to reveal a site was never actually finished.
- No two pages should share an identical title; each should describe that specific page (see [`on-page-seo`](../on-page-seo/SKILL.md) for the SEO-specific requirements on top of this baseline).

### Favicon

- A real favicon is required, not the framework's default logo (Vite's, Next.js's, or Create React App's default icon left in `public/`).
- Minimum set: `favicon.ico` (32x32, for legacy support), an SVG or PNG favicon for modern browsers, and an `apple-touch-icon.png` (180x180) for iOS home-screen saves. Verify all are actually linked in `<head>`, not just present as unused files in the public directory.

### Custom 404 page

The framework's default 404 (a bare "404 | This page could not be found" on a white screen) is a dead end that looks unfinished. See [`custom-error-pages`](../custom-error-pages/SKILL.md) for the full treatment; at minimum for this audit, confirm a branded 404 exists and that navigating to a nonexistent URL actually serves it (some hosting configs silently fall back to the framework default despite a custom page existing in the codebase).

### Footer lines

- Every footer link must go somewhere real; `#` placeholder hrefs on social icons are a common leftover.
- Confirm legal links (privacy policy, terms) are present and not dead if the business has them (see [`legal-compliance-pages`](../legal-compliance-pages/SKILL.md)).
- Check for a stray leftover "Powered by [template/builder name]" or "Made by [agency]" credit line that wasn't actually authorized by the site owner.

### Copyright year

Never hardcode the year as a static string; it goes stale the moment the calendar turns and is a small but visible sign that a site was set up once and forgotten. Generate it dynamically:

```js
// client-rendered
<span>&copy; {new Date().getFullYear()} Business Name</span>
```

```html
<!-- build-time (static sites without JS) -->
<!-- inject the year at build time from the build tool/CI, not by hand -->
```

## Never do this

- Ship with any item above unchecked because "it's a small thing." These are exactly the small things a real reviewer (or a skeptical customer) notices first.
- Fix these issues only on desktop. Most of this list (overflow, broken buttons, mobile nav) is invisible on a wide desktop viewport and only appears at real mobile widths.
- Treat a passing visual scan as sufficient for broken links; links can look correct and still 404. Actually crawl the site.

## Verification checklist

- [ ] Tested at 320px width, not just a resized desktop window
- [ ] Ran a full link crawl (not manual clicking) with zero unexpected 404s or dead anchors
- [ ] Every button/link has a real destination or handler; none intercepted by an overlapping element
- [ ] No content forces horizontal scroll or overflows its container on mobile
- [ ] Repo-wide placeholder-text search returns nothing
- [ ] Every nav item resolves to a real, finished page
- [ ] Every page has a unique, non-default title
- [ ] Favicon set is complete (`favicon.ico`, modern icon, `apple-touch-icon.png`) and actually linked in `<head>`
- [ ] Navigating to a nonexistent URL serves the custom 404, not the framework default
- [ ] Every footer link resolves; no `#` placeholders remain
- [ ] Copyright year is generated dynamically, not hardcoded

See [references/full-checklist.md](references/full-checklist.md) for a copy-paste version of this checklist to run per project.
