# Additional Schema Templates

Copy-paste starting points. Replace every field with the real business's actual data, and validate in Google's Rich Results Test after adapting, per the parent SKILL.md.

## Article (for blog posts)

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "5 Signs Your AC Needs Repair Before Summer",
  "author": {
    "@type": "Person",
    "name": "Jane Smith"
  },
  "datePublished": "2026-03-01",
  "dateModified": "2026-03-01",
  "image": "https://example.com/blog/ac-signs.jpg"
}
```

## Review and AggregateRating (only with real reviews)

Never populate this with fabricated ratings; see [`review-testimonials-social-proof`](../../review-testimonials-social-proof/SKILL.md). Only mark up review counts and averages that are genuinely collected and displayed on the page.

```json
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "Cool Air HVAC",
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.8",
    "reviewCount": "127"
  }
}
```

## BreadcrumbList

See [`breadcrumbs-internal-linking`](../../breadcrumbs-internal-linking/SKILL.md) for the full breadcrumb treatment; this is the schema half.

```json
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    {
      "@type": "ListItem",
      "position": 1,
      "name": "Home",
      "item": "https://example.com/"
    },
    {
      "@type": "ListItem",
      "position": 2,
      "name": "Services",
      "item": "https://example.com/services"
    },
    {
      "@type": "ListItem",
      "position": 3,
      "name": "AC Repair",
      "item": "https://example.com/services/ac-repair"
    }
  ]
}
```
