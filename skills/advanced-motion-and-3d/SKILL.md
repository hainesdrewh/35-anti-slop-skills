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

### Cinematic showcase motion (mouse-parallax depth and scroll-driven pans)

This is the specific pattern to reach for when a hero needs to feel like a camera genuinely moving through a space, a property walkthrough, a product in an environment, a portfolio piece, rather than a static photo with a fade or a uniform zoom-drift applied to it. Uniform zoom-drift (the whole image slowly scaling up) is the default an agent reaches for and reads as generic exactly because every layer moves together; real depth comes from different elements moving at different rates relative to each other.

**Mouse-parallax depth**, multiple image layers (foreground, midground, background, cut from the same scene or photographed/rendered separately) shift by different amounts as the cursor moves, simulating look-around depth:

```html
<div class="parallax-scene" data-parallax>
  <img src="hero-bg.jpg" class="parallax-layer" data-depth="0.15" alt="">
  <img src="hero-mid.jpg" class="parallax-layer" data-depth="0.35" alt="">
  <img src="hero-fg.jpg" class="parallax-layer" data-depth="0.6" alt="Living room interior, [specific real description]">
</div>
```

```css
.parallax-scene { position: relative; overflow: hidden; }
.parallax-layer {
  position: absolute; inset: -5%; width: 110%; height: 110%; object-fit: cover;
  transition: transform 0.2s var(--ease-standard);
  will-change: transform;
}
```

```js
const scene = document.querySelector('[data-parallax]');
const layers = scene.querySelectorAll('.parallax-layer');
scene.addEventListener('pointermove', (e) => {
  const rect = scene.getBoundingClientRect();
  const x = (e.clientX - rect.left) / rect.width - 0.5;   // -0.5 to 0.5
  const y = (e.clientY - rect.top) / rect.height - 0.5;
  layers.forEach(layer => {
    const depth = Number(layer.dataset.depth);
    layer.style.transform = `translate(${-x * depth * 40}px, ${-y * depth * 40}px)`;
  });
});
scene.addEventListener('pointerleave', () => {
  layers.forEach(layer => { layer.style.transform = 'translate(0, 0)'; });
});
```

Layers with a higher `data-depth` (closer to the viewer) move more; the background barely moves. This alone, with no scroll involvement, reads as a real 3D space rather than a photo.

**Scroll-driven camera pan**, a wide panoramic image (or a sequence of a few images) pans horizontally or zooms as the visitor scrolls past the hero, simulating a camera moving through a room rather than the whole frame just fading in:

```css
.pan-hero { height: 100vh; overflow: hidden; position: sticky; top: 0; }
.pan-hero img {
  width: 140%; max-width: none; height: 100%; object-fit: cover;
  animation: pan-across linear both;
  animation-timeline: scroll();
  animation-range: 0 100vh;
}
@keyframes pan-across {
  from { transform: translateX(0); }
  to { transform: translateX(-28%); }
}
```

Source a genuinely wide/panoramic image (or a real photo with room to pan within, not a standard-aspect photo stretched) so the pan reveals actual new content rather than just cropping the same frame. For a multi-room feel, sequence 2-3 pans back to back down the page rather than one long pan, each revealing a different real space.

Both techniques degrade gracefully: without JS, the mouse-parallax scene just shows the layered image statically; without `animation-timeline` support, the scroll-pan falls back to a static frame. Both need the `prefers-reduced-motion` treatment below, since parallax and scroll-linked camera movement are exactly the kind of motion most likely to cause genuine discomfort for vestibular-sensitive visitors.

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
  .pan-hero img { animation: none; transform: none; width: 100%; }
  .parallax-layer { transition: none !important; transform: none !important; }
}
```

For the mouse-parallax scene specifically, also check `window.matchMedia('(prefers-reduced-motion: reduce)').matches` in the JS before attaching the `pointermove` listener at all, not just via CSS, since the listener itself does no harm but skipping it entirely is cleaner than fighting it with `!important`.

## Never do this

- Never add WebGL or elaborate scroll effects to a project in a category that calls for fast, plain, information-forward execution, purely because the effect looks impressive.
- Never apply parallax motion to body text or anything the visitor needs to read comfortably.
- Never ship a 3D scene with no performance budget or testing on a real mid-tier mobile device.
- Never leave a WebGL render loop running when its canvas isn't visible.
- Never ship any scroll-driven or 3D effect without a `prefers-reduced-motion` fallback that shows final content immediately.
- Never default to a single uniform zoom-drift on a hero image as the only "cinematic" option; that's the generic version of this exact category of motion. If a showcase needs to feel like real depth or camera movement, use layered mouse-parallax or a scroll-driven pan across a genuinely wide image instead.
- Never pan or zoom a standard-aspect photo stretched wider than its real content; source or crop an image that actually has room to reveal something new as it pans.

## Verification checklist

- [ ] The decision to use advanced motion/3D was made deliberately based on whether this project's category actually calls for it
- [ ] If the goal is a cinematic/depth showcase, layered mouse-parallax or a scroll-driven pan was used instead of a single uniform zoom-drift
- [ ] Scroll-driven effects use the native Scroll-Driven Animations API or IntersectionObserver, not per-frame scroll-position recalculation
- [ ] Parallax is subtle and never applied to readable body text
- [ ] Any WebGL scene loads asynchronously, has a static fallback, is complexity-budgeted, and pauses when off-screen
- [ ] Every advanced motion effect has a tested `prefers-reduced-motion` fallback showing final content immediately, and mouse-parallax also skips attaching its JS listener when reduced motion is requested
