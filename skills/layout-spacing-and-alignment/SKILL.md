---
name: layout-spacing-and-alignment
description: 'Use this skill whenever writing CSS/layout code for any component, header, card, or page section, and whenever a user reports that something "looks a little off," "feels cramped," "isn''t lined up right," or asks to "fix the spacing." Apply it by default on every layout decision, not only when spacing is explicitly mentioned, since inconsistent spacing is one of the fastest ways a site reads as unpolished even when every individual element looks fine in isolation. This is a companion to anti-ai-slop-design: that skill covers macro layout and visual judgment, this one covers the fine-grained spacing and alignment discipline that turns "looks fine" into "looks intentional."'
---

# Layout, Spacing, and Alignment

## Why this matters

A site can have great typography, a considered color palette, and genuinely good copy, and still feel subtly unpolished because of inconsistent gaps, misaligned icons, and padding values picked ad hoc per component. This is often the actual cause behind a vague "something feels off" reaction, and it's invisible until named directly: a logo mark sitting 2px too high next to its wordmark, a card with more padding on top than the sides, a row of icons that don't share a baseline. None of these break functionality. All of them add up to a site that reads as not quite finished.

## Do this

### Use one spacing scale, everywhere

Pick a base unit (commonly 4px or 8px) and derive every margin, padding, and gap value from it as multiples, rather than choosing pixel values per component as they come up.

```css
:root {
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-6: 24px;
  --space-8: 32px;
  --space-12: 48px;
  --space-16: 64px;
}
```

A component using `padding: 14px 19px` next to one using `padding: 16px 20px` is a tell that spacing wasn't systematized; both should resolve to values from the same scale.

### Establish vertical rhythm between sections

Section-to-section spacing on a page should follow a consistent pattern (e.g. every major section gets `--space-16` of padding, sub-sections within it get `--space-8`), not a different gap every time depending on how the content happened to lay out. Inconsistent rhythm is most noticeable when scrolling quickly through a page: sections should feel like they belong to the same document.

### Correct for optical alignment, not just mathematical alignment

Mathematically centering an icon next to a line of text based on bounding-box height often looks off-center, because icons and glyphs don't fill their bounding box symmetrically. Nudge by a pixel or two based on how it actually looks, not just what a centering calculation produces. The same applies to a logo mark next to a wordmark: match cap-height or optical weight, not just container height.

```css
/* A logo icon often needs a small manual offset to sit visually
   level with the wordmark beside it, even when both are the same
   container height. */
.logo svg { margin-top: -1px; }
```

### Keep related elements' gaps consistent with their relationship

Elements that are closely related (a label and its input, an icon and its label) should have less space between them than elements that are only loosely related (two separate form fields, two separate cards). If every gap in a layout is visually similar regardless of what's actually related to what, the grouping isn't legible at a glance, forcing a reader to work out relationships from content alone.

### Align to a real grid

Use CSS Grid or a consistent column system so that edges (left edges of text blocks, right edges of images) line up across a section instead of drifting by a few pixels from container to container. When two adjacent elements are supposed to align and don't, quite by how much, check for accidental extra padding, a border adding to width, or `box-sizing` inconsistency between them.

### Check padding is even for what it's meant to be

A button or badge with `padding: 8px 12px` should have consistent vertical centering of its text within that padding; if the text sits visibly closer to the top or bottom, check for an unaccounted line-height or an icon inside pushing things off-center.

## Never do this

- Never pick a one-off pixel value for a single component's spacing without checking it against the site's spacing scale first.
- Never leave a mathematically-centered icon or logo mark in place if it visually reads as off-center; trust the eye over the calculation.
- Never let padding around similar components (a set of buttons, a set of cards) vary without a specific reason.
- Never let related-vs-unrelated spacing collapse to the same gap value; the spacing itself should communicate grouping.

## Verification checklist

- [ ] Every margin/padding/gap value in the stylesheet traces back to a single defined spacing scale
- [ ] Section-to-section vertical spacing follows a consistent, repeatable pattern down the page
- [ ] Logos, icons, and adjacent text are checked visually for optical alignment, not just mathematical centering
- [ ] Closely related elements have visibly smaller gaps than loosely related ones
- [ ] Elements meant to align to a shared edge (text blocks, images, columns) actually do, checked at real viewport widths
- [ ] No component's padding was copy-pasted from another without confirming it still produces balanced, centered content
