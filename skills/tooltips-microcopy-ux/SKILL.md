---
name: tooltips-microcopy-ux
description: 'Use this skill whenever building tooltips, modals, confirmation dialogs, empty states, or helper text anywhere in a UI. Also use it when a user asks to "add a tooltip," "add a confirmation before deleting," or "improve the empty state." Covers making these small UI moments accessible and genuinely helpful, rather than decorative or, for destructive actions, dangerously easy to trigger by accident.'
---

# Tooltips, Modals, and Microcopy

## Why this matters

These are the small moments in a UI, a hover hint, a confirmation before an irreversible action, an empty list state, that either quietly help a user understand what's happening or quietly frustrate them. Getting the destructive-action confirmation wrong specifically (too easy to trigger, or not actually confirming anything) causes genuine, hard-to-recover data loss, which makes this one of the highest-consequence small details in this entire repo.

## Do this

### Rich, accessible tooltips

Build tooltips that are keyboard-accessible (appear on focus, not only on mouse hover) and screen-reader-announced (`aria-describedby` linking the trigger to the tooltip content), not just a native `title=""` attribute, which is inconsistent across browsers, has a slow/no-configurable delay, and is invisible to keyboard and many screen-reader users entirely.

```html
<button aria-describedby="tip-1">Learn more</button>
<div id="tip-1" role="tooltip">This fee only applies to jobs over 50 miles away.</div>
```

Keep tooltip content short and genuinely useful (clarifying an ambiguous term or field), not a repeat of information already visible nearby.

### Modals

- Trap focus within an open modal so Tab doesn't escape to the page behind it, and return focus to the triggering element when the modal closes.
- Close on Escape, on clicking outside, and via a clearly visible close control, all three, not just one.
- Prevent the page behind the modal from scrolling while it's open, but release that lock cleanly on close (a stuck scroll-lock is a common bug).

### Confirmation modals for destructive actions

Any irreversible or hard-to-reverse action (deleting an account, deleting data, canceling a subscription) needs an explicit confirmation step that states specifically what will happen, not a generic "Are you sure?" A confirmation that requires typing the item's name for a truly high-stakes deletion (deleting an entire account or project) raises the bar appropriately above a single accidental click; a lower-stakes action just needs a clear, specific confirm/cancel choice.

```
"Delete 'Q3 Marketing Campaign'? This will permanently remove the project
and all 14 associated tasks. This cannot be undone."
[Cancel]  [Delete Project]
```

Never make the destructive confirm button visually identical in prominence to a safe default; style the destructive action distinctly (often a red/warning treatment) rather than letting Cancel and Confirm look like an equal, arbitrary choice.

### Empty states

Design a real empty state for any list, dashboard, or search result that can legitimately be empty, explaining why it's empty and what to do next ("No projects yet. Create your first one to get started." with a clear action), rather than a bare blank space or a raw "No results" with no path forward.

### Helper text

Place helper/hint text for a form field or setting close to what it explains, worded specifically enough to actually resolve the likely confusion, not a vague restatement of the field's label.

## Never do this

- Never rely on the native `title` attribute as the sole implementation of a tooltip that conveys meaningful information.
- Never let Escape, outside-click, and an explicit close button all be missing from a modal, users need at least one reliable way to close it, and ideally all three.
- Never make a destructive confirmation as easy to trigger as a routine action, or style the destructive option identically to the safe default.
- Never leave a genuinely empty list or dashboard with no explanation or next step.

## Verification checklist

- [ ] Tooltips are keyboard-focusable and screen-reader-announced, not `title=""` only
- [ ] Modals trap focus, restore focus on close, and close via Escape, outside-click, and an explicit control
- [ ] Body scroll lock during a modal releases cleanly on close
- [ ] Destructive actions require an explicit, specific confirmation, visually distinct from the safe/cancel option
- [ ] High-stakes deletions require a stronger confirmation step (e.g. typing the item's name) than routine actions
- [ ] Every legitimately-empty state explains why and offers a next action
