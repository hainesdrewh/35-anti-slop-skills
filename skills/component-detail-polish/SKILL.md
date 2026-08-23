---
name: component-detail-polish
description: 'Use this skill whenever building or styling any interactive component: buttons, inputs, cards, icons, links. Also use it when a user says a UI "feels unfinished," "feels janky," or asks to "polish the components." Apply it by default for every component, not only on request, since most components only ever get a hover state designed and every other real-world state (active, disabled, focus, loading) is left at browser defaults, which is one of the more common tells that a UI wasn''t fully finished.'
---

# Component Detail Polish

## Why this matters

Most attention during a build goes to what a component looks like in its default and hover states, since those are what's visible while designing. Every other state a component can actually be in (pressed, disabled, loading, focused via keyboard) gets left at browser defaults or skipped entirely, and those are exactly the states a real user hits: clicking a button, tabbing through a form, waiting on a slow network. A UI where only the "designed" state looks intentional and everything else looks like an afterthought reads as unfinished the moment a real user does anything beyond hovering.

## Do this

### Design every real interactive state, not just hover

- **Default**: the resting state.
- **Hover**: for pointer devices only; doesn't exist on touch, so nothing essential should depend on it.
- **Active/pressed**: a visible, immediate response the instant a button is pressed, not just after release. Commonly a slight scale-down or darkened fill.
- **Focus**: a visible indicator for keyboard navigation, distinct from hover (see [`accessibility-basics`](../accessibility-basics/SKILL.md)).
- **Disabled**: visually distinct (reduced opacity, muted color) and with `cursor: not-allowed`, communicating why it can't be interacted with, not just silently doing nothing when clicked.
- **Loading**: for anything that triggers an async action, a visible in-progress state (spinner, skeleton, disabled state with a label change), not a button that appears to do nothing while a request is in flight.

```css
.btn {
  transition: transform 0.1s ease, background-color 0.15s ease;
}
.btn:hover { background-color: var(--btn-hover); }
.btn:active { transform: scale(0.97); }
.btn:disabled { opacity: 0.5; cursor: not-allowed; }
.btn:focus-visible { outline: 2px solid var(--focus-color); outline-offset: 2px; }
```

### Systematize border-radius, shadow, and stroke-width

Pick a small set of radius values (e.g. `--radius-sm`, `--radius-md`, `--radius-lg`) and a small set of shadow/elevation levels, and apply them consistently based on a component's actual role (a card vs. a button vs. a modal), rather than each component getting a radius or shadow value chosen independently. The same applies to icons: one stroke-width and one visual weight across the whole icon set, not a mix of icon libraries with different default weights.

```css
:root {
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 16px;
  --shadow-1: 0 1px 3px rgba(0,0,0,0.08);
  --shadow-2: 0 4px 12px rgba(0,0,0,0.12);
}
```

### Match cursor to actual affordance

`cursor: pointer` on anything clickable, `cursor: not-allowed` on disabled controls, `cursor: default` (not `pointer`) on non-interactive elements that might otherwise look clickable (a card that only has a nested link, not the whole card, shouldn't show a pointer cursor over its non-link areas).

### Give inputs a real invalid and filled state

Beyond the error-message handling in [`form-ux-feedback`](../form-ux-feedback/SKILL.md), the input itself should look visually different when invalid (border color, subtle background tint) versus empty versus filled, so state is communicated at a glance, not only through a separate error message below it.

### Handle image loading states

An image that pops in abruptly once loaded, especially one that's large or above the fold, is a small jolt. Use a low-quality placeholder, a solid background color matched to the image's dominant tone, or a skeleton shape while loading, so the layout doesn't shift and the load doesn't feel abrupt (see also [`image-performance-optimization`](../image-performance-optimization/SKILL.md) for dimension-based layout shift prevention).

## Never do this

- Never ship a button, input, or link with only a hover state designed and every other state left at the browser default.
- Never let a disabled control look identical to an enabled one, or an enabled one look identical to a disabled one.
- Never mix icon sets with different stroke-widths or visual weights on the same page.
- Never show `cursor: pointer` on an element that isn't actually clickable, or the default cursor on one that is.
- Never leave an async action's button with no visible loading state while a request is in flight.

## Verification checklist

- [ ] Every interactive component has a designed default, hover, active, focus, and (where applicable) disabled and loading state
- [ ] Border-radius and shadow values are drawn from a small, consistent system, not chosen per component
- [ ] Icons across the site share one stroke-width and visual weight
- [ ] Cursor styles match actual affordance on every element, not just links and buttons
- [ ] Form inputs visually communicate invalid/filled state, not only through a separate error message
- [ ] Images use a placeholder or skeleton while loading rather than popping in abruptly
