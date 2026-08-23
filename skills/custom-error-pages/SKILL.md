---
name: custom-error-pages
description: 'Use this skill whenever building or reviewing a site''s 404 or 500 error pages, and whenever a user asks to "add a custom 404 page" or "improve the error page." Goes deeper than the baseline check in pre-launch-technical-audit: full treatment of tone, actual recovery paths, and making sure the custom page actually serves in production, not just in local development.'
---

# Custom Error Pages

## Why this matters

A visitor hitting a 404 or 500 has already had something go wrong, a broken link, a typo, an outdated bookmark, and the error page is the only chance to keep them on the site instead of leaving entirely. The framework or hosting platform's bare default error page ("404 - Not Found" on a blank white screen) is a dead end that makes the whole site feel abandoned at the exact page where a visitor most needs reassurance that they haven't left something broken.

## Do this

### 404 pages

- Keep the site's real header/nav intact on the 404 page so the visitor isn't stranded with no way to navigate; a 404 that strips all navigation is worse than one that keeps it.
- State plainly that the page wasn't found, in the site's actual voice, not a generic system message; a small amount of personality here is appropriate as long as it doesn't obscure the actual message or slow down recovery.
- Offer concrete recovery paths: a link back to the homepage, a link to the most likely intended destination if the URL pattern suggests one, and a search box if the site has meaningful content depth.
- If the business is one where a visitor arriving lost is likely trying to reach something specific (a service page, a contact method), surface that directly rather than only a generic "go home" link.

### 500 (server error) pages

- Distinct from a 404: a 500 means something actually broke server-side, not that the visitor made a navigation mistake. Communicate that clearly ("Something went wrong on our end") rather than implying user error.
- Provide a way to reach the business directly (support email or phone) for a persistent error, since a visitor hitting a genuine server error may need help beyond just retrying.
- Log the underlying error server-side with enough detail to actually debug it (see [`transport-headers-and-monitoring`](../transport-headers-and-monitoring/SKILL.md)); the friendly page a visitor sees and the detailed internal log are two separate things, never expose stack traces or internal error details to the visitor-facing page itself.

### Tone calibration

Match the error page's tone to the actual business. A playful "Oops, this page took a wrong turn" fits a casual consumer brand; a professional services or medical site should keep the tone plain and reassuring rather than jokey. Never let tone experimentation slow down or obscure the actual recovery path (the links/search that get the visitor back on track).

### Confirm the custom page actually serves in production

A custom 404/500 built in the codebase doesn't always take effect automatically; some hosting configurations serve the platform's own default error page unless explicitly configured to use the custom one. Verify by navigating to a genuinely nonexistent URL on the live, deployed site, not just in local development, and confirming the custom page (not the platform default) actually appears.

## Never do this

- Never ship the framework or hosting platform's bare default error page to production.
- Never strip all navigation from a 404 page, leaving the visitor with no way forward except the browser's back button.
- Never expose internal error details, stack traces, or debug information on a visitor-facing 500 page.
- Never assume a custom error page works in production just because it renders correctly in local development; verify on the live deployment.

## Verification checklist

- [ ] Navigating to a nonexistent URL on the deployed production site serves the custom 404, not a platform default
- [ ] The 404 page keeps site navigation intact and offers real recovery paths (home link, search, or a likely-intended destination)
- [ ] A custom 500 page exists, communicates a server-side error clearly, and offers a way to reach the business directly
- [ ] No internal error details or stack traces are exposed on the visitor-facing error page
- [ ] Tone matches the actual business and doesn't obscure the recovery path
