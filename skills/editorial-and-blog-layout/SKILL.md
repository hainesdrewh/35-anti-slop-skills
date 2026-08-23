---
name: editorial-and-blog-layout
description: 'Use this skill whenever building the visual layout of a content-heavy, magazine- or publication-style site: a blog''s actual page templates, a news or editorial site, a newsletter archive. This is the layout-craft companion to blog-content-seo, which covers what to write and how to structure it for search; this skill covers how it should actually look and read once it''s a real page, and applies whenever reading is the primary activity on the page.'
---

# Editorial and Blog Layout

## Why this matters

A content site succeeds or fails on whether people actually read what's there, and reading comfort is determined almost entirely by typographic and layout decisions that are easy to get wrong by default: a body column too wide to read comfortably, a font not chosen for sustained reading, no clear hierarchy separating an article from the surrounding site chrome. [`typography-craft`](../typography-craft/SKILL.md) covers the underlying line-length and line-height rules; this skill covers how to apply them specifically to an editorial layout, plus the structural decisions specific to publication-style content.

## Do this

### Design the article template around sustained reading

- Cap body copy at a genuinely comfortable measure (see [`typography-craft`](../typography-craft/SKILL.md)), and choose a body typeface actually suited to long-form reading (real text weight and x-height, not a display face repurposed for body text).
- Give the article a clear visual distinction from surrounding chrome (nav, sidebar, related content) so a reader's eye settles into the content itself, not a page where everything competes for attention equally.
- Use a real, deliberate hierarchy for in-article headings, pull quotes, and image captions, distinct from the site's marketing-page heading styles; an article's H2 doesn't need to shout the way a landing page's H2 does.

### Handle the homepage/index as curation, not just a reverse-chronological dump

A pure reverse-chronological list is the easiest thing to build and often the weakest choice: feature the genuinely best or most relevant piece prominently, and let older or less central content recede in visual weight rather than treating every post as equally important by default.

### Design real, working metadata

Author, publish date, and (see [`custom-error-pages`](../custom-error-pages/SKILL.md) et al.'s general honesty principle) an honest last-updated date if content is revised, displayed consistently across every article, not just the ones where someone remembered to add it. Reading time estimates, if used, should be calculated from real word count, not a static guess copied across every post.

### Make related/next content genuinely relevant

An auto-generated "related posts" block that surfaces unrelated content by coincidence (same content type, wrong topic) actively hurts engagement, since a reader who clicks through to something irrelevant learns not to trust that section. See [`blog-content-seo`](../blog-content-seo/SKILL.md) for the underlying content-relationship requirement; this skill's concern is making sure the visual treatment doesn't overstate confidence in a weak match (don't present three unrelated posts as if they were a carefully chosen author's picks).

### Handle images as part of the reading experience, not decoration bolted on

A lead/hero image and any in-article images should support the specific content of that piece (see [`contrast-and-image-integrity-checks`](../contrast-and-image-integrity-checks/SKILL.md) for verifying they actually depict what the article describes), sized and placed so they don't interrupt reading flow more than necessary, with real captions and alt text per [`on-page-seo`](../on-page-seo/SKILL.md) and [`accessibility-basics`](../accessibility-basics/SKILL.md).

### Support a real reading-continuation habit

A print stylesheet (see [`frontend-polish-microinteractions`](../frontend-polish-microinteractions/SKILL.md)), a working table of contents for long pieces, and a genuinely working search or archive/category browse (see [`data-grid-and-listing-pages`](../data-grid-and-listing-pages/SKILL.md) if the archive is presented as a filterable grid) all support a reader who wants to do more than read one article and leave.

## Never do this

- Never let body copy run the full width of a wide viewport with no measure constraint.
- Never treat every piece of content as equally prominent on the homepage/index by default; curate.
- Never present a weak, coincidental content match as a confident "related" recommendation.
- Never use a display/headline typeface for sustained body reading.

## Verification checklist

- [ ] Body copy measure and line-height follow `typography-craft`'s readability guidance
- [ ] The article template is visually distinct from surrounding site chrome
- [ ] The homepage/index curates rather than defaulting to a flat reverse-chronological list
- [ ] Author, date, and (if applicable) last-updated metadata are consistent across every piece of content
- [ ] Related-content suggestions are genuinely relevant, not coincidentally matched
- [ ] Images support and match the specific content of the piece they appear in
