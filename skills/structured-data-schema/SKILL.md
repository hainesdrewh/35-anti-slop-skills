---
name: structured-data-schema
description: 'Use this skill whenever adding structured data or schema markup to a site, and whenever a user asks to "add schema," "get rich results in Google," "add FAQ schema," or "help my business show up better in search." Also apply it by default for any business site, local business site, service page, or FAQ section, since structured data is what lets search engines display rich results (star ratings, FAQ dropdowns, business info panels) instead of a plain blue link. This skill always includes validating the markup, not just writing it; schema that has never been checked in Google''s Rich Results Test is a common way broken markup ships unnoticed.'
---

# Structured Data and Schema Markup

## Why this matters

Structured data (JSON-LD, the current recommended format) tells search engines exactly what a piece of content is, a business, a service, a review, a question and answer, rather than making them infer it from surrounding text. Done correctly, it's what unlocks rich results: star ratings next to a search listing, an expandable FAQ directly in search results, or a knowledge-panel-style business info card. Done incorrectly (a common outcome when it's copy-pasted without adapting the fields), it can be ignored or, worse, flagged as an error in Search Console. Copy-paste templates exist in [references/schema-templates.md](references/schema-templates.md); this file covers how to use and validate them correctly.

## Do this

### Organization schema

Include on the homepage at minimum, describing the business itself.

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Cool Air HVAC",
  "url": "https://example.com",
  "logo": "https://example.com/logo.png",
  "sameAs": [
    "https://www.facebook.com/example",
    "https://www.instagram.com/example"
  ]
}
```

### LocalBusiness schema

For any business with a physical location or defined service area, use the specific subtype where one exists (`HVACBusiness`, `Plumber`, `Restaurant`, `Dentist`) rather than the generic `LocalBusiness` type, since a more specific type unlocks more relevant rich-result treatment.

```json
{
  "@context": "https://schema.org",
  "@type": "HVACBusiness",
  "name": "Cool Air HVAC",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "123 Main St",
    "addressLocality": "Fort Worth",
    "addressRegion": "TX",
    "postalCode": "76102",
    "addressCountry": "US"
  },
  "telephone": "+18175550142",
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

### Service schema

On each dedicated service page (see [`local-service-seo`](../local-service-seo/SKILL.md)).

```json
{
  "@context": "https://schema.org",
  "@type": "Service",
  "serviceType": "AC Repair",
  "provider": {
    "@type": "HVACBusiness",
    "name": "Cool Air HVAC"
  },
  "areaServed": "Fort Worth, TX"
}
```

### FAQ schema

Only mark up FAQ content that's genuinely visible on the page as an FAQ; using FAQ schema on content that isn't actually presented as questions and answers to the visitor is against Google's guidelines and risks the markup being ignored or the page being flagged.

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Do you offer same-day AC repair?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Yes, most calls received before noon are completed the same day."
      }
    }
  ]
}
```

### Validate every schema block before shipping

Writing the JSON-LD is not the finish line. Run every page's markup through Google's Rich Results Test (search.google.com/test/rich-results) or the Schema Markup Validator, for each schema type added:

1. Paste the live page URL or the raw HTML into the tool.
2. Confirm each intended schema type is detected with zero errors, and review warnings even if they don't block eligibility.
3. Re-validate after any content change that touches a field referenced in the schema (a phone number update, a changed business name), since drift between the visible content and the schema is itself a quality signal search engines check.

## Never do this

- Never mark up content as an FAQ (or any schema type) that doesn't genuinely match what's visibly presented to the user on the page.
- Never copy a schema template from another business's site without replacing every field with this business's actual, accurate data.
- Never ship schema markup that's never been run through a validator; "the JSON is well-formed" is not the same as "the markup is valid and eligible for rich results."
- Never let the schema drift out of sync with visible page content after edits.

## Verification checklist

- [ ] Organization schema present on the homepage with accurate name, URL, logo, and social links
- [ ] LocalBusiness (or the most specific applicable subtype) schema present with accurate address, phone, and hours
- [ ] Service schema present on each dedicated service page
- [ ] FAQ schema present only where content is genuinely presented as an FAQ on the page
- [ ] Every schema block has been run through Google's Rich Results Test with no errors
- [ ] Schema fields match the actual visible page content exactly

See [references/schema-templates.md](references/schema-templates.md) for additional copy-paste-ready templates (Article, Review/AggregateRating, BreadcrumbList).
