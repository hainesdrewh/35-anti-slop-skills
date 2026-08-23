---
name: motion-system
description: 'Use this skill whenever adding any animation, transition, or hover effect to a site, and whenever a user asks to "add an animation," "make it feel smoother," or says transitions "feel inconsistent" or "feel janky." Apply it by default whenever writing any CSS transition or animation, not only when motion is explicitly requested, since an inconsistent, ungoverned set of animation timings across a site is a subtle but real tell, distinct from having too much or too little motion.'
---

# Motion System

## Why this matters

Individual animations are usually judged one at a time while building, so it's easy to end up with a hover transition here at 200ms, a modal fade there at 400ms, and a card lift somewhere else at 150ms, each reasonable in isolation but collectively inconsistent in a way a user feels without being able to name. A coherent motion system (one small set of easing curves and durations, applied by role rather than invented per component) is what makes motion feel like part of one designed product instead of a pile of individually-added effects. This is distinct from [`frontend-polish-microinteractions`](../frontend-polish-microinteractions/SKILL.md), which covers specific UI patterns like dark-mode toggles and scroll-to-top buttons; this skill covers the underlying timing and easing rules that every one of those patterns should draw from.

## Do this

### Define a small set of durations and easing curves

```css
:root {
  --ease-standard: cubic-bezier(0.2, 0, 0, 1);
  --ease-decelerate: cubic-bezier(0, 0, 0, 1);
  --duration-fast: 100ms;
  --duration-base: 200ms;
  --duration-slow: 350ms;
}
```

Assign durations by role, not by feel in the moment: micro-interactions (button press, checkbox toggle) use `--duration-fast`; standard UI transitions (hover states, dropdown open) use `--duration-base`; larger movements (modal entrance, page-level transitions) use `--duration-slow`. A new component's transition duration should be chosen by matching its role to this list, not by picking whatever number looks good in isolation.

### Scale duration to distance and size

A small element moving a short distance should animate faster than a large element moving a long distance; using the same fixed duration for both makes the small movement feel sluggish and the large one feel abrupt. This doesn't require a precise formula, just a sanity check: does this duration feel proportional to what's actually moving?

### Ease out for things entering, ease in for things leaving

Elements appearing or moving into view generally feel most natural decelerating into place (ease-out); elements leaving can accelerate away (ease-in). A linear or default-eased transition on an entrance is one of the more common small tells that motion wasn't considered deliberately.

### Respect reduced motion everywhere motion exists, not just on the obvious one

It's common to remember `prefers-reduced-motion` on one large, obvious animation (a hero background effect) and forget it on the many smaller transitions scattered through the rest of the site. Apply the override broadly.

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

### Don't animate properties that force layout recalculation

Prefer animating `transform` and `opacity`, which the browser can composite without recalculating layout, over animating `width`, `height`, `top`, or `left`, which force layout recalculation on every frame and can cause visibly janky motion, especially on lower-powered devices.

```css
/* Prefer this */
.card { transition: transform var(--duration-base) var(--ease-standard); }
.card:hover { transform: translateY(-4px); }

/* Over this, which triggers layout on every frame */
.card { transition: top var(--duration-base) var(--ease-standard); }
```

## Never do this

- Never pick a transition duration or easing curve for a new component without checking it against the site's existing motion scale.
- Never apply `prefers-reduced-motion` handling to only the most visible animation and skip the smaller ones.
- Never animate `width`, `height`, `top`, `left`, or `margin` when `transform` and `opacity` can achieve the same visual effect.
- Never use the same duration for a small hover effect and a full modal entrance; scale duration to what's actually moving.

## Verification checklist

- [ ] A defined, small set of durations and easing curves exists and every transition/animation on the site draws from it
- [ ] Duration feels proportional to the size/distance of what's animating, checked by comparing a few different components side by side
- [ ] Entrances generally ease out, exits generally ease in
- [ ] `prefers-reduced-motion` is handled globally, not only on the single most obvious animation
- [ ] Animations primarily transform `transform` and `opacity` rather than layout-triggering properties
