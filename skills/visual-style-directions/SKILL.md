---
name: visual-style-directions
description: 'Use this skill at the same point as anti-ai-slop-design, right after project-scoping-and-prd, whenever starting the visual design of any site, to deliberately choose a style direction instead of defaulting to whichever look was used most recently. Also use it when a user says a design "looks like every other site you''ve built," asks for something that "looks different," or asks for a specific mood (clean, bold, luxury, minimal, playful). This skill exists because even genuinely tasteful, anti-slop output can become its own kind of sameness if the same style choices get reached for on every project regardless of what the business actually needs.'
---

# Visual Style Directions

## Why this matters

[`anti-ai-slop-design`](../anti-ai-slop-design/SKILL.md) rules out the obvious generic look (the purple gradient, the emoji-icon feature grid), but ruling something out doesn't automatically produce variety in what replaces it. Left unguided, an agent that has internalized "avoid gradients, use a real spacing scale, use Fraunces-and-Public-Sans-style serif/sans pairings" can end up reaching for the same specific tasteful look on every project, which is a subtler version of the same underlying problem: every site still looking similar to every other site this agent builds. This skill exists to make the style decision an explicit, deliberate choice from a set of genuinely distinct directions, driven by the PRD's actual audience and positioning, not by inertia.

## Do this

### Choose a direction based on the PRD, not by default

Before writing any CSS, look at the ICP and positioning from [`project-scoping-and-prd`](../project-scoping-and-prd/SKILL.md) and pick the direction (from [references/style-directions.md](references/style-directions.md) or a genuinely different one this project calls for) that actually fits: a luxury real estate brokerage and a scrappy local plumber should not land on the same style even though both are legitimate, non-slop choices in isolation.

### Commit fully once a direction is chosen

A style direction is a coherent system, palette, type pairing, spacing personality (tight and structured vs. generous and airy), and motion character (restrained vs. expressive), not just a color choice. Half-committing (a minimal palette with a maximalist type treatment) tends to read as inconsistent rather than eclectic. Pick a direction and let it govern every subsequent design decision on the project.

### Track which direction was used, don't repeat it reflexively

If this agent has built multiple sites, actively check what direction was used last and treat repeating it as a decision that needs a reason ("this business genuinely calls for the same clean-minimal direction as the last project"), not an unexamined default. Variety across an agent's output is itself part of not reading as generic; a portfolio of five sites that all look like variations on one template is a slop tell at the portfolio level even if no individual site violates `anti-ai-slop-design` on its own.

### Adapt, don't copy a direction verbatim

The named directions in the reference file are starting points with real specifics (so they're actually usable, not vague mood words), but the specific palette, type choices, and details should still be adapted to the actual business, its existing brand assets if any, and its real competitors, not applied as an unmodified template.

### Vary structure, not just palette and font

This is the mistake that undermines this skill most often, and it's subtle enough to happen even while genuinely trying to follow it: swapping the color variables and the font pairing while reusing the exact same layout skeleton from the last project (the same header pattern, the same hero composition, the same card anatomy, the same section rhythm, the same floating chrome) produces two sites that are still recognizably the same template wearing different colors. A visitor, and especially another site built by the same agent sitting side by side, reads that as sameness regardless of how different the palette is. Palette and type are the least of what makes two sites feel distinct; structure is most of it.

Before starting a new build, deliberately choose, and vary from the last project, at least the following:

- **Header/nav pattern**: a simple inline text nav with a filled CTA button, a minimal logo-only header with nav revealed on scroll or in a slide-out, a centered logo with nav split left/right around it, or a bold full-width bar with no floating/sticky behavior at all.
- **Hero composition**: full-bleed photo with text overlay, a split-screen layout (text on a solid color panel beside an image panel), a centered text-only hero with no image, an asymmetric layout with an off-center image bleeding off one edge, or a hero built from a grid of smaller images rather than one large one.
- **Card/grid anatomy**: bordered cards with rounded corners and shadow-on-hover (the default that's easy to reach for), borderless images with caption text below and no card container at all, an editorial alternating-row layout instead of a grid, overlapping/layered image treatment, or a dense list/table view instead of a card grid.
- **Section rhythm**: alternating background bands (light/alt/light), one continuous background with dividers or whitespace doing the separation instead, or a fully asymmetric page with no repeating rhythm at all.
- **Floating chrome**: a floating CTA button and scroll-to-top are genuinely useful for some categories (see [`frontend-polish-microinteractions`](../frontend-polish-microinteractions/SKILL.md)) and actively wrong for others; a restrained editorial-luxury direction, for instance, is undermined by the same floating brass button pattern reused from a warm-craft local-service site. Decide per project whether floating chrome fits the direction at all.
- **Motion signature**: the specific easing/duration values from [`motion-system`](../motion-system/SKILL.md) should differ in character between projects too, a slow deliberate fade for an editorial-luxury site reads differently than a snappy, energetic transition for a bold-maximalist one, not just the same drift-zoom hero animation with a different photo underneath.

If a new project's header, hero, and card structure would be interchangeable with the previous project's if you swapped the photos and color variables, that's the signal this step was skipped, not evidence the direction was distinct enough.

### Vary the recurring mid-page sections too, not only the hero and header

It's possible to genuinely restructure the header, hero, and footer, the highest-visibility, most-scrutinized parts of a page, and still ship something that reads as the same template, because the sections in between (a stats/trust band, a feature callout with an image and text side by side, a testimonial grid, a closing CTA band) got carried over unchanged with only the color variables swapped. Those sections are just as much a structural fingerprint as the hero: a `grid-3` of identically-styled cards for testimonials, a `grid-2` image-left-text-right feature callout, and a dark full-width CTA band are a recognizable combination on their own even with a perfectly redesigned hero above them. Treat every repeating section on the page as a place to apply this skill, not only the parts a visitor sees first.

Concretely, before shipping, look at the full page top to bottom against the previous project's and ask section by section, not just "is the hero different" but "is the stats band different, is the feature callout different, is the testimonial layout different, is the CTA band different." A single un-varied section is a smaller miss than an un-varied hero, but four or five of them in a row is the difference a visitor actually notices when they say two sites "look the same."

## Never do this

- Never default to the same style direction across multiple unrelated projects without a specific reason this project calls for it too.
- Never mix incompatible signals from different directions (a restrained luxury palette with bouncy, playful motion, for example) without a deliberate reason.
- Never treat a style direction as only a color palette; type, spacing personality, and motion character all need to cohere with it.
- Never apply a named direction's specifics verbatim without adapting them to the actual business and any existing brand assets.
- Never reuse the previous project's header pattern, hero composition, card anatomy, and section rhythm unchanged while only swapping the color palette and font pairing; that produces two sites that are structurally identical, which reads as sameness regardless of how different the colors are.

## Verification checklist

- [ ] The chosen direction was selected based on the PRD's actual audience and positioning, not defaulted to
- [ ] Palette, typography, spacing personality, and motion character all cohere with the chosen direction
- [ ] If this agent has built other sites, the direction wasn't repeated reflexively from the most recent project
- [ ] The direction's specifics were adapted to this business's actual brand and market, not copied verbatim
- [ ] Header/nav pattern, hero composition, card/grid anatomy, and section rhythm were each deliberately chosen and differ structurally from the immediately previous project, not just recolored
- [ ] Every recurring mid-page section (stats/trust band, feature callout, testimonial layout, CTA band) was checked individually against the previous project, not only the hero and header
- [ ] Floating chrome (call button, scroll-to-top) was a deliberate choice for this direction, not a carried-over default
- [ ] If you swapped this project's photos and color variables into the previous project's markup, would anyone notice? If the honest answer is no, the structural variation step was skipped

See [references/style-directions.md](references/style-directions.md) for five fully-specified starting directions (clean minimal, editorial luxury, bold maximalist, dark technical, warm craft).
