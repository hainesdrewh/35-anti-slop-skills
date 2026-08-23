---
name: on-page-seo
description: 'Use this skill whenever creating or editing any web page''s title, meta description, headings, or body copy, and whenever a user asks to "improve SEO," "add meta tags," "optimize this page for search," or "make this rank better." Also apply it by default when generating any new page, not only when SEO is explicitly requested, since these fundamentals cost nothing to get right at creation time and are expensive to retrofit across dozens of pages later.'
---

# On-Page SEO

## Why this matters

On-page SEO is the layer search engines use to understand what a page is actually about, before ranking factors like backlinks or authority ever come into play. A page with a missing or generic title, no meta description, and a heading structure that's just bold text can rank poorly even with excellent content, because the signals search engines rely on to categorize and summarize the page are simply absent.

## Do this

### Page titles

- Every page needs a unique `<title>`, roughly 50 to 60 characters, that describes that specific page's content, not a copy-pasted site-wide title.
- Put the most important, specific term near the front: "Same-Day AC Repair in Fort Worth | [Business Name]" rather than "[Business Name] | Home."
- Avoid keyword-stuffing the title with repeated variations of the same term; write it as a real, readable phrase a human would click on in search results.

```html
<title>Same-Day AC Repair in Fort Worth | Cool Air HVAC</title>
```

### Meta descriptions

- Write a unique meta description per page, roughly 150 to 160 characters, that accurately summarizes the page and gives a reason to click (search engines display this as the snippet under the title in results).
- Never leave it blank or duplicate it across pages; search engines will otherwise generate their own snippet from page content, which is unpredictable and often less compelling.

```html
<meta name="description" content="Family-owned HVAC company serving Fort Worth since 2009. Same-day AC repair, licensed and insured, no dispatch fee if we can't fix it same-visit.">
```

### Keyword-rich headings (real hierarchy, not just bold text)

- Use exactly one `<h1>` per page, containing the primary topic/keyword for that page.
- Use `<h2>` through `<h6>` to reflect actual content structure (sections and subsections), not as a way to make text bigger; a heading level should never be chosen purely for visual weight.
- Work the page's actual topic and relevant, natural-language keyword variations into headings where they genuinely fit, never forced in a way that reads as unnatural to a human visitor.

```html
<h1>Same-Day AC Repair in Fort Worth</h1>
<h2>Our AC Repair Services</h2>
<h3>Emergency No-Cool Calls</h3>
<h3>Routine Maintenance and Tune-Ups</h3>
```

### Internal links

- Link between related pages using descriptive anchor text ("see our AC maintenance plans," not "click here").
- Every real page on the site should be reachable via at least one internal link from somewhere else on the site; an orphaned page with no internal links pointing to it is both a discoverability problem for users and a signal problem for search engines. See [`breadcrumbs-internal-linking`](../breadcrumbs-internal-linking/SKILL.md) for the deeper linking strategy.

### Image alt text

- Every meaningful image needs `alt` text that describes its actual content and, where relevant, naturally incorporates the page's topic ("technician repairing a rooftop AC unit in Fort Worth," not "image1.jpg" or a generic "AC unit").
- Purely decorative images (background textures, spacers) should use `alt=""` (empty, not omitted) so screen readers correctly skip them rather than reading a filename.
- Never stuff alt text with repeated keywords; it must accurately describe the image first, since it also serves screen-reader users directly, not just search engines.

## Never do this

- Never leave a page with a framework-default or duplicate title across multiple pages.
- Never leave the meta description blank, or copy the exact same one across every page.
- Never use heading tags purely for font size; use CSS for visual sizing and heading tags for actual structure.
- Never stuff keywords unnaturally into titles, headings, or alt text at the expense of readability.

## Verification checklist

- [ ] Every page has a unique, descriptive `<title>` in the ~50-60 character range
- [ ] Every page has a unique, accurate meta description in the ~150-160 character range
- [ ] Exactly one `<h1>` per page, and heading levels reflect real content structure
- [ ] Internal links use descriptive anchor text, and every real page is reachable via at least one internal link
- [ ] Every meaningful image has accurate, non-generic alt text; decorative images use `alt=""`
- [ ] No keyword-stuffing in titles, headings, or alt text
