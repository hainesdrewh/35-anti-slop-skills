---
name: form-ux-feedback
description: 'Use this skill whenever building any form: contact forms, signup/login forms, checkout forms, settings pages, or multi-step wizards. Also use it when a user asks to "add a form," "add validation," "show an error message," or "add a password field," and whenever reviewing existing forms for missing feedback states. It covers the specific, unglamorous UX details (error messages, success confirmation, validation timing, password visibility) that determine whether a form feels trustworthy or feels like it might have silently failed.'
---

# Form UX Feedback

## Why this matters

A form with no clear feedback state leaves the user guessing whether their submission worked, and "guessing" in a form context reads as broken even when the backend succeeded. This is one of the highest-leverage, lowest-effort fixes available: the difference between a generic form and a good one is rarely the layout, it's whether the user always knows exactly what state the form is in.

## Do this

### Error messages

- Be specific about what's wrong and how to fix it: "Enter a valid email address" rather than "Invalid input," and "Password must be at least 8 characters" rather than "Error."
- Show errors inline, next to the field they belong to, not only in a summary banner at the top of the form the user has to scroll back to read.
- Use a real visual signal beyond color alone (an icon, a border change, plus text) since color-only error indication fails for colorblind users and doesn't reproduce reliably across themes.

### Success messages

- Confirm the actual outcome specifically: "Message sent, we'll reply within 1 business day" rather than a bare "Success!"
- For a form that navigates away on success (a checkout, an application), the confirmation belongs on the destination (see [`conversion-ctas`](../conversion-ctas/SKILL.md) for thank-you-page treatment), not just a toast that could be missed.

### Validation timing

- Validate on blur (when the user leaves a field) for most fields, not on every keystroke, which produces error messages while the user is still mid-typing a valid value.
- Re-validate on submit regardless, to catch fields the user never interacted with.
- For fields with a clear "still typing" pattern (password confirmation, email format), it's fine to wait until blur or submit rather than flashing an error the instant the field diverges.

### Required-field indication

Mark required fields clearly and consistently (an asterisk with a legend, or explicit "(required)" text), and prefer marking the minority: if most fields are required, mark the few optional ones "(optional)" instead of asterisking everything.

### Password visibility toggle

Include a show/hide toggle (an eye icon) on password fields rather than forcing masked-only input. This meaningfully reduces failed-login and failed-signup rates caused by typos in a field the user can't verify.

```html
<div class="password-field">
  <input type="password" id="password" />
  <button type="button" aria-label="Show password" onclick="toggleVisibility()">👁</button>
</div>
```

Make sure the toggle button has an accessible label that updates with state (`aria-label="Show password"` / `"Hide password"`), and never store or log the revealed value differently than the masked one; the toggle only changes the `type` attribute between `password` and `text`.

### Loading and disabled states

While a submission is in flight, disable the submit button and show a clear in-progress indicator (spinner plus label, e.g. "Sending...") so a slow network doesn't invite a frustrated double-click, which can cause a duplicate submission if the backend isn't idempotent.

## Never do this

- Never show a generic "Something went wrong" with no indication of what or where.
- Never validate aggressively on every keystroke, especially on the first character typed into a field.
- Never leave a submitted form with no visible acknowledgment (no toast, no redirect, no message) that leaves the user unsure whether it worked.
- Never mask a password field with no way for the user to verify what they typed.

## Verification checklist

- [ ] Every validation error is specific and appears next to its field, not only in a top-of-form summary
- [ ] Errors are indicated by more than color alone
- [ ] Success is confirmed with a specific message describing the actual outcome
- [ ] Validation fires on blur/submit, not on every keystroke
- [ ] Required fields are marked clearly and consistently
- [ ] Password fields include a working, accessible show/hide toggle
- [ ] The submit button shows a loading state and is disabled during submission
