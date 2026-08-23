---
name: secrets-and-env-hardening
description: 'Use this skill whenever writing code that reads an API key, database credential, webhook secret, or any third-party service token, and whenever setting up a new project''s environment configuration. Also use it when a user asks to "add Stripe," "connect to a database," "call the OpenAI API," or any integration requiring a secret, and whenever reviewing code for security before it is committed or deployed. The default failure mode this prevents is a leaked API key: hardcoded in source, committed in a .env file, or exposed in client-side JavaScript where anyone can view it in the browser and rack up charges or access data on the owner''s account.'
---

# Secrets and Env Hardening

## Why this matters

A leaked API key is not a theoretical risk. Committed secrets get found by automated scrapers within minutes of a public push, and a key exposed in client-side JavaScript is visible to literally anyone who opens dev tools, no scraping required. The consequences range from a surprise bill (an OpenAI or AWS key used to run someone else's workload) to a full data breach (a database service-role key that bypasses all access controls). This is the first thing to get right because every other security skill in this repo assumes secrets are actually secret.

## Do this

### Keep secrets out of source control

- Every project needs a `.env` file for secrets, and that file must be listed in `.gitignore` before it ever contains a real value, not after.
- Commit a `.env.example` with the variable names and dummy/placeholder values so the shape of required config is documented without exposing anything real.
- Load secrets via environment variables (`process.env.X`, `os.environ["X"]`, or the framework's equivalent), never as literal strings pasted into source files.

```
# .gitignore
.env
.env.local
.env.*.local
```

```
# .env.example (safe to commit)
DATABASE_URL=postgres://user:password@localhost:5432/dbname
STRIPE_SECRET_KEY=sk_test_placeholder
OPENAI_API_KEY=sk-placeholder
```

### Know which keys are safe on the client and which are not

Some keys are explicitly designed to be public (a Stripe *publishable* key, a Google Maps key restricted by domain/referrer). Most are not. Before putting any key in frontend code, confirm the provider explicitly documents it as a public/publishable key. If in doubt, treat it as private and proxy the call through a backend.

- Private keys (database credentials, secret API keys, service-role/admin keys) must only ever be read on the server, never bundled into frontend JavaScript, never referenced in a client component that ships to the browser.
- In frameworks that distinguish build-time env exposure (e.g. Next.js's `NEXT_PUBLIC_` prefix, Vite's `VITE_` prefix), anything without that prefix stays server-only, and anything with it should be treated as public information. Never prefix a genuinely private key just to make a build error go away.

### Purge secrets that already leaked into git history

A key removed from the current file is still readable in git history until the history itself is rewritten. If a real secret was ever committed:

1. Rotate the key immediately at the provider. This is the only step that actually neutralizes the leak; rewriting history alone does not un-expose a key that's already been scraped.
2. Then remove it from history with `git filter-repo` (preferred over the older `filter-branch`) or BFG Repo-Cleaner if the exposure needs to be scrubbed from a shared repo.
3. Force-push the rewritten history only after coordinating with anyone else working on the repo, since it invalidates their existing clones.

### Rotate on any suspected exposure

Treat any of these as a rotation trigger: a key pasted into a chat/ticket/screenshot, a repo that was briefly public before being made private, a dependency or CI log that may have printed an env var, or an employee/contractor offboarding.

## Never do this

- Never hardcode a real API key, password, or connection string directly in source, "just for now," with a plan to move it to `.env` later. Later doesn't reliably happen before a commit does.
- Never log full request/response objects that might contain an `Authorization` header or API key in plaintext.
- Never assume a private repo makes hardcoded secrets acceptable; repos change visibility, get forked, or get accessed by more collaborators than originally intended.
- Never put a genuinely private key behind only client-side obfuscation (base64 encoding, splitting the string) as a substitute for keeping it server-side. Obfuscation is not encryption and is trivially reversed.

## Verification checklist

- [ ] `.env` (and any `.env.local`/`.env.*.local` variants) is listed in `.gitignore` before it holds real values
- [ ] `.env.example` exists with placeholder values, documenting required config without exposing real secrets
- [ ] `git log -p -- .env` (or a full-history secret scanner like `gitleaks` or `trufflehog`) shows no real secrets ever committed
- [ ] No API key, database URL, or credential appears as a literal string anywhere in the codebase
- [ ] Every value exposed to client-side code has been explicitly confirmed as provider-documented-public, not assumed safe
- [ ] Any key that was ever exposed (chat, log, public repo window) has been rotated, not just removed from the current code
