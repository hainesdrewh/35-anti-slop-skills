---
name: input-validation-and-injection-defense
description: 'Use this skill whenever writing code that accepts input from a user, a form, a URL parameter, an uploaded file, or an external API, and whenever that input is used in a database query, rendered back to a page, stored, or passed to an AI/LLM call. Also use it when a user asks to "add a search feature," "let users submit a form," "build a comment section," or "add an AI chat feature," and whenever reviewing code for injection vulnerabilities. The default failure modes this prevents are SQL injection, cross-site scripting (XSS), and, for AI-backed features, prompt injection, all of which stem from the same root cause: trusting input without validating, sanitizing, or properly escaping it.'
---

# Input Validation and Injection Defense

## Why this matters

Every one of these vulnerability classes shares a root cause: code that treats user-supplied data as if it were trusted, either interpreting it as executable instructions (SQL injection, prompt injection) or rendering it without neutralizing active content (XSS). They are also among the oldest, best-understood vulnerability classes in software, which makes it more embarrassing, not less, when they still ship. The fixes below are standard, low-effort, and should be applied by default, not added reactively after an incident.

## Do this

### Validate server-side, always

Client-side validation (HTML `required`, JavaScript form checks) is a UX convenience, never a security control; a request can bypass the browser entirely. Every input must be validated again on the server before it's used, checking type, length, format, and range, not just presence.

### Use parameterized queries, never string concatenation

```js
// Wrong: user input concatenated directly into the query
db.query(`SELECT * FROM users WHERE email = '${email}'`);

// Right: parameterized, the driver handles escaping
db.query('SELECT * FROM users WHERE email = $1', [email]);
```

This applies to every database driver and ORM; if an ORM ever exposes a raw-query escape hatch, treat it the same way, always parameterized, never interpolated.

### Escape output, not just input

Sanitizing on the way in is not sufficient on its own; escape user-generated content at the point it's rendered, based on the context it's rendered into (HTML body, HTML attribute, URL, JavaScript string each need different escaping). Most modern frameworks (React, Vue) escape by default when rendering text; the danger is specifically in APIs that bypass that default, like React's `dangerouslySetInnerHTML` or Vue's `v-html`. Avoid those entirely for user-generated content, and if genuinely unavoidable, run the content through a dedicated sanitizer library (e.g. DOMPurify) first.

### Sanitize before storing, not just before displaying

Data stored raw and only sanitized at render time means every future render path (a new admin panel, an export feature, an email digest) has to remember to sanitize correctly. Normalize and validate the format at write time as well, so unsafe or malformed data isn't sitting in the database waiting for a code path that forgets to escape it.

### Defend against prompt injection on AI-backed features

Any feature that takes user text and feeds it into an LLM call is exposed to prompt injection: a user crafting input designed to override the system prompt or extract data it shouldn't. Concretely:

- Never concatenate user input directly into a system prompt string that also contains privileged instructions or secrets; keep user content clearly delimited (e.g. in a dedicated message role or explicitly fenced) and treat it as data, not instructions, in the surrounding prompt.
- Never let an LLM call trigger a sensitive action (a database write, a payment, sending an email) directly from unreviewed user input without a separate server-side authorization check on the action itself; the LLM's interpretation of the input is not a substitute for that check.
- Cap what the model's output is allowed to do; if it's producing a response for display, treat that output as untrusted content too and escape it the same way user input would be escaped.

## Never do this

- Never build a SQL query with string interpolation or concatenation of user input, even for "just an internal admin tool."
- Never use `dangerouslySetInnerHTML`, `v-html`, or equivalent on unsanitized user content.
- Never assume input is safe because it passed client-side validation; that check runs in a browser the attacker fully controls.
- Never pass raw, unfiltered user input straight into a system prompt string alongside instructions or secrets the application depends on staying private.

## Verification checklist

- [ ] Every user-facing input is validated server-side (type, length, format), independent of any client-side check
- [ ] No SQL query anywhere concatenates or interpolates user input directly; all use parameterized queries or an ORM's safe query builder
- [ ] No use of `dangerouslySetInnerHTML`/`v-html` (or equivalent) on content that includes user input, without a sanitizer library in between
- [ ] Data is validated/normalized at write time, not sanitized only at render time
- [ ] Any LLM-backed feature keeps user input clearly separated from system instructions in the prompt
- [ ] No LLM output is allowed to directly trigger a sensitive server-side action without an independent authorization check
