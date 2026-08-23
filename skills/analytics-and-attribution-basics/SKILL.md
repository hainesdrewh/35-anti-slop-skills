---
name: analytics-and-attribution-basics
description: 'Use this skill whenever setting up analytics, tracking marketing campaign performance, or adding UTM parameters to links. Also use it when a user asks to "track where our traffic comes from," "set up analytics," or "see which ads are working." Covers keeping tracking useful and privacy-respecting, in coordination with legal-compliance-pages for consent requirements, rather than either skipping measurement entirely or over-tracking in a way that creates compliance risk.'
---

# Analytics and Attribution Basics

## Why this matters

A business that can't tell which marketing effort actually drove a lead or sale is flying blind on where to spend the next dollar. At the same time, tracking has to coexist with real privacy obligations (see [`legal-compliance-pages`](../legal-compliance-pages/SKILL.md)); the goal here is measuring what actually matters, not maximizing the amount of data collected.

## Do this

### UTM tracking conventions

Use consistent UTM parameters on every link shared in a trackable channel (paid ads, email campaigns, social posts, a QR code on a printed flyer) so traffic sources are distinguishable in analytics.

```
https://example.com/?utm_source=facebook&utm_medium=paid-social&utm_campaign=spring-promo
```

- `utm_source`: the specific platform (`facebook`, `google`, `newsletter`).
- `utm_medium`: the channel type (`paid-social`, `email`, `cpc`, `organic-social`).
- `utm_campaign`: the specific campaign name, consistent across all its links.

Keep naming conventions consistent across the whole team/business (lowercase, consistent separators) since inconsistent casing or naming (`Facebook` vs `facebook`) fragments the same source into multiple entries in reports.

### Conversion tracking hygiene

Track the events that actually matter to the business (a form submission, a call click, a completed purchase, a booked appointment), not every possible interaction indiscriminately. Define what counts as a conversion clearly before setting up tracking, and confirm each tracked event actually fires correctly (test it directly, don't assume the implementation is correct) rather than discovering months later that a conversion event silently never fired.

### Privacy-respecting analytics

- Only load analytics/tracking scripts after consent where required (see [`legal-compliance-pages`](../legal-compliance-pages/SKILL.md)); this is a hard requirement, not a nice-to-have, in jurisdictions covered by GDPR and similar regimes.
- Consider privacy-focused analytics tools (that don't rely on individual cross-site tracking cookies) where the business's needs don't specifically require granular cross-site attribution; this often simplifies consent requirements considerably.
- Avoid collecting more personal data than the business actually uses to make decisions; a field collected "just in case" is a liability with no offsetting benefit if it's never actually analyzed.

## Never do this

- Never use inconsistent UTM naming across campaigns, which fragments reporting and makes source comparison unreliable.
- Never fire analytics/marketing trackers before consent where consent is legally required.
- Never set up conversion tracking without verifying it actually fires correctly in a real test.
- Never collect personal data beyond what's genuinely used, just because a tracking tool makes it easy to capture.

## Verification checklist

- [ ] UTM parameters follow a consistent naming convention across every campaign and channel
- [ ] Defined conversion events are tested and confirmed to fire correctly, not just assumed to work
- [ ] Analytics/tracking scripts respect consent requirements per `legal-compliance-pages`
- [ ] No personal data is collected beyond what the business actually uses
