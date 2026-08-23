---
name: database-access-control
description: 'Use this skill whenever designing database schema, writing queries or API endpoints that read or write user data, or setting up a database service like Supabase, Firebase, or Postgres. Also use it when a user asks to "let users see their own data," "add a database," "connect to Supabase," or "build an API endpoint," and whenever reviewing code that touches a database for access-control gaps. The default failure mode this prevents is broken object-level access control: any authenticated user able to read or modify any other user''s data by simply changing an ID in a request, which is consistently one of the most common real-world vulnerabilities in deployed applications.'
---

# Database Access Control

## Why this matters

The most common serious vulnerability in real applications is not a clever exploit; it is a missing ownership check. An endpoint that fetches `/api/orders/:id` without verifying the requesting user actually owns order `:id` lets any logged-in user read or edit anyone else's data just by changing the number in the URL. This is boring, easy to miss, and devastating when found, since it usually exposes every record in the system rather than just one.

## Do this

### Enforce ownership server-side, on every request

Never trust a client-supplied ID to determine what a request is allowed to touch. Every read or write to a specific record needs an explicit check that the record belongs to (or is otherwise accessible by) the authenticated user making the request, done in the query itself, not just in application logic that's easy to forget to add to the next endpoint.

```sql
-- Wrong: trusts the client-supplied id with no ownership check
SELECT * FROM orders WHERE id = $1;

-- Right: scoped to the authenticated user
SELECT * FROM orders WHERE id = $1 AND user_id = $2;
```

### Use row-level security where the database supports it

Postgres (and services built on it, like Supabase) supports row-level security (RLS): policies enforced at the database layer that apply no matter which application code path reaches the table, closing the gap where one endpoint remembers the ownership check and another one doesn't.

```sql
alter table orders enable row level security;

create policy "users can only access their own orders"
on orders for all
using (auth.uid() = user_id);
```

Treat RLS as a backstop, not a replacement for reviewing application-level query logic; a wide-open RLS policy left as `using (true)` during development is a common way this protection gets accidentally disabled in production.

### Restrict database roles to least privilege

The database credential a normal application server uses should not be a superuser/service-role key. Create a role scoped to only the tables and operations the application actually needs, and reserve admin/service-role credentials for trusted server-side administrative tasks, never exposed to any client-facing code path (see [`secrets-and-env-hardening`](../secrets-and-env-hardening/SKILL.md)).

### Block mass assignment and field tampering

When accepting a JSON body to create or update a record, explicitly allow-list which fields the client is permitted to set, rather than passing the entire request body into the update. Otherwise a client can set fields never intended to be user-editable.

```js
// Wrong: attacker can include role: "admin" in the request body
await db.users.update(userId, req.body);

// Right: only the intended fields can ever be set from the client
const { name, email } = req.body;
await db.users.update(userId, { name, email });
```

### Encrypt sensitive fields at rest

For genuinely sensitive fields (SSNs, payment details beyond what a PCI-compliant processor already tokenizes, health data), encrypt at the application or database-column level in addition to relying on disk-level encryption, so a raw database dump or backup leak doesn't expose the field in plaintext. Do not build custom encryption; use the database's or a well-established library's built-in column encryption.

## Never do this

- Never rely solely on hiding an ID (making it a UUID instead of a sequential integer) as the access control mechanism; obscurity is not a substitute for an actual ownership check, since a UUID a user already has can still be replayed.
- Never expose a service-role or admin database key to any code that runs in the browser or a mobile client.
- Never let an update endpoint accept and apply an entire request body without an explicit allow-list of editable fields.
- Never leave a row-level-security policy set to allow-all as a "temporary" development convenience; it is easy to forget to tighten before launch.

## Verification checklist

- [ ] Every read/write endpoint that touches a specific record verifies ownership server-side, in the query, not just in a conditional that's easy to miss on a new endpoint
- [ ] Row-level security is enabled and scoped correctly on every table containing user data, if the database supports it
- [ ] The application's database credential is scoped to least privilege, not a superuser or service-role key
- [ ] Service-role/admin database credentials never appear in client-side or mobile code
- [ ] Every update endpoint uses an explicit allow-list of client-editable fields, not the raw request body
- [ ] Genuinely sensitive fields are encrypted at rest, not just relying on disk-level encryption
