---
name: mobile-navigation-ux
description: 'Use this skill whenever building site navigation, a header, or a mobile menu, and whenever the site includes a phone number, email address, or logo in the header/footer. Also use it when a user asks to "add a mobile menu," "make the nav responsive," "add a hamburger menu," or "make the phone number clickable," and whenever reviewing a site''s mobile experience. It covers the specific interaction details, tap targets, clickable contact info, a working hamburger menu, that separate a genuinely mobile-usable site from one that merely resizes without breaking.'
---

# Mobile Navigation UX

## Why this matters

A large share of traffic to most sites, especially local-service and e-commerce sites, is mobile, often the majority. A nav that technically fits on a small screen but is awkward to use (tiny tap targets, a phone number that isn't tappable, a menu that doesn't close properly) creates friction at the exact moment a visitor is trying to take action, which for a local business is very often "call them right now."

## Do this

### Mobile menu (hamburger done right)

- Use a real, recognizable hamburger icon (three lines) or an explicit "Menu" label, not an ambiguous custom icon.
- Open as a full-screen overlay or slide-in panel with a visible, easy-to-tap close control, not a tiny dropdown that's hard to dismiss.
- Trap focus within the open menu for keyboard/screen-reader users, and close it on: tapping the close control, tapping outside the menu, pressing Escape, and navigating to a new page (a menu that stays open after navigation is a common bug).
- Ensure tap targets are at least 44x44px (Apple's and most accessibility guidelines' minimum), with adequate spacing between adjacent links so a large thumb doesn't mis-tap the neighboring item.

### Clickable logo

The logo in the header should always link to the homepage, on every page including the homepage itself (linking to itself is harmless and expected; omitting the link entirely is the actual mistake). This is one of the most universally expected navigation conventions on the web.

### Clickable phone number

Any phone number displayed anywhere on the site (header, footer, contact page) should be a real `tel:` link, not just styled text that looks clickable but isn't.

```html
<a href="tel:+18175550142">(817) 555-0142</a>
```

Use the full international format in the `href` (with country code) even if the display text uses a friendlier local format; this ensures it dials correctly regardless of the visitor's phone settings.

### Clickable email

Any displayed email address should be a `mailto:` link.

```html
<a href="mailto:hello@example.com">hello@example.com</a>
```

For a business that gets meaningful volume through this, consider whether a `mailto:` link (which just opens the visitor's mail client, if they have one configured) or a contact form is actually the better primary path; either way, if an email address is shown as text, it must be clickable.

### Tap-to-call placement

For any business where phone contact is a primary conversion path (most local-service businesses), place a visible, tappable phone number or a persistent "Call Now" button within easy thumb reach on mobile, not only buried in the footer. A sticky header or floating action button with the phone number is a common, effective pattern (see [`frontend-polish-microinteractions`](../frontend-polish-microinteractions/SKILL.md) for the floating-button treatment).

### Mobile optimization generally

- Set the viewport meta tag correctly: `<meta name="viewport" content="width=device-width, initial-scale=1">`. Its absence or a hardcoded width breaks responsive layout entirely on real devices.
- Use real responsive breakpoints tested at actual device widths (320px, 375px, 414px, 768px), not just a browser window dragged to an arbitrary size.
- Avoid hover-dependent functionality (a menu that only opens on hover) since touch devices have no hover state; every interactive element must work with a tap alone.

## Never do this

- Never style a phone number or email to look clickable without actually making it a `tel:`/`mailto:` link.
- Never ship a mobile menu that traps the user (no visible way to close it) or leaves scroll locked on the body behind it indefinitely.
- Never rely on hover for any functionality that needs to work on mobile.
- Never leave the logo unlinked in the header.

## Verification checklist

- [ ] Logo links to the homepage from every page
- [ ] Every displayed phone number is a working `tel:` link with the full international format in the `href`
- [ ] Every displayed email address is a working `mailto:` link
- [ ] Mobile menu opens/closes reliably (tap outside, close button, Escape, and on navigation) with no scroll-lock left behind
- [ ] All tap targets are at least 44x44px with adequate spacing
- [ ] Viewport meta tag is present and correct
- [ ] No functionality depends solely on hover
- [ ] Phone contact (for phone-reliant businesses) is reachable within one tap from anywhere on the mobile site
