---
name: technical-seo-crawlability
description: 'Use this skill whenever launching a new site or making it publicly accessible for the first time, and whenever a user asks to "submit this to Google," "add a sitemap," "add robots.txt," or "set up Search Console." Also use it proactively for any production site, since these files are invisible in normal browsing but directly control whether and how search engines and AI crawlers can find, index, and correctly attribute the site''s pages.'
---

# Technical SEO and Crawlability

## Why this matters

A page can have perfect on-page SEO and still never be found if the infrastructure that tells crawlers what to index, what to ignore, and which URL is canonical is missing or misconfigured. These files are also exactly the kind of thing that's easy to forget because nothing visibly breaks in a browser when they're absent; the site looks fine to a human visitor while being effectively invisible or miscategorized to search engines.

## Do this

### sitemap.xml

Generate a real `sitemap.xml` listing every real, indexable page (not draft/admin/internal routes), served at `/sitemap.xml`, and reference it in `robots.txt`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://example.com/</loc>
    <lastmod>2026-08-01</lastmod>
  </url>
  <url>
    <loc>https://example.com/services/ac-repair</loc>
    <lastmod>2026-08-01</lastmod>
  </url>
</urlset>
```

For sites with a CMS or many dynamic pages (blog posts, product pages), generate the sitemap programmatically at build or request time so it stays current automatically, rather than maintaining it by hand.

### robots.txt

Write a real, intentional `robots.txt`, not the framework default (which is sometimes a blanket `Disallow: /` left over from a staging environment, silently blocking the entire site from being indexed once it goes to production).

```
User-agent: *
Allow: /
Disallow: /admin/
Disallow: /api/

Sitemap: https://example.com/sitemap.xml
```

Always double-check this file specifically after deploying to production; a staging-environment `Disallow: /` that never got removed is one of the most common and most damaging technical SEO mistakes.

### llms.txt

`llms.txt` is an emerging convention (served at `/llms.txt`) that gives AI crawlers and assistants a curated, structured summary of the site: what it is, its key pages, and content meant to be surfaced in AI-generated answers. It's not yet universally adopted by every crawler, but costs little to add and positions the site for the growing share of discovery that happens through AI assistants rather than traditional search.

```
# Example Business Name

> Family-owned HVAC company in Fort Worth, TX, providing AC repair and installation since 2009.

## Key Pages
- [Services](https://example.com/services): Full list of AC repair and installation services
- [Service Area](https://example.com/service-area): Cities served
- [Contact](https://example.com/contact): Phone, email, and hours
```

### Canonical tags

Set a canonical tag on every page pointing to its preferred URL, which prevents duplicate-content issues from URL variants (with/without trailing slash, with tracking parameters, `http` vs `https`, `www` vs non-`www`) being treated as separate competing pages.

```html
<link rel="canonical" href="https://example.com/services/ac-repair">
```

Every page should self-canonicalize to its own clean URL by default; canonical tags pointing elsewhere are only for genuine duplicate-content cases (e.g. a filtered product-listing URL canonicalizing back to the unfiltered version).

### Google Search Console

Verify site ownership in Google Search Console and submit the sitemap through it, rather than relying purely on organic crawling to discover pages. This also surfaces indexing errors, manual actions, and search-performance data that are otherwise invisible.

1. Verify ownership (DNS record, HTML file upload, or meta tag, per Search Console's instructions).
2. Submit the sitemap URL under Sitemaps.
3. Check the Coverage/Indexing report periodically for crawl errors, not just once at setup.

## Never do this

- Never leave a staging `Disallow: /` in `robots.txt` after deploying to production.
- Never maintain a sitemap by hand on a site where pages are added or removed dynamically; it will drift out of date.
- Never set a canonical tag that points away from a page's own real, indexable URL without a specific duplicate-content reason.
- Never skip Search Console verification, treating organic discovery as sufficient.

## Verification checklist

- [ ] `sitemap.xml` exists at `/sitemap.xml`, lists all real indexable pages, and is kept current (ideally generated automatically)
- [ ] `robots.txt` is intentional, not a leftover staging blanket-disallow, and references the sitemap
- [ ] `llms.txt` exists with a clear summary and key page links
- [ ] Every page has a canonical tag pointing to its correct, clean URL
- [ ] Site is verified in Google Search Console and the sitemap is submitted
- [ ] Search Console's coverage/indexing report shows no unexpected errors
