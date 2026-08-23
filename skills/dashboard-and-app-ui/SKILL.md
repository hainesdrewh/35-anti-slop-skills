---
name: dashboard-and-app-ui
description: 'Use this skill whenever building an internal application UI, an admin panel, or a logged-in product dashboard: data tables, sidebars, settings screens, analytics views. Also use it when a user asks to "build a dashboard," "add an admin panel," or "build the app UI" as distinct from the public marketing site. Dashboard UI optimizes for a returning user doing repeated tasks efficiently, which is a different design problem than a marketing page optimizing for a first-time visitor''s impression, and treating them the same produces a dashboard that looks nice once and is annoying to actually use daily.'
---

# Dashboard and App UI

## Why this matters

A marketing page is judged on a first impression measured in seconds; a dashboard is judged on how it feels the five-hundredth time someone uses it to do their job. Decorative animation, generous marketing-page whitespace, and playful copy that read as charming on a landing page read as friction and noise to someone trying to get through a repeated task efficiently. The design priorities genuinely invert: density and predictability matter more than delight, though delight in small, non-obstructive doses still has a place.

## Do this

### Prioritize information density appropriate to daily use

A returning user benefits from seeing more at once (a denser table, more visible fields) rather than the generous whitespace appropriate to a marketing page. Use [`layout-spacing-and-alignment`](../layout-spacing-and-alignment/SKILL.md)'s spacing scale, but choose the tighter end of it deliberately for data-dense views, reserving generous spacing for genuinely low-density screens (a settings page with few fields).

### Design data tables for real use, not just display

- Sortable columns with a visible indicator of current sort direction.
- Sensible default column widths that don't force horizontal scroll for common data, and a real strategy (horizontal scroll with a frozen first column, or a responsive card view) for narrow screens rather than an unusably squeezed table.
- Row-level actions (edit, delete, view) that are consistently placed and don't require hunting on each row.
- Pagination or virtualized scrolling for large datasets, never rendering thousands of rows at once with no strategy.
- Empty and loading states specific to the table (see [`data-grid-and-listing-pages`](../data-grid-and-listing-pages/SKILL.md) for the underlying empty/loading-state principles, which apply here too).

### Keep navigation predictable and persistent

A sidebar or persistent nav structure that stays in the same place and the same order across the whole app lets a returning user build muscle memory; don't let navigation reflow or reorder itself between sessions or pages without a specific reason. Show the user clearly where they are (breadcrumbs or a highlighted active nav item, see [`breadcrumbs-internal-linking`](../breadcrumbs-internal-linking/SKILL.md)) since app UIs are often deeper than marketing sites.

### Handle forms and settings screens for efficient repeated use

Save state clearly (an explicit save confirmation per [`form-ux-feedback`](../form-ux-feedback/SKILL.md), or genuine, clearly-indicated autosave, never silent autosave with no confirmation at all) and group related settings so a user doesn't have to search the whole screen for one option they remember existing somewhere.

### Use motion sparingly and functionally

Favor motion that clarifies state change (a row sliding out on delete, a subtle loading transition) over motion that's purely decorative; see [`motion-system`](../motion-system/SKILL.md) for the underlying timing/easing discipline, applied here toward function over delight. A returning daily user will find decorative animation that adds even 200ms to every repeated action actively annoying within a week.

### Design permission and role states honestly

If a user can't perform an action due to permissions, show that clearly (a disabled state with an explanation, not a hidden control that just doesn't work) rather than presenting a control that silently fails; see [`component-detail-polish`](../component-detail-polish/SKILL.md) for the disabled-state standard this extends. Never rely on hiding a control alone as an access-control mechanism; see [`database-access-control`](../database-access-control/SKILL.md) for the actual server-side enforcement this UI-level treatment must be backed by.

## Never do this

- Never apply marketing-page-scale whitespace and decorative animation to a screen meant for efficient repeated daily use.
- Never render an unbounded, unpaginated table of rows with no strategy for large datasets.
- Never let primary navigation reorder or reflow unpredictably between visits.
- Never silently autosave with zero indication that it happened.
- Never hide a permission-restricted action with no explanation, or rely on hiding it as the actual access control.

## Verification checklist

- [ ] Information density is appropriate to daily repeated use, not defaulted from marketing-page spacing conventions
- [ ] Tables are sortable, handle large datasets without rendering everything at once, and have real empty/loading states
- [ ] Primary navigation is persistent and predictable, with a clear indication of current location
- [ ] Save actions give clear feedback; autosave, if used, is visibly indicated
- [ ] Permission-restricted actions are shown with a clear disabled state and explanation, backed by real server-side enforcement
- [ ] Motion serves state clarity over decoration, and never meaningfully slows down a repeated action
