---
name: legal-compliance-pages
description: 'Use this skill whenever building a site that collects any user data (forms, accounts, analytics, cookies) or sells anything, and whenever a user asks to "add a privacy policy," "add terms of service," or "add a cookie banner." Also apply it by default before any site launches publicly, since operating without these pages is a real legal and trust liability, not just a missing nice-to-have page. This skill does not replace legal counsel for a business with real compliance exposure; it covers the baseline every site should have in place.'
---

# Legal and Compliance Pages

## Why this matters

A privacy policy and terms of service are not decorative footer links; they are often legally required (GDPR in the EU, CCPA in California, and similar laws elsewhere) the moment a site collects any personal data, including through analytics or a contact form. Beyond legal exposure, their absence is also a trust signal visitors and sophisticated buyers actively look for; a site asking for payment or personal information with no visible privacy policy reads as unprofessional at best.

## Do this

### Privacy policy

Cover, at minimum: what data is collected (forms, cookies, analytics), why, how it's used, whether it's shared with third parties (payment processors, analytics providers, email tools), how long it's retained, and how a user can request deletion or access. Generate this from the site's actual data practices, not a generic template pasted in unchanged; a policy that describes practices the site doesn't actually follow is itself a compliance problem.

### Terms of service

Cover, at minimum: acceptable use of the site/product, account terms if applicable, payment and refund terms if the site sells anything, limitation of liability, and how disputes are handled. For a simple marketing site with no accounts or transactions, a lighter terms page covering acceptable use and liability is sufficient; don't force a full SaaS-style terms document onto a business model that doesn't need one.

### Cookie consent

Implement real, functioning consent, not a decorative banner that shows up and does nothing when dismissed.

- Non-essential cookies (analytics, marketing/ad trackers) should not fire until the user has actually consented, for any visitor covered by GDPR/similar regimes; a banner that says "we use cookies" with only an "OK" button while trackers are already running before that click is not real consent.
- Provide a genuine "reject" or "manage preferences" option alongside "accept," not accept-only.
- Remember the user's choice (a cookie or local storage flag) so the banner doesn't reappear every visit, and provide a way to change the choice later (a footer link to reopen preferences).
- For a low-complexity site using only essential cookies (session, no tracking), a simple, honest banner is enough; don't build a full consent-management platform where it isn't warranted, but don't skip the banner because building it fully feels heavy either.

## Never do this

- Never publish a boilerplate privacy policy or terms page copied from an unrelated business without adapting it to what the site actually does.
- Never fire analytics or marketing trackers before consent is given, in a jurisdiction where that consent is required.
- Never build an accept-only cookie banner with no real reject/manage option for a site with EU or similarly-regulated traffic.
- Never present these as static image or hardcoded copy the site owner can't actually update as their data practices change; make it a normal editable page.

## Verification checklist

- [ ] Privacy policy accurately reflects the site's real data collection and sharing practices
- [ ] Terms of service is present and scoped appropriately to the actual business model (simple site vs. transactional/SaaS)
- [ ] Non-essential cookies/trackers do not fire before consent, where required
- [ ] Cookie banner offers a genuine reject/manage option, not accept-only
- [ ] User's consent choice persists and can be changed later
- [ ] Both pages are linked from the footer and reachable from every page
