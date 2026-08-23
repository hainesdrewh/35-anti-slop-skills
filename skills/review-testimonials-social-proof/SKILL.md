---
name: review-testimonials-social-proof
description: 'Use this skill whenever adding customer reviews, testimonials, author bios, or a guarantee statement to a site. Also use it when a user asks to "add testimonials," "show our reviews," or "add a guarantee." Draws a hard line between social proof that builds credibility and fabricated social proof that destroys it the moment a skeptical visitor checks, which they increasingly do.'
---

# Reviews, Testimonials, and Social Proof

## Why this matters

Social proof works because it's independently verifiable, or at least appears to be; a testimonial that reads as fabricated (generic praise, a stock headshot, no way to verify the person is real) doesn't just fail to help, it actively signals the business is willing to fabricate content, which undermines every other claim on the page. This is a direct extension of the anti-fabrication principle in [`anti-ai-slop-design`](../anti-ai-slop-design/SKILL.md), applied specifically to reviews and credibility content.

## Do this

### Customer reviews

Display real reviews, ideally sourced and linked from a verifiable third-party platform (Google Business Profile, Yelp, an industry-specific review site) rather than only self-hosted, unverifiable quotes. Where schema markup is used for ratings (see [`structured-data-schema`](../structured-data-schema/SKILL.md)), the rating count and average must reflect genuinely collected reviews, never an invented number.

- Full name and, where the reviewer has agreed, a specific, verifiable detail (their city, the specific service they used) makes a review read as real; "Great service! - Anonymous" does not.
- If the business genuinely has very few reviews so far, show the real (small) number rather than inflating it, and consider prioritizing an active request-for-reviews process over an aggressive display of what little exists.

### Author bios

Covered fully in [`blog-content-seo`](../blog-content-seo/SKILL.md); the same standard applies to any content with an attributed author, credit a real person with genuine, relevant credentials.

### Guarantee statements

A guarantee is a strong trust signal only if it's specific and genuinely honored. "100% satisfaction guaranteed" with no further detail reads as boilerplate; "If we can't fix it in one visit, the diagnostic fee is waived" is specific, credible, and actually differentiates the business. State the actual terms plainly, including any limits or conditions, rather than an unconditional-sounding claim the business doesn't actually intend to honor unconditionally.

## Never do this

- Never invent testimonials, reviewer names, or star ratings.
- Never use stock photography as a stand-in for a real reviewer's photo.
- Never display an aggregate rating or review count that doesn't match what's actually been collected.
- Never state a guarantee in absolute terms that the business doesn't actually intend to honor without conditions; be specific about the real terms instead.

## Verification checklist

- [ ] Every displayed review/testimonial is real, ideally with a link back to its source platform
- [ ] No stock photography used to represent a real reviewer
- [ ] Any displayed rating/review count schema matches genuinely collected data
- [ ] Guarantee statements are specific about actual terms and limits, not vague absolute claims
