# Five Style Directions

Each one is a coherent system, not just a palette. Adapt specifics to the real business; don't apply verbatim.

## 1. Clean minimal

Fits: professional services, healthcare, fintech, B2B SaaS aimed at a technical or enterprise buyer.

- **Palette**: one neutral (true white or a very light warm/cool gray), one dark neutral for text, one accent color used only for primary actions. No more than 3 colors total in regular use.
- **Type**: a single, highly legible sans-serif (system UI font or something like Inter/Public Sans) for everything, differentiated by weight and size, not by mixing typefaces.
- **Spacing**: generous, consistent, airy. Let content breathe; density is low on purpose.
- **Motion**: minimal and fast (100-150ms), functional only (state changes), no decorative animation.
- **Imagery**: simple, high-quality, often product screenshots or clean photography with a lot of negative space around the subject.
- **Structural signature**: minimal logo-only header, nav revealed on scroll or tucked in a slide-out rather than always inline; centered text-only hero with no photo, or a small supporting screenshot; bordered cards kept minimal (thin 1px border, no shadow, no hover-lift); no floating call button, a scroll-to-top is the only floating chrome if any.

## 2. Editorial luxury

Fits: real estate, hospitality, high-end retail, professional creative services, anything selling on taste and craft.

- **Palette**: a restrained, warm or muted neutral base (cream, warm gray, deep charcoal) with one considered accent, often drawn from the actual brand/product rather than a default.
- **Type**: a serif display face with real character (Fraunces-style or a genuine classic serif) paired with a plain, quiet sans for body and UI text.
- **Spacing**: generous, deliberate, asymmetric where it adds visual interest rather than defaulting to centered symmetry everywhere.
- **Motion**: slow and smooth (300-500ms for larger movements), used sparingly for genuine emphasis (a slow image reveal, a considered hover), never bouncy or playful.
- **Imagery**: full-bleed, high-quality, real photography treated as the primary content, not decoration.
- **Structural signature**: split-screen hero (text on a solid panel beside a full-height image) rather than photo-with-overlay-text; an editorial alternating-row layout for showcasing items instead of a uniform card grid, borderless images with caption text below rather than bordered cards with shadows; no floating call button or scroll-to-top, this direction's restraint is undermined by persistent floating chrome.

## 3. Bold maximalist

Fits: entertainment, events, youth-oriented consumer brands, creative agencies, anything where energy and personality are the actual product.

- **Palette**: saturated, high-contrast, genuinely bold color choices, deliberately chosen and brand-specific, not a random loud palette; still avoid the specific purple/pink gradient slop signature.
- **Type**: a distinctive display face with real personality for headlines, paired with a simple, get-out-of-the-way sans for body text so readability doesn't suffer for boldness's sake.
- **Spacing**: can be tighter and more energetic than minimal or luxury directions, with intentional visual density in places, but still needs a real underlying spacing scale, energetic does not mean inconsistent.
- **Motion**: expressive and characterful (playful easing, real personality in transitions), while still respecting `prefers-reduced-motion` and performance budgets from [`motion-system`](../../motion-system/SKILL.md).
- **Imagery**: can be illustrated, photographic, or mixed, but should feel specific to the brand's actual personality, not generic stock energy.
- **Structural signature**: bold full-width header bar, not a floating pill-shaped sticky header; hero built from an asymmetric or overlapping image collage rather than one full-bleed photo; overlapping/layered card treatment instead of a uniform bordered grid; a floating CTA is appropriate here if the business genuinely benefits from urgency, styled boldly rather than as a quiet pill.

## 4. Dark technical

Fits: developer tools, technical products, security/infrastructure companies, gaming-adjacent products.

- **Palette**: a dark base (not pure black, a deep near-black with slight warmth or coolness) with a single vivid accent color used sparingly for emphasis and interactive elements, plus a light-mode equivalent if the product needs one.
- **Type**: a clean sans for UI text, often paired with a genuine monospace for code/technical content where relevant, not decoratively.
- **Spacing**: precise and structured, reflecting the technical audience; moderate density is expected and appropriate.
- **Motion**: crisp and fast, functional (state changes, data updates), rarely decorative.
- **Imagery**: real product UI, terminal/code screenshots, diagrams, rather than abstract illustration or stock photography.
- **Structural signature**: centered logo with nav split left/right around it, or a top utility bar plus a separate primary nav row; hero built around a real product screenshot or terminal window rather than a lifestyle photo; dense card/table hybrid layouts are appropriate here where they'd feel wrong elsewhere; no floating call button, a compact scroll-to-top or none at all.

## 5. Warm craft

Fits: local service businesses, artisanal/handmade products, food and hospitality at a non-luxury tier, family-owned businesses.

- **Palette**: warm, natural tones (earth tones, warm neutrals) grounded in the actual business's real-world materials or setting, not a generic "friendly" palette applied regardless of business.
- **Type**: a serif or slab-serif with warmth for headlines, paired with a plain, readable sans for body text; avoid overly corporate or overly playful type choices that don't match a genuinely small, real business.
- **Spacing**: comfortable and unpretentious, real information density (this audience wants to see specifics: pricing, real photos, real reviews) rather than airy minimalism that can read as evasive for a business that should feel approachable and concrete.
- **Motion**: restrained and functional, similar to editorial luxury but less slow/dramatic, since the audience is browsing practically, not being sold an aspirational lifestyle.
- **Imagery**: real photography of the actual business, people, and work; this direction has the least tolerance for generic stock photography of any of the five, since the entire appeal is genuineness.
- **Structural signature**: simple inline header with a filled CTA button (the one direction where this default genuinely fits); full-bleed photo hero with overlay text is appropriate here; standard bordered card grid with shadow-on-hover is a reasonable default for this direction specifically; a floating call button is often the single highest-value piece of chrome for this audience and should stay.
