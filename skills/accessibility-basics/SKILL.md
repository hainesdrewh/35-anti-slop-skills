---
name: accessibility-basics
description: 'Use this skill whenever building any web page UI, and apply it by default rather than only when a user explicitly mentions accessibility, since these are table-stakes requirements, not optional extras. Also use it when a user asks to "make this accessible," "fix contrast issues," or "add keyboard navigation." Covers contrast, focus states, semantic HTML, alt text, and skip-to-content, the baseline that determines whether a site is usable by people relying on screen readers, keyboard navigation, or who have low vision.'
---

# Accessibility Basics

## Why this matters

Accessibility failures are not an edge case affecting a tiny fraction of users; low vision, color blindness, motor impairments affecting mouse use, and screen-reader use collectively affect a meaningful share of any real audience, and many of the fixes here also improve the experience for everyone (better contrast, clearer focus states, semantic structure that search engines also benefit from). It also carries real legal exposure in some jurisdictions for public-facing sites. This skill overlaps deliberately with [`on-page-seo`](../on-page-seo/SKILL.md) (alt text, heading structure) since good semantic HTML serves both purposes at once.

## Do this

### Contrast

Text needs sufficient contrast against its background: at minimum a 4.5:1 ratio for normal-size body text and 3:1 for large text (WCAG AA). Check actual color combinations with a contrast checker rather than eyeballing it; a light gray on white that looks fine at full brightness on a good monitor often fails this ratio outright.

### Focus states

Every interactive element (links, buttons, form fields) needs a visible focus indicator when navigated to via keyboard, not just a hover state. Never remove the default focus outline (`outline: none`) without providing a clear, visible custom replacement; doing so silently breaks keyboard navigation for every user relying on it.

```css
/* Wrong: removes focus indication with nothing to replace it */
button:focus { outline: none; }

/* Right: custom but still clearly visible */
button:focus-visible { outline: 2px solid var(--focus-color); outline-offset: 2px; }
```

### Semantic HTML

Use actual semantic elements (`<button>` for actions, `<a>` for navigation, `<nav>`, `<header>`, `<main>`, `<footer>`, real heading tags) rather than generic `<div>`s with click handlers and CSS styled to look like the real thing. Semantic elements come with built-in keyboard interaction and screen-reader announcement behavior that a styled `<div>` does not, and would otherwise have to be manually reimplemented and is easy to get wrong.

### Alt text

Covered in depth in [`on-page-seo`](../on-page-seo/SKILL.md); the accessibility angle is the same requirement viewed from the user side: a screen-reader user experiences a missing or generic alt text (`alt="image1"`) as a meaningless announcement where real information should be.

### Keyboard navigation

Every interactive element and flow (menus, modals, forms, carousels) must be fully operable using only a keyboard: Tab to move between elements in a logical order, Enter/Space to activate, Escape to close overlays. Test this directly by navigating the whole page with the mouse untouched, rather than assuming it works because the mouse experience is fine.

### Skip-to-content link

Provide a visually-hidden-until-focused "Skip to main content" link as the very first focusable element on the page, so keyboard users don't have to tab through the entire header/nav on every single page to reach the actual content.

```html
<a href="#main-content" class="skip-link">Skip to main content</a>
<!-- ... header/nav ... -->
<main id="main-content">...</main>
```

```css
.skip-link {
  position: absolute;
  left: -9999px;
}
.skip-link:focus {
  left: 0;
  top: 0;
}
```

## Never do this

- Never remove the focus outline without a clearly visible custom replacement.
- Never build a clickable control as a styled `<div>` with a click handler when a real `<button>` or `<a>` would work.
- Never rely on color alone to convey meaning (an error state shown only by a red border, with no icon or text).
- Never skip testing a page's flows with keyboard-only navigation before considering it done.

## Verification checklist

- [ ] All text meets WCAG AA contrast ratios against its actual background
- [ ] Every interactive element has a visible keyboard focus state
- [ ] Real semantic HTML elements are used for buttons, links, and page structure, not styled generic divs
- [ ] Every meaningful image has real alt text; decorative images use `alt=""`
- [ ] The entire page is operable via keyboard alone, tested directly
- [ ] A working skip-to-content link is present as the first focusable element
