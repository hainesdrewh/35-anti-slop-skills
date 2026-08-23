---
name: auth-and-session-security
description: 'Use this skill whenever building login, signup, password reset, or session management for any application. Also use it when a user asks to "add authentication," "add login," "let users sign up," or "reset their password," and whenever reviewing existing auth code for security gaps. The default failure modes this prevents are all common and all exploited in practice: plaintext or weakly-hashed passwords, sessions that survive a password change, reset links that never expire, and login endpoints with no rate limit that let an attacker brute-force credentials at will.'
---

# Auth and Session Security

## Why this matters

Authentication is the single highest-value target on almost any application, since compromising one account often means compromising a real person's data, money, or identity elsewhere (password reuse is extremely common). Auth bugs are also unusually forgiving of neglect until the moment they are not: a login form with no rate limit works fine for months of normal traffic and then gets brute-forced overnight. Every item below is a well-known, well-documented attack pattern with a well-known fix; there is no excuse for shipping the vulnerable version.

## Do this

### Password storage

- Hash passwords with a purpose-built algorithm: `bcrypt`, `argon2`, or `scrypt`. Never plaintext, never a fast general-purpose hash like raw MD5 or SHA-1/SHA-256 with no salt or work factor.
- Use the library's built-in salt handling rather than rolling your own; `bcrypt.hash(password, 12)` (or the framework equivalent) handles salting internally.
- Never log a password, even by accident via a request-body logger that captures the login endpoint's payload.

### Session cookies

Set all three flags on session cookies:

```
Set-Cookie: session=<token>; HttpOnly; Secure; SameSite=Lax
```

- `HttpOnly` prevents client-side JavaScript (and therefore XSS payloads) from reading the cookie.
- `Secure` ensures the cookie is only ever sent over HTTPS.
- `SameSite=Lax` (or `Strict` where the flow allows it) mitigates CSRF by default; use `Strict` unless the app needs cross-site navigation to preserve the session.

### CSRF protection

For any state-changing request (POST/PUT/PATCH/DELETE) that relies on cookie-based session auth, include a CSRF token: generated server-side, embedded in the form or as a header the client must echo back, and validated on submission. Frameworks with built-in CSRF middleware (Django, Rails, Next.js with the right library) should have it enabled, not disabled for convenience.

### Session lifecycle

- Invalidate every existing session for a user the moment their password changes. A stolen session token should stop working the instant the legitimate user notices and changes their password, not continue working indefinitely.
- Expire password-reset links quickly (15 to 60 minutes) and make them single-use; a reset link that still works a week later is a standing vulnerability.
- Regenerate the session identifier on login and on privilege change (e.g. a normal user being promoted to admin), not just on logout, to prevent session fixation.

### Preventing user enumeration

Login and password-reset flows should not reveal whether an email/username exists in the system.

- "Wrong email or password" (identical message for both cases), not "no account found with that email" vs "incorrect password."
- Password reset: always respond with the same "if an account exists, a reset link has been sent" message, regardless of whether the email is actually registered.

### Brute-force defense

- Rate-limit login attempts per account and per IP (see also [`api-abuse-and-rate-limiting`](../api-abuse-and-rate-limiting/SKILL.md) for the general mechanism).
- Lock an account (or require a delay/CAPTCHA) after a threshold of failed attempts, e.g. 5-10 within a short window, and communicate the lockout without revealing whether the account itself exists.
- Rate-limit the password-reset endpoint separately; it is a common target for enumeration and spam since it often sends an email on every request.

## Never do this

- Never store passwords with reversible encryption instead of one-way hashing; there is no legitimate reason an application needs to recover a user's plaintext password.
- Never build a custom auth scheme from scratch (custom token signing, custom session handling) when a maintained library or the framework's built-in auth exists; hand-rolled auth is where subtle, exploitable bugs live.
- Never trust a client-supplied user ID or role claim without verifying it server-side against the actual authenticated session.
- Never skip rate limiting on auth endpoints because "it's just a small app"; automated credential-stuffing bots do not check traffic volume before attacking.

## Verification checklist

- [ ] Passwords hashed with bcrypt/argon2/scrypt, never plaintext or a fast unsalted hash
- [ ] Session cookies set `HttpOnly`, `Secure`, and an appropriate `SameSite` value
- [ ] CSRF tokens present and validated on all state-changing, cookie-authenticated requests
- [ ] All sessions invalidated on password change
- [ ] Password-reset links expire quickly and are single-use
- [ ] Login and reset-request responses do not reveal whether an account exists
- [ ] Login and password-reset endpoints are rate-limited per account and per IP
- [ ] Accounts lock or throttle after repeated failed login attempts
