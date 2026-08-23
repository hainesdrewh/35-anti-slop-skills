---
name: conversion-ctas
description: 'Use this skill whenever placing calls to action on a page, building a form-submission flow, or setting up checkout/pricing display. Also use it when a user asks to "add a CTA," "improve conversions," "add a thank-you page," or "make the pricing clearer." Covers where and how CTAs should appear, what happens after a form is submitted, and making sure pricing/payment terms are stated honestly rather than obscured until checkout.'
---

# Conversion CTAs

## Why this matters

A visitor who is ready to act (call, buy, sign up) and can't quickly find how, or hits an unclear or dishonest pricing moment right before committing, leaves. Every item here is about removing friction and ambiguity at the exact moments that matter most for conversion, not about aggressive dark-pattern persuasion tactics.

## Do this

### CTA above the fold

The primary action a visitor should take (call, book, buy, sign up) needs to be visible without scrolling on both desktop and mobile. This doesn't mean the entire hero has to be an ad for the CTA; it means the path to act is immediately visible, not something a visitor has to hunt for after scrolling through several sections.

### CTA placement and copy throughout the page

- Repeat the primary CTA at natural decision points down the page (after key content sections, not just once at the very top and bottom), rather than forcing every visitor to scroll back up.
- Use specific, action-describing copy ("Get a Free Quote," "Call Now," "Start Your Trial") rather than a generic "Submit" or "Click Here," which gives no indication of what happens next.
- Keep one clear primary CTA per section rather than competing CTAs of equal visual weight that force the visitor to choose between two similarly-styled options.

### Thank-you pages

After a form submission or purchase, redirect to a real, specific thank-you page rather than leaving the visitor on the same form with only a small inline message they might miss (this also gives a clean event to track for analytics, see [`analytics-and-attribution-basics`](../analytics-and-attribution-basics/SKILL.md)).

A good thank-you page confirms the specific action taken ("Thanks, we've received your request and will call within one business day"), sets a clear expectation for what happens next, and offers a next step (a phone number for urgent needs, a link back to relevant content) rather than being a dead end.

### Payment method clarity

State pricing and payment terms plainly before the visitor is committed, not revealed only at the final step of checkout. Show what payment methods are accepted, whether there are additional fees (taxes, service charges) not included in the displayed price, and any recurring-billing terms clearly, before asking for payment details. A price that changes or reveals hidden fees only at the last step is a well-known trust-destroying pattern, not just a UX nitpick.

## Never do this

- Never bury the primary CTA below multiple scrolls of content with no earlier prompt to act.
- Never use vague CTA copy ("Submit," "Click Here," "Learn More" as the only action on a page meant to convert) that doesn't describe the actual outcome.
- Never leave a visitor on the same form page after submission with only an easily-missed inline confirmation.
- Never reveal additional fees, less-favorable terms, or payment methods only at the final checkout step after the visitor has already invested time in the flow.

## Verification checklist

- [ ] The primary CTA is visible above the fold on both desktop and mobile
- [ ] The CTA repeats at natural points down the page, not only once
- [ ] CTA copy is specific and describes the actual action/outcome
- [ ] Form submissions and purchases redirect to a real, specific thank-you page
- [ ] The thank-you page confirms the action and sets a clear next-step expectation
- [ ] Full pricing, fees, and accepted payment methods are stated before the final checkout step, not revealed late
