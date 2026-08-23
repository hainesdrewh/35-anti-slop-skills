---
name: advanced-motion-and-3d
description: 'Use this skill whenever considering scroll-driven animation, parallax, 3D transforms, or WebGL/three.js effects for a site, and whenever a user asks to "add 3D," "make it feel more dynamic," "add parallax," or references a site with elaborate scroll effects as inspiration. This is a companion to motion-system, which covers basic transition/easing discipline; this skill covers the harder judgment call of whether advanced motion is actually justified for this project, and how to implement it without wrecking performance or accessibility if it is.'
---

# Advanced Motion and 3D

## Why this matters

Elaborate motion is one of the fastest ways to make a site feel expensive and considered when it fits, and one of the fastest ways to make it feel slow, gimmicky, and inaccessible when it doesn't. The failure mode isn't usually the specific technique; it's applying an impressive-looking effect to a project that doesn't call for it (a local plumber's site does not need a WebGL hero), or applying it without the performance and accessibility discipline that makes it survivable on real devices and for real users.

## Do this

### Judge whether it's justified before building it

Advanced motion earns its place when the product/brand is genuinely about visual craft or technical sophistication (a design/creative portfolio, a 3D product configurator, a game or entertainment property, a technical product demonstrating a genuinely spatial or visual concept), see [`portfolio-and-creative-showcase`](../portfolio-and-creative-showcase/SKILL.md) and [`visual-style-directions`](../visual-style-directions/SKILL.md)'s bold-maximalist or dark-technical directions for where it tends to fit. It's rarely justified for a local service business, a professional services firm, or anything where the visitor's task is to quickly extract information and act, per [`industry-visual-execution`](../industry-visual-execution/SKILL.md). When in doubt, the safer choice is restraint; a plain, fast, well-crafted site consistently outperforms an elaborate one for most business categories.

### Scroll-driven reveals and parallax

Use the native CSS Scroll-Driven Animations API (`animation-timeline: view()` or `scroll()`) where browser support allows, which runs off the main thread and doesn't require a scroll-listener library; fall back to `IntersectionObserver`-triggered class toggles for broader support, avoiding scroll-position-based JavaScript recalculation on every scroll event, which is a common source of jank.

```css
@keyframes reveal {
  from { opacity: 0; transform: translateY(24px); }
  to { opacity: 1; transform: translateY(0); }
}
.reveal-on-scroll {
  animation: reveal linear both;
  animation-timeline: view();
  animation-range: entry 0% cover 30%;
}
```

Keep parallax subtle (a background layer moving at a meaningfully different rate than foreground content, not an extreme effect) and never apply it to body text, which becomes uncomfortable to read while it's moving.

### 3D transforms and tilt effects

CSS `perspective` and `transform-style: preserve-3d` can produce a genuinely effective tilt-on-hover card or a subtle 3D product view without WebGL, at a fraction of the performance cost. Reserve actual WebGL/three.js for cases that need real 3D geometry, camera control, or physically-based rendering that CSS transforms can't achieve, not for effects CSS could handle more cheaply.

### If using WebGL/three.js, budget for it explicitly

- Load the 3D library and scene asynchronously, after the critical page content, so it never blocks initial render or Core Web Vitals.
- Provide a static image or simplified fallback for devices that can't handle WebGL well (older mobile GPUs) or that have JavaScript disabled.
- Keep the 3D scene's complexity (polygon count, texture size, number of lights) deliberately bounded and tested on a mid-tier mobile device, not just the development machine.
- Pause or stop the render loop when the canvas isn't visible (off-screen, tab not focused) to avoid burning battery and CPU for no visible benefit.

### Always provide a reduced-motion path

Every scroll-driven, parallax, or 3D effect needs a `prefers-reduced-motion` fallback that shows the content in its final state immediately, not just a shorter version of the same motion; see [`motion-system`](../motion-system/SKILL.md) for the broader reduced-motion requirement this extends specifically to advanced effects, which are more likely to cause genuine discomfort (vestibular issues) than a simple hover transition.

```css
@media (prefers-reduced-motion: reduce) {
  .reveal-on-scroll { animation: none; opacity: 1; transform: none; }
}
```

## Never do this

- Never add WebGL or elaborate scroll effects to a project in a category that calls for fast, plain, information-forward execution, purely because the effect looks impressive.
- Never apply parallax motion to body text or anything the visitor needs to read comfortably.
- Never ship a 3D scene with no performance budget or testing on a real mid-tier mobile device.
- Never leave a WebGL render loop running when its canvas isn't visible.
- Never ship any scroll-driven or 3D effect without a `prefers-reduced-motion` fallback that shows final content immediately.

## Verification checklist

- [ ] The decision to use advanced motion/3D was made deliberately based on whether this project's category actually calls for it
- [ ] Scroll-driven effects use the native Scroll-Driven Animations API or IntersectionObserver, not per-frame scroll-position recalculation
- [ ] Parallax is subtle and never applied to readable body text
- [ ] Any WebGL scene loads asynchronously, has a static fallback, is complexity-budgeted, and pauses when off-screen
- [ ] Every advanced motion effect has a tested `prefers-reduced-motion` fallback showing final content immediately
