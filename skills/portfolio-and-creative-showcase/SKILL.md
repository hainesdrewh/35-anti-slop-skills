---
name: portfolio-and-creative-showcase
description: 'Use this skill whenever building a portfolio site for an individual (designer, photographer, developer, artist, writer) or a creative studio. Also use it when a user asks to "build my portfolio," "show off my work," or "make a personal site." A portfolio''s entire job is demonstrating taste and capability directly through its own execution, so generic execution here is especially self-defeating: a designer''s portfolio built from a generic template actively undermines the claim the site exists to make.'
---

# Portfolio and Creative Showcase

## Why this matters

A portfolio site is unusual among the categories in this repo: the site itself is part of the work sample. A photographer's portfolio with clumsy image handling, or a designer's portfolio with generic AI-slop layout choices, doesn't just fail to sell the work, it directly contradicts the claim the whole site exists to make. The bar here is higher than "doesn't look like a template" because the visitor is specifically evaluating taste and craft, not just deciding whether to buy a service.

## Do this

### Let the work be the largest thing on the page

Design decisions should recede in favor of the actual work: generous space around images, minimal competing visual elements, restrained typography that doesn't compete with the visuals for attention. The strongest portfolios often look the simplest, because every design decision serves showing the work rather than showing off the designer's range.

### Choose a genuinely fitting visual language for the discipline

A photographer's site should handle images as the primary medium (full-bleed, careful cropping, real attention to load performance for high-resolution work per [`image-performance-optimization`](../image-performance-optimization/SKILL.md)). A developer's portfolio can afford more technical, structured presentation (real code snippets, live demos, GitHub activity) since that audience reads differently than a visual-arts audience. A writer's portfolio should prioritize readable typography (see [`typography-craft`](../typography-craft/SKILL.md)) over visual flourish. Don't apply one generic "portfolio template" across disciplines that actually need different things shown differently.

### Structure each project as a real case study, not just a gallery image

Where the work allows it, a project entry benefits from context: the problem, the specific role played, and the outcome, not just an image with a title (see [`case-studies-portfolio`](../case-studies-portfolio/SKILL.md) for the deeper case-study structure). A gallery of unlabeled, uncontextualized images asks the visitor to do all the interpretive work themselves.

### Make the "hire me" or "work with me" path unambiguous

Even a portfolio focused on showcasing work needs a clear, low-friction way to make contact (see [`contact-page-standards`](../contact-page-standards/SKILL.md)); a beautifully designed portfolio that makes a visitor hunt for how to reach the person behind it wastes the interest it just earned.

### Use motion and interaction with genuine restraint

A portfolio is one of the few categories where more elaborate interaction (a custom cursor, a scroll-driven transition, subtle 3D on a project thumbnail) can be genuinely appropriate, since it's itself a demonstration of craft, see [`advanced-motion-and-3d`](../advanced-motion-and-3d/SKILL.md) for how to do this without hurting performance or accessibility. But it must serve the work, not distract from it; an interaction that makes a visitor wait or fight the interface to see the actual work has failed regardless of how impressive it looks in isolation.

## Never do this

- Never apply a generic template that could belong to any discipline; a photographer's site and a developer's site should not be structured identically.
- Never let a decorative interaction slow down or obstruct access to the actual work being showcased.
- Never present a project gallery with zero context, forcing the visitor to guess what they're looking at.
- Never bury the contact path so deep that genuine interest has no easy way to convert into an inquiry.

## Verification checklist

- [ ] The visual language fits the specific discipline (photography, design, development, writing), not a generic cross-discipline template
- [ ] Each showcased project has enough real context to be understood, not just an unlabeled image
- [ ] Any elaborate motion/interaction serves the work rather than gating or distracting from it, and respects `prefers-reduced-motion`
- [ ] Image-heavy work is optimized per `image-performance-optimization` so quality doesn't come at the cost of load time
- [ ] A clear, low-friction way to make contact is present and easy to find
