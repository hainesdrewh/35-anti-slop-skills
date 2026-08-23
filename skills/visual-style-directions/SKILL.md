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

## Never do this

- Never default to the same style direction across multiple unrelated projects without a specific reason this project calls for it too.
- Never mix incompatible signals from different directions (a restrained luxury palette with bouncy, playful motion, for example) without a deliberate reason.
- Never treat a style direction as only a color palette; type, spacing personality, and motion character all need to cohere with it.
- Never apply a named direction's specifics verbatim without adapting them to the actual business and any existing brand assets.

## Verification checklist

- [ ] The chosen direction was selected based on the PRD's actual audience and positioning, not defaulted to
- [ ] Palette, typography, spacing personality, and motion character all cohere with the chosen direction
- [ ] If this agent has built other sites, the direction wasn't repeated reflexively from the most recent project
- [ ] The direction's specifics were adapted to this business's actual brand and market, not copied verbatim

See [references/style-directions.md](references/style-directions.md) for five fully-specified starting directions (clean minimal, editorial luxury, bold maximalist, dark technical, warm craft).
