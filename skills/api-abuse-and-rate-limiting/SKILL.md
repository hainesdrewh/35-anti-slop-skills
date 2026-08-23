---
name: api-abuse-and-rate-limiting
description: 'Use this skill whenever building any public API endpoint, a signup or login flow, a contact form, or any feature that calls a paid third-party API (especially an AI/LLM API) on a user''s behalf. Also use it when a user asks to "add an AI feature," "let users generate content," "add a free tier," or "add a contact form," and whenever reviewing an application for abuse resistance before launch. The default failure modes this prevents: unlimited requests draining a paid API budget, scripted bots farming free-tier signups for unlimited usage, and public endpoints with no rate limit being trivially hammered or scraped.'
---

# API Abuse and Rate Limiting

## Why this matters

Any endpoint that costs money per call (an LLM API, a paid email/SMS provider, a metered database) or that gates a limited free resource (a free-tier credit balance, a single-use discount code) will be found and abused if it has no limit, and this happens faster than most teams expect, often within days of a product getting any real traffic or exposure. This is one of the few security categories that directly threatens a business's operating budget, not just its data, since an unmetered AI feature can produce a large bill overnight from scripted abuse alone.

## Do this

### Rate-limit every public endpoint, not just login

Apply rate limiting broadly, keyed by a combination of IP address and authenticated user ID where available, since either alone is bypassable (IPs rotate, accounts multiply).

```js
// Example using a token-bucket style limiter (concept, adapt to the actual stack)
const limiter = rateLimit({ windowMs: 60_000, max: 20, keyGenerator: (req) => req.user?.id ?? req.ip });
app.use('/api/', limiter);
```

Set stricter limits on expensive or abuse-prone endpoints specifically (AI generation calls, password reset, signup, search) than on cheap read-only endpoints.

### Cap AI/LLM usage per user

Track usage per user (request count, token count, or spend) against an explicit cap, enforced server-side before the call to the underlying provider is made, not just displayed as a soft warning in the UI. For a free tier, the cap needs to be low enough that abusing it isn't profitable for a scripted account-farming operation, and for a paid tier, overages should be blocked or explicitly billed, never silently absorbed by the business.

```js
// Enforce before calling the provider, not after
const usage = await getUsage(userId);
if (usage.tokensThisMonth >= plan.tokenLimit) {
  throw new UsageLimitError();
}
const result = await callLLM(prompt);
await recordUsage(userId, result.tokensUsed);
```

### Limit request size

Cap request body size at the framework or reverse-proxy level (e.g. a few hundred KB for a typical JSON API, larger only where a specific feature genuinely needs it, like file upload) to prevent oversized payloads from being used to exhaust memory or bandwidth.

### Add bot protection to forms and signup

Use a CAPTCHA or an invisible challenge service (Cloudflare Turnstile, hCaptcha) on signup, login, and any public form (contact, waitlist) that's a realistic spam target. Pair this with rate limiting rather than relying on either alone; a CAPTCHA slows down casual scripting, while rate limiting bounds the damage from anything that gets past it.

### Block scripted signup/login spam and free-tier farming specifically

- Require email verification before granting meaningful free-tier resources, so a single throwaway address can't instantly claim a fresh credit balance.
- Watch for the specific pattern of many accounts created in quick succession from the same IP or a narrow IP range, and throttle or flag it rather than treating every signup as independent.
- Where the abuse risk is high (a generous free AI credit, a referral bonus), consider requiring a verified phone number or payment method on file even for a "free" tier, which meaningfully raises the cost of farming accounts.

## Never do this

- Never ship an endpoint that calls a metered third-party API with no per-user cap, "to see what usage looks like first." Usage from an abuse script looks identical to legitimate usage in the first few minutes and very different in the bill.
- Never rely on a client-side check (a disabled button, a JS counter) as the actual enforcement mechanism for a usage limit; it does nothing against a direct API call.
- Never assume low current traffic means abuse resistance can wait; a public AI feature can be discovered and scripted against within hours of being shared anywhere.

## Verification checklist

- [ ] Every public API endpoint has a rate limit, not only the login endpoint
- [ ] Rate limits are keyed by user ID where authenticated, IP otherwise, and account for both being spoofable
- [ ] Any call to a paid third-party API enforces a per-user usage cap server-side, before the call is made
- [ ] Request body size is capped at the framework/proxy level
- [ ] Signup, login, and public forms have bot protection (CAPTCHA or equivalent challenge)
- [ ] Free-tier resources require email verification (or stronger) before being granted
- [ ] Rapid multi-account creation from the same source is throttled or flagged, not treated as independent normal signups
