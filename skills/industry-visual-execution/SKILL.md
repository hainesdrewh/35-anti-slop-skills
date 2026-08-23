---
name: industry-visual-execution
description: 'Use this skill whenever building a website for a specific business vertical (real estate, restaurant, landscaping, professional services, home services, medical/dental, fitness) where a generic template would visibly fail to match how that industry actually presents itself. Also use it whenever a user names an industry and asks for a site that "looks professional," "looks premium," or references a specific competitor/inspiration site''s look. This is a companion to anti-ai-slop-design: that skill teaches what to avoid in general, this one teaches what excellent actually looks like for a specific kind of business, since the right answer is genuinely different per vertical, not one template with the colors swapped.'
---

# Industry Visual Execution

## Why this matters

A real estate listing page, a landscaping company site, and a restaurant site should not be visually interchangeable, because they're selling fundamentally different things in fundamentally different ways: a listing page sells a specific physical space through photography and hard facts, a landscaping site sells trust and visible transformation, a restaurant sells atmosphere and craveability. Applying one generic layout template across all of them, even a well-executed one, is a subtler version of the same genericness [`anti-ai-slop-design`](../anti-ai-slop-design/SKILL.md) targets at the component level. This skill exists to make the industry-specific visual decision deliberately instead of defaulting to whatever layout was used last.

Always run [`project-scoping-and-prd`](../project-scoping-and-prd/SKILL.md) first; the ICP and value proposition it produces should inform which of the patterns below actually fits, rather than picking a vertical's default pattern purely because the business happens to be in that industry.

## Do this

### Real estate / property listings

The photography and the facts are the product; the UI should get out of the way of both. Full-bleed, high-resolution imagery with a real gallery/carousel (not four small thumbnails), key facts (price, beds, baths, square footage) presented as scannable data immediately near the hero image rather than buried in a paragraph, a map showing actual location and proximity to relevant points of interest, and a clear, low-friction path to schedule a showing or contact an agent. Property listing pages in particular benefit from a sticky summary bar (price and primary CTA) that stays visible while scrolling through a long photo set.

### Landscaping / home exterior services

Visible transformation is the product. Before/after presentation (see [`case-studies-portfolio`](../case-studies-portfolio/SKILL.md)) does more work than descriptive copy. A full-bleed, high-quality hero image or slow-moving background video of real completed work (with a `prefers-reduced-motion` fallback to a static image, and never autoplaying with sound) reads as far more credible than an illustration or stock photo. Seasonal relevance matters more here than in most verticals: a hero image of a lush summer lawn shown in the middle of winter reads as either stale or dishonest about current conditions.

### Restaurants / food service

Atmosphere and craveability drive the decision. Real, well-lit photography of actual dishes (never stock food photography, which reads as generic almost instantly to anyone who's looked at a restaurant site before) is the single highest-leverage visual asset. Hours, location, and a reservation/ordering path need to be reachable within one tap from the homepage, not buried under an "About" click-through. A menu should be real, readable HTML content (for SEO and accessibility) rather than only a PDF or an image, which is invisible to search engines and unreadable to screen readers.

### Professional services (law, accounting, consulting)

Trust and credibility carry more weight than visual flourish. Credentials, specific case outcomes or client results (see [`case-studies-portfolio`](../case-studies-portfolio/SKILL.md) and [`review-testimonials-social-proof`](../review-testimonials-social-proof/SKILL.md)), and a clear, calm visual register (more whitespace, more restrained color, fewer competing CTAs) read as more credible for this category than a high-energy consumer-brand treatment would. A cluttered, hard-sell layout actively undermines trust in a category where the visitor is often making a high-stakes decision.

### Home services (HVAC, plumbing, electrical, contracting)

Speed to contact and visible trust signals (licensing, insurance, years in business, real reviews) matter more than visual polish alone, since a meaningful share of visitors are in an active-problem state (something broke) and want the fastest path to a phone call. Tap-to-call and clear service-area/availability information belong above the fold (see [`mobile-navigation-ux`](../mobile-navigation-ux/SKILL.md) and [`local-service-seo`](../local-service-seo/SKILL.md)), not several scrolls down.

### Medical, dental, and fitness

A calmer, reassuring visual register similar to professional services, but with a stronger emphasis on approachability: real photos of the actual practice/facility and staff (never generic stock photos of unrelated medical professionals), clear information on insurance/accepted payment and how to book, and accessibility given extra weight since this audience skews toward visitors who specifically benefit from strong contrast and clear navigation (see [`accessibility-basics`](../accessibility-basics/SKILL.md)).

## Never do this

- Never apply the same generic template across visibly different business types just because the underlying tech stack is the same.
- Never use stock photography where real photography of the actual business is the entire point (food, completed project work, the actual space or team).
- Never show a hero image that's seasonally or visibly out of sync with current reality for a business where visual freshness matters (landscaping, restaurants with seasonal menus).
- Never bury the single most time-sensitive action (call now, book a table, schedule a showing) below content that could wait.

## Verification checklist

- [ ] The layout pattern was chosen deliberately for this business's category, not defaulted from a generic template
- [ ] The visual asset that actually sells this business (property photos, food photography, before/after transformation, credentials) is the dominant visual element, not an afterthought
- [ ] Any background video/imagery has a static, reduced-motion-safe fallback and never autoplays with sound
- [ ] The single most time-sensitive action for this business type is reachable without scrolling past unrelated content
- [ ] Photography is real and specific to this business, not generic stock imagery standing in for the real thing

See [references/industry-patterns.md](references/industry-patterns.md) for more detailed layout breakdowns and concrete section-by-section structure per vertical.
