---
name: data-grid-and-listing-pages
description: 'Use this skill whenever building a browsing, filtering, or listing page: real estate listings, e-commerce category/search results, job boards, directories, or any page whose job is to let a visitor scan many similar items and narrow them down. Also use it when a user asks to "add a listings page," "add search and filters," "build a browse page," or "add a product grid." This is a distinct layout problem from a marketing page or a single item''s detail page, dense, scannable, and filterable, and treating it like a marketing page (generous whitespace, one hero, no real density) is a common way these pages end up feeling broken rather than just plain.'
---

# Data Grid and Listing Pages

## Why this matters

A listing/browse page has a different job than a homepage: a visitor is scanning many items quickly to decide which ones deserve a closer look, not being sold on one idea. Applying marketing-page instincts here, generous whitespace, one big hero, sparse information per section, produces a page that either wastes the visitor's scrolling (too little per screen) or leaves cards with awkward, uneven internal spacing because the layout wasn't actually designed for repeating at scale. Real estate listing pages, e-commerce category pages, and job boards all share this same underlying structure even though the content differs.

## Do this

### Design the card as a repeating unit, not a one-off

Every card in the grid needs the same anatomy, in the same order, with the same spacing rules, so the eye can scan across dozens of them without re-parsing structure each time: image, then a fixed-position primary identifier (address, product name, job title), then key facts as a scannable row (price/beds/baths, price/rating, salary/location), never a fact appearing in one card's second line and another card's fourth line.

```
[image]
[category or status badge, if any]
[primary title, one line, truncated with ellipsis if needed]
[secondary line: location/subtitle]
[key facts row: price · fact · fact · fact]
```

Test the card design against the shortest and longest realistic content it will hold (a one-word city vs. a long neighborhood name, a 3-digit price vs. a 7-digit price) so spacing doesn't only work for the placeholder content it was designed against.

### Give the grid real, consistent rhythm

Use CSS Grid with a fixed or `auto-fill`/`minmax` column definition and one gap value from the site's spacing scale (see [`layout-spacing-and-alignment`](../layout-spacing-and-alignment/SKILL.md)), so row and column gaps are visually identical and cards align to a real grid, not an approximately-even flex-wrap.

```css
.listing-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: var(--space-8);
}
```

### Make filters immediately usable, not decorative

A filter/search control that doesn't visibly do anything (no result count update, no visible active-filter state, no way to clear it) reads as broken even if it technically works. At minimum: show the current result count, reflect active filters visibly (a chip, a highlighted control), and provide an obvious way to clear or change them without reloading the whole page if avoidable.

### Handle empty and loading states explicitly

A filter combination that returns zero results needs a real empty state (see [`tooltips-microcopy-ux`](../tooltips-microcopy-ux/SKILL.md)) explaining that plainly and suggesting a next step (broaden the filters, clear them), not a blank grid that looks like the page is broken. While results are loading, use skeleton cards matching the real card's shape (see [`component-detail-polish`](../component-detail-polish/SKILL.md)), not a blank gap or a generic spinner that gives no sense of what's coming.

### Keep information density intentional

A listing page benefits from more visible content per screen than a marketing page; don't apply marketing-page-scale whitespace (large section padding, oversized headings) to a grid meant for scanning. At the same time, don't cram cards edge-to-edge with no breathing room; the goal is a deliberate density decision, tighter than a hero section, looser than a spreadsheet, not a default inherited from whichever page type was built most recently.

### Verify contrast and image accuracy per card, not just once

Because a listing grid repeats the same card structure dozens of times, a contrast or image-mismatch bug (see [`contrast-and-image-integrity-checks`](../contrast-and-image-integrity-checks/SKILL.md)) in the card template affects every single item at once. Check the card template specifically against this, since it is the highest-leverage place in the whole page for exactly that class of bug.

## Never do this

- Never let the same fact appear in a different position from card to card; the repeating structure is the entire point.
- Never ship a filter control with no visible feedback that it did anything.
- Never leave a zero-result state indistinguishable from a broken or still-loading page.
- Never apply marketing-page whitespace and hero-scale typography to a page meant for scanning many items quickly.
- Never test the card design only against ideal placeholder content; check it against the shortest and longest realistic real content.

## Verification checklist

- [ ] Every card follows the identical anatomy and fact order, tested against both short and long realistic content
- [ ] The grid uses a real CSS Grid definition with one consistent gap value, not approximate flex spacing
- [ ] Filters show active state, a live result count, and an obvious way to clear them
- [ ] A zero-result state exists and explains what happened and what to do next
- [ ] A loading state uses skeleton cards matching the real card shape, not a blank gap or generic spinner
- [ ] The card template specifically has been checked against `contrast-and-image-integrity-checks`, since any bug there repeats across every card in the grid
