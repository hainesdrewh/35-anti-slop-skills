---
name: contrast-and-image-integrity-checks
description: 'Use this skill before calling any page with text over an image or a dark section "done," and whenever adding, sourcing, or generating any photo used to represent a specific property, product, person, or place. Also use it when a user reports text is "hard to read," "invisible," or "blends into the background," or that an image "doesn''t match" what it''s supposed to show. This skill exists because both failures (unreadable text, mismatched images) are consistently missed by prose-only design guidance; it replaces "make sure it looks right" with an actual script or a concrete checklist that gets run, the same way pre-launch-technical-audit replaces "check for overflow" with a real console script.'
---

# Contrast and Image Integrity Checks

## Why this matters

Two specific, well-documented failure modes keep shipping past design review because nobody actually checks for them mechanically: text that renders with almost no contrast against its background (especially text placed over a photo, where the photo's content varies by region and a color that looks fine over the sky looks invisible over a dark roofline), and an image that doesn't actually depict what the surrounding copy claims (a "Victorian" listing shown with a glass-and-steel modern interior, a "hand-crafted" product shown with an obviously generic stock photo). Both are invisible to an agent that only reasons about them in the abstract, and both are easy to catch with an actual check.

## Do this

### Check contrast programmatically, not by eye

For any text sitting on a photographic background or a custom (non-default) color combination, compute the actual contrast ratio rather than eyeballing it. In the browser, this can be checked directly:

```js
function relativeLuminance(rgb) {
  const [r, g, b] = rgb.map(c => {
    c /= 255;
    return c <= 0.03928 ? c / 12.92 : Math.pow((c + 0.055) / 1.055, 2.4);
  });
  return 0.2126 * r + 0.7152 * g + 0.0722 * b;
}
function contrastRatio(rgb1, rgb2) {
  const l1 = relativeLuminance(rgb1) + 0.05;
  const l2 = relativeLuminance(rgb2) + 0.05;
  return l1 > l2 ? l1 / l2 : l2 / l1;
}
// Parse two getComputedStyle(...).color values into [r,g,b] and compare;
// WCAG AA requires at least 4.5:1 for normal text, 3:1 for large text.
```

For text placed directly over a photo (not a solid color), the underlying photo's tone varies, so a fixed text color is not enough on its own:

- Add a scrim: a gradient or solid semi-transparent overlay between the photo and the text (see the gallery-caption pattern already used elsewhere in this repo), so contrast holds regardless of what's in that part of the photo.
- Or constrain the text to a fixed-color panel (a solid card, not directly on the image) if a scrim would compromise the photo itself.
- Never place text of an unverified color directly on a photo and assume it will be legible; verify it, or add a scrim that makes verification unnecessary.

### Check every text-on-dark-section pairing specifically

The most common version of this bug is text authored for a light theme (a dark, near-black color chosen to read on white) reused inside a dark-themed section or card without changing it, producing dark-on-dark. Whenever a component or section uses a dark or photo background, explicitly confirm the text color was chosen for that background, not inherited from a global default meant for light backgrounds.

### Verify every image actually shows what the copy claims

Before using any image (sourced stock, AI-generated, or client-provided) to represent something specific, look at it and confirm it actually matches the specific claim being made next to it:

- An architectural style named in the copy (Victorian, Craftsman, mid-century modern) must match what's actually visible in the photo, not just be "a nice house."
- A product description (material, color, a specific feature) must match what the product photo actually shows.
- A "before" and "after" pair must actually be the same location/subject, not two unrelated photos that happen to fit a narrative.
- A photo captioned with a specific neighborhood, city, or region should not obviously contradict it (visible signage, architecture, or landscape wildly inconsistent with the claimed location).

This check takes seconds per image and catches a failure mode that otherwise ships silently: nothing about a mismatched-but-nice-looking photo throws an error, and it goes unnoticed until a real visitor with domain knowledge (a real estate agent, a buyer who knows the neighborhood) catches it, at which point it reads as either incompetence or dishonesty.

### Re-run both checks after any late content or theme change

A dark-mode toggle, a last-minute color rebrand, or swapping a placeholder image for a real one can silently reintroduce either failure. Re-check contrast and image-content match specifically after any such change, not only at initial build time.

## Never do this

- Never place text over a photo without either verifying contrast against the actual range of tones in that photo or adding a scrim that guarantees it.
- Never reuse a text color chosen for a light background inside a dark-themed card or section without re-checking it.
- Never use a stock or generated image to represent a specific style, product, or place without looking at it and confirming it actually matches that specific claim.
- Never assume an image is fine because it looks generically appealing; "looks nice" and "matches the claim" are different checks.

## Verification checklist

- [ ] Every text element placed over a photo has been checked for contrast against the actual photo, not assumed
- [ ] Every text element in a dark-themed section or card uses a color chosen for that background, not a leftover light-theme default
- [ ] Contrast ratios meet at least WCAG AA (4.5:1 normal text, 3:1 large text) for every non-decorative text/background pairing
- [ ] Every image used to represent a specific style, product, or place has been visually confirmed to actually match that claim
- [ ] Both checks were re-run after any late theme, color, or image swap, not only at initial build
