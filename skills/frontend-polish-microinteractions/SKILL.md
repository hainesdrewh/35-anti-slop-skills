---
name: frontend-polish-microinteractions
description: 'Use this skill whenever building UI-level polish features: dark mode, loading states, hover effects, a sticky header, a scroll-to-top button, a scroll progress bar, copy-to-clipboard buttons, a print stylesheet, an expandable FAQ, a floating contact button, a last-updated date, or site search. Also use it when a user asks to "add dark mode," "add a search bar," "improve the loading state," or "add micro-interactions." These are individually small but collectively separate a polished, cared-for site from one that feels merely functional.'
---

# Frontend Polish and Microinteractions

## Why this matters

None of these individually make or break a site, but a site that gets several of them right reads as genuinely cared-for, while a site missing all of them (or implementing them poorly, a dark-mode toggle that flashes the wrong theme on load, a sticky header that overlaps content) reads as rushed even if the core content is solid. Implement each with the same restraint principle as [`anti-ai-slop-design`](../anti-ai-slop-design/SKILL.md): purposeful and well-executed, not decorative for its own sake.

## Do this

### Dark mode toggle

Respect the system preference by default (`prefers-color-scheme`), let the user override it explicitly, and persist their choice (localStorage) so it doesn't reset every visit. Set the theme before first paint (inline script in `<head>`, not a client-side effect that runs after render) to avoid a visible flash of the wrong theme on load.

```html
<script>
  const stored = localStorage.getItem('theme');
  const theme = stored || (matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light');
  document.documentElement.dataset.theme = theme;
</script>
```

### Loading states

Use skeleton placeholders that mirror the actual content's shape for anything that takes a noticeable moment to load, rather than a generic spinner with no indication of what's coming; this reduces the perceived wait and prevents layout shift when the real content arrives.

### Hover states

Hover effects should communicate genuine affordance (this is clickable, this reveals more) rather than being applied uniformly to every element regardless of whether it needs one (see the "lift + shadow on everything" anti-pattern in [`anti-ai-slop-design`](../anti-ai-slop-design/SKILL.md)). Keep hover-only information also available on focus and tap, since hover doesn't exist on touch devices.

### Scroll progress bar

A thin bar at the top of the viewport reflecting scroll position through the page is genuinely useful for long-form content (a blog post, documentation) and out of place on a short marketing page; use it where the content length actually warrants it.

### Copy-to-clipboard buttons

For any content a user is likely to want to copy verbatim (a code snippet, a phone number, an API key, a discount code), include a one-click copy button with a clear success confirmation (a brief "Copied!" state), rather than expecting manual text selection.

### Sticky header

If the header sticks on scroll, make sure it never overlaps content below it (account for its height in scroll-margin/padding on anchor targets) and consider a scroll-direction behavior (hide on scroll-down, reveal on scroll-up) for long pages so it doesn't permanently consume vertical space on mobile.

### Scroll-to-top button

Appear only after the user has scrolled a meaningful distance (not immediately on page load), and scroll smoothly rather than jumping instantly.

### Print stylesheet

For content users realistically print (invoices, recipes, articles, directions), provide a `@media print` stylesheet that hides navigation, ads, and decorative elements, and ensures text remains legible in black-and-white.

### Expandable FAQ

Use a real disclosure pattern (`<details>`/`<summary>` natively handles this accessibly, or a custom accordion with proper `aria-expanded` state) so screen readers correctly announce expanded/collapsed state, not a purely visual toggle with no semantic indication.

### Floating contact button

A persistent floating action button (call, chat, or contact) can genuinely help conversion for a business where immediate contact matters, but must never obscure content or another interactive element, especially on mobile where screen space is limited; test it doesn't overlap the exact area a user needs to tap next.

### Last-updated date

For content where freshness matters to the reader (a blog post, pricing information, a changelog), show a real, accurate last-updated date, generated from actual content-modification data, not left stale after edits.

### Site search

For a small site, a simple client-side search over page titles/headings is sufficient. For a content-heavy site (many blog posts, a large product catalog), use a real search index (Algolia, a self-hosted solution, or the platform's built-in search) rather than a naive linear scan that won't scale or won't rank results meaningfully.

## Never do this

- Never let a theme toggle cause a visible flash of the wrong theme on load.
- Never apply loading spinners or hover effects uniformly without considering whether each specific element needs one.
- Never let a sticky header overlap the content or a jump-to anchor target below it.
- Never build a visually-toggling FAQ or accordion with no underlying semantic/ARIA state for screen readers.

## Verification checklist

- [ ] Dark mode respects system preference by default, persists user choice, and never flashes the wrong theme on load
- [ ] Loading states use content-shaped skeletons where feasible, not a generic spinner alone
- [ ] Hover-only information is also available via focus/tap for touch devices
- [ ] Sticky header never overlaps content or anchor targets
- [ ] Scroll-to-top only appears after meaningful scroll, and scrolls smoothly
- [ ] Copy buttons give clear success confirmation
- [ ] Expandable FAQ/accordion uses real semantic disclosure, not a purely visual toggle
- [ ] Last-updated dates are accurate and reflect real content changes
- [ ] Site search is appropriately scaled to the site's actual content volume
