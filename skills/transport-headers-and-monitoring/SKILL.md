---
name: transport-headers-and-monitoring
description: 'Use this skill whenever configuring a web server, deployment, or hosting setup for any production application, and before any site or API goes live. Also use it when a user asks to "deploy this," "set up hosting," "configure the server," or "harden this before launch," and whenever reviewing production configuration for security gaps. It covers the infrastructure-level defenses that sit outside application code: forcing HTTPS, locking down CORS, setting security headers, disabling directory listing, removing default admin routes, scanning dependencies, and logging security-relevant events so an incident is actually detectable.'
---

# Transport, Headers, and Monitoring

## Why this matters

Application-level code can be entirely correct and still ship an insecure deployment if the surrounding infrastructure is left at defaults. These are the checks that live outside any specific feature, in the server config, hosting platform, and CI pipeline, and they're easy to skip precisely because no single one is tied to a specific user-facing feature request.

## Do this

### Force HTTPS and enable HSTS

Redirect all HTTP traffic to HTTPS at the server or load-balancer level, and set the HSTS header so browsers refuse to downgrade to HTTP even if a user types the bare domain or clicks an old HTTP link.

```
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
```

Most modern hosting platforms (Vercel, Netlify, Cloudflare) handle the HTTPS redirect automatically; confirm it's actually active rather than assuming it, and add HSTS explicitly since it's not always on by default.

### Lock down CORS

Set `Access-Control-Allow-Origin` to an explicit list of trusted origins, never `*` combined with `Access-Control-Allow-Credentials: true` (browsers block that combination for good reason, and permissive CORS otherwise still needlessly widens the attack surface for any API that isn't meant to be called from arbitrary sites).

```js
// Wrong
app.use(cors({ origin: '*', credentials: true }));

// Right
app.use(cors({ origin: ['https://example.com', 'https://app.example.com'], credentials: true }));
```

### Set standard security headers

```
Content-Security-Policy: default-src 'self'; script-src 'self'; object-src 'none'
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: geolocation=(), camera=(), microphone=()
```

Tune the Content-Security-Policy to the actual resources the site loads (fonts, analytics, payment iframes) rather than leaving it default-open; a CSP that allows `unsafe-inline` and `unsafe-eval` broadly defeats its own purpose as an XSS mitigation.

### Disable directory listing and remove default admin routes

- Confirm the web server does not serve a directory index for folders without an explicit index file; an exposed directory listing can reveal backup files, config files, or other content never meant to be browsable.
- Change or remove any framework or CMS's default admin path (`/admin`, `/wp-admin` on non-WordPress stacks that inherited it, a framework's default debug/admin panel) if it's exposed in production and not needed, or at minimum put real authentication in front of it; default paths are the first thing automated scanners check.

### Scan dependencies

Run dependency vulnerability scanning as part of the build or CI pipeline (`npm audit`, `pip-audit`, GitHub's Dependabot alerts, or equivalent), not as a manual occasional check. Treat a high-severity finding in a production dependency as a blocker, not a backlog item to revisit eventually.

### Log security-relevant events

Log failed login attempts, permission-denied responses, and rate-limit triggers with enough detail (timestamp, user/IP, endpoint) to reconstruct what happened during an incident. A breach that leaves no trace in logs is far harder to detect, scope, and respond to; logging after the fact does not help.

## Never do this

- Never leave a site reachable over plain HTTP in production, even "temporarily."
- Never set `Access-Control-Allow-Origin: *` on an API that also sends credentials or handles authenticated requests.
- Never leave a default admin or debug route exposed and unauthenticated in production because it "isn't linked from anywhere"; obscurity is not access control.
- Never treat a dependency vulnerability scan as optional or something to run only right before a big release; new vulnerabilities are disclosed continuously against dependencies already in use.

## Verification checklist

- [ ] All HTTP traffic redirects to HTTPS; HSTS header is set
- [ ] CORS origin list is explicit, never `*` combined with credentials
- [ ] CSP, `X-Content-Type-Options`, `X-Frame-Options`, `Referrer-Policy`, and `Permissions-Policy` headers are set and actually tuned to the site's real resource needs
- [ ] No directory listing is served for any folder without an explicit index
- [ ] Default admin/debug routes are removed, renamed, or properly authenticated in production
- [ ] Dependency vulnerability scanning runs automatically in CI, not manually and occasionally
- [ ] Failed logins, permission denials, and rate-limit triggers are logged with enough detail to investigate later
