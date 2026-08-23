---
name: file-upload-and-payment-integrity
description: 'Use this skill whenever building a file upload feature (images, documents, avatars, attachments) or any checkout/payment flow, including one built on Stripe, PayPal, or a similar processor. Also use it when a user asks to "let users upload a photo," "add checkout," "add a shopping cart," or "accept payments," and whenever reviewing an upload or payment code path for security. The default failure modes this prevents: an uploaded file executing as code on the server, and a client being able to manipulate a price or falsely trigger a "payment succeeded" state.'
---

# File Upload and Payment Integrity

## Why this matters

File uploads and payments are two of the few places where user input directly interacts with the server's filesystem or with real money, which makes both categories disproportionately damaging when handled carelessly. An upload endpoint that trusts a file's declared type can be turned into a way to plant executable code on the server. A checkout flow that trusts a client-submitted price can be manipulated to charge whatever the attacker chooses, including zero.

## Do this

### Whitelist upload types properly

Check the actual file content, not just the filename extension or the client-declared MIME type, both of which are trivially spoofed by renaming a file or editing a form field.

- Verify the file's magic bytes/signature server-side match an allowed type (an image library reading and re-encoding the file as part of processing it naturally does this; use that as the validation step rather than trusting the upload metadata).
- Restrict to the specific types actually needed (e.g. `image/jpeg`, `image/png`, `image/webp` for an avatar upload), never a broad "any file" allowance unless the product genuinely requires it.
- Enforce a file size limit server-side, not just in the frontend uploader's UI.

### Store and serve uploads safely

- Store uploaded files outside the web server's executable path, or in dedicated object storage (S3 or equivalent), rather than a directory the server would execute scripts from.
- Serve uploaded files with a `Content-Disposition` and `Content-Type` that matches the verified actual type, and disable execution permissions on the storage location so an uploaded file can never run as a script even if its extension is misleading.
- Rename uploaded files to a generated identifier rather than preserving the user-supplied filename directly, which avoids path traversal (`../../etc`) and filename-based injection issues.

### Never trust a client-submitted price

The price, total, tax, and discount for any transaction must be computed and enforced server-side, looked up from the actual product/pricing data, never read from a value the client included in the checkout request.

```js
// Wrong: trusts whatever total the client sends
const { productId, amount } = req.body;
await charge(amount);

// Right: server looks up the real price, ignores any client-sent amount
const { productId } = req.body;
const product = await getProduct(productId);
await charge(product.priceInCents);
```

This applies to discount codes and coupons too; validate the code server-side against real rules (expiry, usage limits, eligibility) rather than trusting a client-calculated discounted total.

### Verify payment webhook signatures

When a payment provider notifies the backend that a charge succeeded (via webhook), verify the webhook's cryptographic signature using the provider's SDK before trusting the event, rather than trusting any POST that arrives at the webhook URL claiming success. An unverified webhook endpoint can be called directly by anyone who finds the URL, faking a "payment succeeded" event with no actual payment.

```js
// Stripe example: verify before trusting the event
const event = stripe.webhooks.constructEvent(rawBody, signatureHeader, webhookSecret);
// only now is `event` trustworthy
```

Treat the webhook as the source of truth for order fulfillment, not a client-side "payment complete" redirect, which can be reached without an actual successful payment (e.g. by navigating to the success URL directly).

## Never do this

- Never trust a file's extension or declared MIME type as the sole gate for what's allowed to upload.
- Never serve uploaded user content from a path where the server would execute scripts.
- Never compute a final charge amount from anything the client sent in the request body.
- Never mark an order as paid or fulfilled based solely on a client-side redirect to a "success" page; confirm via the verified server-to-server webhook.

## Verification checklist

- [ ] Upload type validation checks actual file content (magic bytes), not just extension or declared MIME type
- [ ] Upload size is capped server-side
- [ ] Uploaded files are stored outside the executable web root or in dedicated object storage, with execution disabled
- [ ] Uploaded filenames are not used directly as storage paths (no path traversal risk)
- [ ] Price, tax, and discount for every transaction are computed server-side from real data, never from a client-submitted amount
- [ ] Discount/coupon codes are validated server-side against real eligibility and usage rules
- [ ] Payment webhook signatures are verified before any event is trusted
- [ ] Order fulfillment is triggered by the verified webhook, not by a client-side success redirect alone
