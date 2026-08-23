---
name: ecommerce-layout-patterns
description: 'Use this skill whenever building an online store: a product detail page, a category/collection page, a cart, or a checkout flow. Also use it when a user asks to "add a shop," "build a product page," "add a cart," or "add checkout." Covers the specific conversion-critical details of commerce UI (trust signals at the point of payment, real stock/shipping information, a checkout that doesn''t lose the customer) that a generic content-page template does not address, in coordination with file-upload-and-payment-integrity for the backend side and conversion-ctas for general CTA principles.'
---

# E-commerce Layout Patterns

## Why this matters

Commerce pages carry a specific kind of pressure a content page doesn't: a visitor with money in hand who can abandon at any point with zero cost to them and real cost to the business. Every additional point of friction, an unclear price, a hidden shipping cost revealed late, an unconvincing product photo, a checkout that feels untrustworthy, directly costs revenue in a way that's measurable and that competitors are actively optimizing against. Applying [`data-grid-and-listing-pages`](../data-grid-and-listing-pages/SKILL.md) for the category grid and [`conversion-ctas`](../conversion-ctas/SKILL.md) for general CTA principles gets partway there; this skill covers what's specific to buying something.

## Do this

### Product detail page

- Real, high-quality photography from multiple angles, with at least one image showing genuine scale or context (worn, in use, next to a common object) rather than only an isolated studio shot; see [`image-sourcing-and-generation`](../image-sourcing-and-generation/SKILL.md) for sourcing photography honestly.
- Price stated plainly near the top, with any discount shown as a real, verifiable comparison (an actual prior price, not an inflated "was" price invented to manufacture a discount).
- Real stock/availability status ("In stock," "Only 3 left," "Ships in 2-3 days") rather than silence on the question, which reads as evasive.
- Size/variant selection with clear visual feedback for the selected option and an obvious state for unavailable variants (grayed out, not silently absent).
- Genuine reviews (see [`review-testimonials-social-proof`](../review-testimonials-social-proof/SKILL.md)) specific to the product, not a generic site-wide rating applied to every item.
- Shipping and return policy information visible before checkout, not discovered for the first time at the final step.

### Category/collection page

Follow [`data-grid-and-listing-pages`](../data-grid-and-listing-pages/SKILL.md) for the grid itself. Additionally: sort controls (price, popularity, newest) with the current sort visibly indicated, and filter by the attributes that actually matter for this specific category (size and color for apparel, not a generic filter set copied from an unrelated store template).

### Cart

- Show each item with enough detail to recognize it at a glance (thumbnail, name, selected variant), the quantity control, and the per-item and running total, updated immediately when quantity changes, not only after a page reload.
- Make removing an item and changing quantity equally easy; a cart that makes removal harder to find than adding is a dark pattern, not an oversight.
- Surface shipping cost and any threshold for free shipping as early as possible, ideally in the cart itself, not held back until checkout.

### Checkout

- Minimize the number of steps and never require account creation before a first purchase; offer guest checkout, with account creation as an optional step after the order is placed.
- Show a persistent order summary throughout checkout so the total never comes as a surprise at the final step.
- State the accepted payment methods and any final fees (tax, shipping) before the final payment step, never introduced for the first time at that step.
- Confirm the order immediately with a real confirmation page and email, stating what was ordered, the total charged, and an estimated delivery window; see [`conversion-ctas`](../conversion-ctas/SKILL.md) for the thank-you-page standard this extends.
- All pricing and final charge computation must happen server-side per [`file-upload-and-payment-integrity`](../file-upload-and-payment-integrity/SKILL.md); this skill covers the layout and UX, that one covers why the price shown must be the price actually charged.

## Never do this

- Never invent a fake "was" price to manufacture the appearance of a discount.
- Never hide shipping cost or mandatory fees until the final checkout step.
- Never require account creation before a first purchase can be completed.
- Never make an item harder to remove from the cart than it was to add.
- Never show a generic, product-agnostic review score in place of real, product-specific reviews.

## Verification checklist

- [ ] Product photography is real, multi-angle, and includes at least one contextual/scale shot
- [ ] Stock/availability status is stated plainly, not left silent
- [ ] Any discount shown reflects a real prior price
- [ ] Cart updates totals immediately on quantity change and makes removal as easy as adding
- [ ] Shipping cost is visible in the cart, not held back until checkout
- [ ] Guest checkout is available; account creation is optional, not required
- [ ] All fees and the final total are shown before the final payment step, never introduced there for the first time
- [ ] A real order confirmation page and email are sent immediately after purchase
