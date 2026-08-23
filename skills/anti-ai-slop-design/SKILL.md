---
name: anti-ai-slop-design
description: 'Use this skill whenever building, designing, redesigning, or reviewing any website, landing page, web app UI, or mobile app UI, even if the user just says "build me a site," "make a landing page," "redesign this," or gives no design direction at all. Also use it whenever a user says a design "looks AI-generated," "looks generic," "looks like every other SaaS site," "needs more personality," or asks for a design/UI review. This skill overrides default generation habits, since without it default output reliably produces gradient-hero, purple-badge, 3-card-emoji-grid sites that read as AI slop on sight. Apply it before writing any layout, color, or copy, not as a cleanup pass after.'
---

# Anti-AI-Slop Design

## Why this matters

People can tell an AI-generated site in about two seconds, before they've read a word of copy. That perception costs trust and conversions regardless of how good the underlying business is: a site that looks like a template with placeholder-flavored copy reads as low-effort, which reads as untrustworthy. This skill exists because the *default* output of an LLM asked to "build a website" reliably converges on the same visual template, not because that template is good, but because it's the statistical average of every SaaS landing page in the training data. Good design is not the average; it's a specific decision made for a specific audience. This skill's job is to force those specific decisions instead of defaulting to the average.

Every other skill in this repo assumes this one is already in effect. A site can pass every SEO and security check in this repo and still look like slop if this skill wasn't applied first.

If [`project-scoping-and-prd`](../project-scoping-and-prd/SKILL.md) has been run for this project, use its ICP/value-proposition output as the input to every decision below. Design choices made without knowing who the site is for are exactly how generic output happens.

## The tells: name them so you stop reproducing them

These are not vague vibes. They are specific, recognizable patterns. If you catch yourself about to produce any of these, stop and pick something else.

**Layout & structure**
- Hero section: centered headline + subheadline + two buttons + a vague illustration or gradient blob, full viewport height, with zero information density
- The exact sequence: Hero → 3-column "Features" grid with icon-in-a-circle + bold title + one sentence → "How it works" 3-step row → testimonial carousel → pricing table with the middle tier highlighted → FAQ accordion → final CTA band → footer. This sequence, in this order, on a site that isn't actually a SaaS product, is the single strongest slop tell there is.
- Symmetrical, perfectly centered everything with no intentional asymmetry or visual hierarchy beyond font-size
- Excessive whitespace used as a substitute for actual content density, on a site (local business, portfolio, e-commerce) where real information should be visible without scrolling

**Color & surface**
- Purple-to-blue (or pink-to-orange) gradient anywhere, including backgrounds, buttons, or headline text-fill. This is the single most recognizable AI-slop signature there is. Default to a real brand palette instead: one dominant neutral, one accent color used sparingly and consistently, not a gradient standing in for a color decision.
- Gradient or rainbow text-fill on headlines
- Glassmorphism (frosted-glass translucent cards) or floating abstract blob shapes used as decoration with no relationship to the content
- Overuse of soft drop-shadows on every card/button to fake depth
- Every corner radius the same generous rounded value on every single element (cards, buttons, inputs, images) with no variation

**Components**
- Icon-in-a-colored-circle repeated for every feature, especially generic line icons that don't relate to the actual feature
- A "Trusted by" logo row of implausible/generic company names or logos that don't correspond to real clients
- A checkmark bullet list used as a substitute for actually explaining a benefit
- Badge/pill labels used decoratively ("New!", "Popular", "✨ AI-Powered") on things that don't need one
- Particle/animated-blob backgrounds, especially combined with the purple gradient above
- Stock photography of diverse people smiling at laptops or pointing at whiteboards

**Copy**
- "Empower your [noun]," "Unlock the power of," "Take your [X] to the next level," "Revolutionize the way you [verb]," "Seamlessly [verb]," "Elevate your [noun]": this register of inflated, content-free marketing language
- Feature descriptions that restate the feature name instead of explaining the outcome ("Powerful Analytics: Get powerful analytics for your business")
- Generic "We are passionate about [industry]" founder copy with no specific facts (see [`trust-and-about-content`](../trust-and-about-content/SKILL.md))
- Em dashes and "It's not just X, it's Y" constructions used repeatedly as a rhetorical crutch. Em dashes in particular are one of the most recognizable tells of AI-written copy right now, so avoid them in body copy, headlines, and everywhere else on the page. Use a period, comma, or parentheses instead.

**Motion**
- Fade-up-on-scroll applied uniformly to every single section with no variation or purpose
- Hover effects that only ever do "lift + shadow" on every clickable element

## Do this instead

**1. Ground every decision in the actual business, not a template.** Before laying anything out, know: who is this for, what do they need to believe to convert, and what does this specific business look like when it isn't wearing a SaaS costume? A landscaping company, a law firm, a bakery, and a dev-tools product should not produce visually interchangeable sites.

**2. Pick a real, constrained palette.** One neutral (not pure white/black, but a warm or cool off-tone), one primary brand color used deliberately, one accent used sparingly for CTAs only. No gradients standing in for a color choice. If the brand has an existing color (logo, signage, prior materials), use it instead of overriding it with a "modern" palette.

**3. Choose typography with an actual point of view.** A single default system font at uniform weight everywhere is a tell on its own. Pair a distinct display face for headlines (even a well-chosen system serif or a characterful sans) with a plain, readable body font, and use real type scale (headline sizes that vary meaningfully, not just bold vs. not-bold).

**4. Let layout vary by content, not by template.** Not every section needs to be a centered column. Use asymmetry, real grid variation, and information density appropriate to the business. A restaurant menu page and a checkout flow should not share a layout rhythm just because they came from the same generator.

**5. Write copy that could only be about this business.** Specific numbers, specific claims, specific language the actual business would use. If a sentence could be pasted into a competitor's site unchanged, rewrite it. Replace every inflated verb ("empower," "unlock," "revolutionize") with a plain one that states what actually happens.

**6. Use real content, or clearly-marked placeholders, but never fake-real content.** A testimonial carousel with invented quotes and stock headshots is worse than no testimonial section. If real reviews/logos/photos aren't available yet, build the structure but flag it explicitly (see [`pre-launch-technical-audit`](../pre-launch-technical-audit/SKILL.md) for the placeholder-sweep this feeds into) rather than filling it with fabricated "social proof."

**7. Use motion with restraint and purpose.** A single well-placed micro-interaction beats fade-up-on-scroll applied to everything. If every section animates identically, remove the animation from most of them.

**8. Vary component treatment.** Not every clickable thing needs the same rounded-corner, drop-shadow, icon-in-a-circle treatment. Let hierarchy come from real typographic and spatial decisions, not from decorating everything equally.

## Verification checklist

Before calling a design done, check it against this list honestly:

- [ ] Is there a gradient anywhere (background, button, or text-fill)? If yes, justify it specifically or remove it.
- [ ] Does the hero → features → testimonials → pricing → FAQ → CTA sequence appear, on a site that isn't actually a subscription SaaS product? If yes, restructure around the business's actual content.
- [ ] Could this copy be pasted onto a competitor's site with just the name changed? If yes, rewrite with specifics.
- [ ] Are all card/button corner radii, shadows, and icon treatments visually identical across the whole page? If yes, introduce real hierarchy.
- [ ] Are there any testimonials, client logos, or reviews that aren't real? If yes, remove them or replace with a clearly-marked placeholder state, don't fabricate.
- [ ] Would someone unfamiliar with AI tools still describe this as "generic" or "like every other site"? If uncertain, compare it against 2-3 real, well-regarded sites in the same industry (not other AI output) and check for actual differentiation.

See [references/before-after-examples.md](references/before-after-examples.md) for concrete rewrites of common slop patterns (hero sections, feature grids, testimonial sections) into specific alternatives.
