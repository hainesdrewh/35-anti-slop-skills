# Pre-Launch Technical Audit: Copy-Paste Checklist

Run this against the live staging URL, not just localhost; some of these (favicon delivery, custom 404 routing, hosting-level redirects) only show up once actually deployed.

## Horizontal scroll / mobile overflow

- [ ] Loaded at 320px width (iPhone SE) with no horizontal scrollbar
- [ ] Loaded at 375px and 414px widths (common phone sizes) with no overflow
- [ ] Ran the red-outline overflow script from SKILL.md in the console, zero elements flagged
- [ ] All images/video/iframes have `max-width: 100%`
- [ ] No `100vw` used inside a padded container
- [ ] Tables scroll within their own container on narrow screens, not the whole page
- [ ] Long URLs/emails/strings wrap instead of forcing width

## Links and buttons

- [ ] Full-site link crawl run (linkinator, lychee, or equivalent), zero unexpected 404s
- [ ] Every internal anchor link (`#section`) resolves to an existing element
- [ ] Every `tel:` link has a correctly formatted, real number
- [ ] Every `mailto:` link has a real, monitored address
- [ ] No button has a missing `href`/handler
- [ ] No button is permanently or unexpectedly disabled
- [ ] No decorative element overlaps and intercepts a real click target

## Content hygiene

- [ ] Repo-wide search for `lorem ipsum`, `your company`, `example.com`, `555-555`, `123-456-7890`, `todo:`, `fixme`, `john doe` returns nothing
- [ ] No `alt=""` or `alt="image"` on meaningful (non-decorative) images
- [ ] Every nav item links to a finished, real page
- [ ] No duplicate nav items pointing to the same destination

## Titles and metadata

- [ ] No page has a framework-default title (`React App`, `Document`, `Vite + React`, etc.)
- [ ] Every page's title is unique across the site

## Favicon

- [ ] `favicon.ico` present and not the framework default
- [ ] Modern SVG/PNG favicon linked in `<head>`
- [ ] `apple-touch-icon.png` (180x180) present and linked
- [ ] Favicon actually renders in a browser tab on the deployed site, not just in local dev

## Error pages

- [ ] Navigating to a nonexistent path on the deployed site serves a custom, branded 404
- [ ] The 404 page includes real navigation back into the site (see `custom-error-pages`)

## Footer

- [ ] No `#` placeholder hrefs on social icons or footer links
- [ ] Legal links (privacy policy, terms) present and resolve, if applicable
- [ ] No unauthorized leftover "Powered by" / "Made by" credit line
- [ ] Copyright year renders as the current year via dynamic generation, not a hardcoded string
