---
name: saas-marketing-pages
description: 'Use this skill whenever building a marketing site for a software product: a landing page, a pricing page, or a features page. Also use it when a user asks to "build a landing page for my app," "add a pricing page," or "make a SaaS website." SaaS marketing is the category most saturated with AI-slop templates already (the exact hero-features-pricing-FAQ sequence anti-ai-slop-design names as a tell), so this skill exists to make deliberate, specific decisions for an actual product instead of reproducing that template, and to get the pricing page specifically right, since it is where the most revenue-critical decisions on the whole site live.'
---

# SaaS Marketing Pages

## Why this matters

SaaS marketing pages are the category [`anti-ai-slop-design`](../anti-ai-slop-design/SKILL.md) is most directly reacting to, precisely because there are so many of them and they converge so hard on one template. Building a genuinely good one requires actively resisting that convergence, not just executing the standard sections competently. The pricing page in particular is where unclear or manipulative structure directly costs revenue, either through confused visitors who don't convert or through structures that convert dishonestly and generate refund requests and chargebacks later.

## Do this

### Landing page

- Lead with the specific problem this product solves and for whom, in concrete terms, not an abstract capability statement; a visitor should know within one sentence whether this product is even relevant to them.
- Show the actual product, a real screenshot or short product demo, not an abstract illustration standing in for what the software does. If the product is genuinely hard to show statically, a short, real (not staged) demo video or GIF does more work than any amount of descriptive copy.
- Address the specific alternative a visitor is likely comparing against (a competitor, a manual process, doing nothing) rather than writing as if this product exists in a vacuum.
- Use real, specific proof: actual customer logos (with permission), actual usage numbers, actual named case studies, not vague "loved by thousands" claims with no specifics.
- Vary section structure and order based on what this specific product actually needs to explain, rather than defaulting to hero-features-testimonials-pricing-FAQ-CTA in that exact order every time; see [`anti-ai-slop-design`](../anti-ai-slop-design/SKILL.md) for why that specific sequence is a slop tell.

### Pricing page

- State prices plainly; if pricing is genuinely usage-based or enterprise-only, say so explicitly rather than hiding a "Contact us" tier among priced tiers with no explanation of why it differs.
- Make tier differences genuinely scannable: a comparison table with consistent rows across tiers, not prose paragraphs that require re-reading each tier to compare a specific feature.
- If a tier is highlighted as recommended, that should reflect genuine best-value analysis for the target ICP, not just decorate the middle tier by default; see [`anti-ai-slop-design`](../anti-ai-slop-design/SKILL.md)'s pricing-section guidance for the specific pattern to avoid.
- State billing terms plainly: whether prices are monthly or annual, whether annual billing is required for the listed price, and what happens on cancellation, before the user has to reach checkout to find out.
- If there's a free tier or trial, state its real limits (usage caps, feature restrictions, trial length) rather than leaving them to be discovered after signup; this also directly connects to [`api-abuse-and-rate-limiting`](../api-abuse-and-rate-limiting/SKILL.md), since a free tier's stated limits need to be the limits actually enforced.

### Features page

Organize around outcomes the user cares about, not an alphabetical or engineering-org-chart list of every feature the product has. Group related features under the job they accomplish, and let the most differentiating features (the ones a competitor doesn't have) get more space than table-stakes features every competitor also has.

### Sign-up flow

Ask for the minimum information needed to create an account; every additional required field before a user has experienced any value is a point where they can abandon. Defer non-essential information (company size, use case details) to onboarding after signup, or make it optional.

## Never do this

- Never default to the generic hero-features-testimonials-pricing-FAQ-CTA sequence without a specific reason this product needs exactly that structure.
- Never hide a pricing tier's real terms (annual-only pricing, usage caps) until checkout.
- Never inflate a free tier's advertised limits beyond what's actually enforced in the product.
- Never require account creation to include fields that aren't actually needed to create the account.
- Never illustrate what the product does with an abstract graphic when a real screenshot or demo would show it directly.

## Verification checklist

- [ ] The landing page states the specific problem and audience within the first screen
- [ ] A real screenshot or demo of the actual product is shown, not only abstract illustration
- [ ] Pricing tiers are presented in a genuinely scannable comparison, with billing terms and cancellation policy stated plainly
- [ ] Any "recommended" tier reflects real best-value reasoning for the target audience
- [ ] Free tier or trial limits stated on the pricing page match what's actually enforced
- [ ] The signup form asks only for what's needed to create the account
