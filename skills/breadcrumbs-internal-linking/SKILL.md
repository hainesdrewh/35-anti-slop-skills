---
name: breadcrumbs-internal-linking
description: 'Use this skill whenever building a site with more than a couple of levels of page hierarchy (services under categories, blog posts under topics, products under collections), and whenever a user asks to "add breadcrumbs" or "improve site navigation." Also apply it whenever adding new pages to an existing site, to make sure the internal linking structure keeps every page discoverable rather than accumulating orphaned pages over time.'
---

# Breadcrumbs and Internal Linking

## Why this matters

Breadcrumbs and a deliberate internal linking structure serve the same underlying purpose from two angles: helping a visitor understand where they are and move around efficiently, and helping search engines understand the site's structure and find every page. A site that relies only on top-level nav for discovery tends to accumulate pages reachable only by a direct URL, which both users and search engines are unlikely to ever find.

## Do this

### Breadcrumb navigation

Add breadcrumbs to any page more than one level deep in the site's hierarchy, showing the actual path from the homepage to the current page, each level a real, working link.

```html
<nav aria-label="Breadcrumb">
  <ol>
    <li><a href="/">Home</a></li>
    <li><a href="/services">Services</a></li>
    <li aria-current="page">AC Repair</li>
  </ol>
</nav>
```

Pair this with BreadcrumbList schema (see [`structured-data-schema`](../structured-data-schema/SKILL.md)) so search engines can display the breadcrumb path directly in search results instead of a raw URL.

### Internal linking strategy

- Every real, indexable page should be reachable via at least one link from somewhere else on the site, not just from an external share link or a sitemap entry no human ever clicks; a page with zero internal links pointing to it is effectively orphaned.
- Link contextually within content, not just through nav and footer: a blog post mentioning a specific service should link to that service's page, using descriptive anchor text that states what the destination actually is ("our AC maintenance plans," not "click here" or the bare URL).
- Avoid excessive, unnatural link density that reads as manipulative rather than genuinely helpful to a reader; link where it adds real value to the visitor's next step, not on every possible keyword occurrence.

### Auditing for orphaned pages

Periodically crawl the site (the same tools used in [`pre-launch-technical-audit`](../pre-launch-technical-audit/SKILL.md) for broken-link checking can also report pages with zero inbound internal links) and either add a real link to any orphaned page or remove it if it no longer serves a purpose.

## Never do this

- Never ship a breadcrumb trail that doesn't match the page's real hierarchy, or that isn't actually clickable.
- Never publish a page reachable only through a direct URL with zero internal links pointing to it.
- Never use "click here" or a bare URL as link text where descriptive anchor text would tell the visitor (and search engines) what the destination actually is.

## Verification checklist

- [ ] Pages more than one level deep show accurate, working breadcrumb navigation
- [ ] Breadcrumbs are paired with BreadcrumbList schema
- [ ] Every real, indexable page has at least one internal link pointing to it from elsewhere on the site
- [ ] Contextual in-content links use descriptive anchor text, not "click here" or bare URLs
- [ ] A periodic crawl confirms no orphaned pages remain undiscovered
