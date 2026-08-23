---
name: image-sourcing-and-generation
description: 'Use this skill whenever a site needs an image and no real, client-provided photo is available: choosing freely-licensed stock photography, or prompting and evaluating an AI image generation tool. Also use it whenever a user asks to "find some images," "generate a hero image," or "add stock photos." This skill exists because sourcing an image by guessing a stock photo ID or generating one without checking it actually depicts the intended content is exactly how mismatched, wrong, or generic-looking images end up shipped, the specific failure contrast-and-image-integrity-checks exists to catch after the fact; this skill covers how to avoid causing it in the first place.'
---

# Image Sourcing and Generation

## Why this matters

An image that doesn't match what it's supposed to depict, wrong architectural style, wrong product, an obviously generic stock feel, actively damages credibility once a visitor with any domain knowledge notices, which is often immediate for the exact people the image is meant to persuade (a buyer who knows what a Craftsman home actually looks like, a customer who's seen this exact stock photo on a competitor's site too). Sourcing and generating images by trial and error without deliberately checking the result against what's actually needed is how this happens, not a rare edge case.

## Do this

### Search stock photography with a real strategy, not guesswork

Random guessing at stock-photo IDs or URLs produces whatever that specific photo happens to be, unrelated to what's needed; this is not a search strategy. Where a real search API is available (a stock photo service's actual search endpoint, a Wikimedia Commons category or full-text search), use it with specific, descriptive query terms matching the actual content needed, and always view the candidate result before using it, per [`contrast-and-image-integrity-checks`](../contrast-and-image-integrity-checks/SKILL.md), rather than trusting that a search result matching the query text will also match the query visually.

- Prefer sources with a clear, permissive license for the intended use (Unsplash's license, Pexels' license, openly-licensed Wikimedia Commons images), and note the source/license basis used, especially for anything that might go to production rather than stay a local demo.
- When searching by keyword returns a mix of relevant and irrelevant results, don't take the first result; review several and pick the one that actually matches the specific claim being made (style, subject, mood, setting).
- For a business site with no real photos yet, mark placeholder imagery as a known gap explicitly (see [`anti-ai-slop-design`](../anti-ai-slop-design/SKILL.md)'s placeholder-vs-fabrication distinction) rather than treating a stock photo as a permanent stand-in for what should eventually be real photography of the actual business.

### Prompt AI image generation deliberately

When generating an image rather than sourcing one:

- Write a specific, detailed prompt describing the actual subject, style, and setting needed, not a vague prompt hoping the model infers the right specifics; a vague prompt is the generative equivalent of guessing a stock photo ID.
- Specify a consistent style/mood across a set of generated images meant to appear together (a gallery, a set of team photos) so they don't visibly clash in lighting, rendering style, or color grade.
- Generate more than one candidate where the tool allows it, and pick the one that actually holds up under inspection, rather than accepting the first output.

### Check generated output for the specific tells that reveal it's AI-generated

Before using a generated image, look specifically for: distorted or extra fingers/limbs, nonsensical or garbled text rendered within the image, asymmetric or uncanny facial features, physically impossible reflections or shadows, and an overly smooth, waxy rendering style on skin or surfaces. Any of these, especially in an image meant to represent something real (a person, a specific product), is disqualifying; regenerate or switch to real photography instead.

### Never present a generated image as if it were a real photo of a specific real thing

A generated image can stand in for generic illustrative content (an abstract background texture, a conceptual illustration) more safely than it can for something the copy claims is specific and real (a photo captioned as if it depicts an actual completed project, an actual team member, an actual location). Where a generated image is used for something that reads as a claim of authenticity, consider whether the honest move is to label it as illustrative or replace it with real photography instead.

### Verify the final result against the actual claim, every time

Whether sourced or generated, run the image through the same check described in [`contrast-and-image-integrity-checks`](../contrast-and-image-integrity-checks/SKILL.md): does this image actually show what the adjacent copy says it shows. This is the step that actually prevents the failure this skill exists to avoid; sourcing or generating carefully and then skipping this final check still allows the same mismatch to ship.

## Never do this

- Never guess at a stock photo ID or URL and use whatever it happens to return without viewing and verifying it first.
- Never use a vague, non-specific prompt for an image meant to represent something specific.
- Never use a generated image with visible AI-generation tells (distorted hands, garbled text, uncanny faces) especially where it's meant to represent something real.
- Never present a generated image as an authentic photo of a specific real person, place, or completed project without at least considering whether that crosses into misrepresentation.
- Never skip the final verification that the image actually matches the claim next to it, regardless of how it was sourced.

## Verification checklist

- [ ] Every sourced stock image was found through an actual descriptive search and viewed before use, not selected by guessing an ID
- [ ] License/source basis is noted for any image likely to go to production
- [ ] Any generated image was created from a specific, detailed prompt, not a vague one
- [ ] Generated images meant to appear together share a consistent style/mood
- [ ] Generated images were checked for visible AI-generation tells before use, especially where representing something real
- [ ] Every image, sourced or generated, was verified against the specific claim in its surrounding copy before shipping
