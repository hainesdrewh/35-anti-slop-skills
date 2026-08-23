---
name: local-service-seo
description: 'Use this skill whenever building a site for a local business, a service-area business (plumbers, electricians, landscapers, HVAC, contractors, salons, clinics), or any business that serves customers in a specific geographic area. Also use it when a user asks to "rank in local search," "show up on Google Maps," "add service pages," or "target customers in my city." Local search behaves differently from general SEO, ranking is heavily influenced by consistent business information and location/service-specific content, not just general on-page quality.'
---

# Local and Service-Business SEO

## Why this matters

Local search (Google Maps results, the local pack, "near me" queries) uses different ranking signals than general organic search, and a site built with only generic on-page SEO in mind (see [`on-page-seo`](../on-page-seo/SKILL.md)) will underperform for a business that actually depends on local discovery. The businesses this matters most for, contractors, clinics, salons, restaurants, are also exactly the ones most likely to end up with a generic template site if this skill isn't applied deliberately.

## Do this

### Service pages

Create a dedicated page per real service, not one page trying to describe everything. Each service page should cover: what the service includes, what it costs (a real range, or clear "request a quote" if pricing genuinely varies), why this business specifically for this service, and a clear call to action. A single "Services" page with a paragraph per service is weaker for both users and search than dedicated pages, each targeting its own specific search intent.

### Location pages

For a business serving multiple distinct areas, create a dedicated page per real service area (city or region), each with genuinely unique content (not the same template with only the city name swapped), covering: confirmation the business serves that specific area, any location-specific detail (local landmarks, area-specific regulations, response-time expectations for that area), and the same conversion path as every other page. A location page that's identical except for a find-and-replaced city name is a well-known thin-content pattern that underperforms and can be penalized.

### Local keywords

Naturally incorporate the actual service plus location combination a real searcher would type ("emergency plumber in Fort Worth," not just "plumber" or just "Fort Worth") into titles, headings, and body copy, written the way a person would actually search and speak, never as an unnaturally repeated keyword string.

### Opening hours

Mark up hours with actual structured data, not just an image or a plain-text line buried in the footer, so search engines and Google Business Profile can surface accurate open/closed status.

```json
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "Cool Air HVAC",
  "openingHoursSpecification": [
    {
      "@type": "OpeningHoursSpecification",
      "dayOfWeek": ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"],
      "opens": "08:00",
      "closes": "18:00"
    }
  ]
}
```

See [`structured-data-schema`](../structured-data-schema/SKILL.md) for the full LocalBusiness schema this belongs inside.

### NAP consistency

Name, Address, and Phone number must appear identically, character for character, everywhere they're listed: the site itself, Google Business Profile, and any directory listings (Yelp, industry-specific directories). Inconsistent formatting ("St." vs "Street," a different phone number format, an old address left on one listing) actively hurts local ranking, since search engines use NAP matching across sources as a trust signal.

## Never do this

- Never publish location pages that are identical except for a swapped city name; each needs genuinely distinct, useful content.
- Never let the business's name, address, or phone number differ even slightly across the site, Google Business Profile, and directory listings.
- Never bury opening hours in an image or unstructured text with no markup.
- Never target a broad keyword ("plumber") when the business only serves a specific area; the location-qualified version converts better and faces less competition.

## Verification checklist

- [ ] Each real service has its own dedicated page, not a shared generic services page
- [ ] Each real service area has its own page with genuinely distinct content, not a template with only the city swapped
- [ ] Service-plus-location keyword combinations appear naturally in titles, headings, and copy
- [ ] Opening hours are marked up as structured data, not just an image or plain text
- [ ] NAP (name, address, phone) is identical across the site, Google Business Profile, and any directory listings
