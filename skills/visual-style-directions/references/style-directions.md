# Six Style Directions

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

## 6. Cinematic bold

Fits: premium real estate, architecture and design firms, luxury travel/hospitality, automotive, anything where the product itself is visually spectacular and the site's job is to feel as impressive as the product. The highest-visual-ambition direction on this list; it takes real production effort (photography quality, headline copy that reads well oversized) to pull off, and looks worse than a plain site if attempted half-heartedly.

- **Palette**: a dark, moody base (deep navy or near-black) over which real photography and bright white or gradient-fill typography sit; a single vivid accent (often a saturated green, purple, or amber) used only for the primary CTA pill and small UI accents, never as a large fill.
- **Type**: one very heavy, condensed or extra-bold sans for the oversized hero headline (headline text is a graphic element here, not just large body type), paired with a plain, small-scale sans for everything else, nav, captions, body copy, so the scale contrast does the work.
- **Spacing**: the hero is dense with layered elements (nav, headline, caption, floating cards, a ticker) rather than a single centered message; everywhere else on the page reverts to conventional, comfortable spacing so the density is a hero-specific effect, not the whole site's personality.
- **Motion**: the marquee ticker runs continuously and subtly; other motion (card hovers, page transitions) stays crisp and understated so it doesn't compete with the hero's visual density.
- **Imagery**: full-bleed, genuinely striking, high-production photography of the actual property/product from a flattering wide angle; this direction has zero tolerance for a mediocre or dark/flat photo, since the whole hero is built around it carrying real visual weight. Never substitute a more dramatic but unrelated photo (a different, more striking property) for the real thing being sold, see `contrast-and-image-integrity-checks` and `image-sourcing-and-generation`; a real, well-shot, honest photo of the actual property in a wide establishing angle is the requirement, not a swap.
- **Structural signature**: a floating pill-shaped nav bar sitting directly on the hero image with no boxed header behind it (a small logo mark floats top-left, a filled accent-color CTA pill floats top-right, nav links sit in a white or blurred pill in the center); an oversized headline (10-15vw) laid directly over the hero photo, using a gradient or blend-mode fill so it reads as part of the image rather than a text box on top of it; a short caption line sitting directly on the image near a bottom corner, not in a separate content panel; a floating overlay card (a featured listing thumbnail plus price) anchored to a hero corner; a continuously scrolling marquee ticker along the hero's bottom edge showing prices or quick stats.

### Cinematic bold: concrete implementation

**Oversized headline blended into the photo**, not a plain white heading in a text box:

```css
.hero-mega-headline {
  position: absolute; top: 8%; left: 0; right: 0; text-align: center;
  font-size: clamp(4rem, 14vw, 11rem); font-weight: 800; line-height: 0.9;
  letter-spacing: -0.02em; margin: 0; z-index: 1; pointer-events: none;
  background: linear-gradient(180deg, rgba(255,255,255,0.95) 0%, rgba(255,255,255,0.15) 100%);
  -webkit-background-clip: text; background-clip: text; color: transparent;
}
.hero-media img { position: relative; z-index: 2; } /* photo's main subject sits above the faded headline tail */
```

The gradient fade (opaque at top, transparent by the bottom of the text) combined with the photo's real subject rendered at a higher stacking position is what produces the "text behind the building" collage effect without needing a manually cut-out image.

**Floating pill nav with no boxed header**:

```css
.hero-nav {
  position: absolute; top: var(--space-6); left: var(--space-6); right: var(--space-6);
  z-index: 3; display: flex; align-items: center; justify-content: space-between;
}
.hero-nav-links {
  display: flex; gap: var(--space-2); background: rgba(255,255,255,0.12);
  backdrop-filter: blur(12px); border-radius: 999px; padding: var(--space-1);
}
.hero-nav-links a { padding: var(--space-2) var(--space-5); border-radius: 999px; color: #fff; text-decoration: none; font-size: 0.92rem; }
.hero-nav-links a[aria-current="page"] { background: #fff; color: #111; }
.hero-cta-pill { background: var(--accent); color: #111; padding: var(--space-2) var(--space-5); border-radius: 999px; font-weight: 600; text-decoration: none; }
```

**Marquee ticker** (pause on hover, and stop entirely under reduced motion per `advanced-motion-and-3d`):

```css
.ticker { overflow: hidden; white-space: nowrap; background: rgba(0,0,0,0.35); position: absolute; left: 0; right: 0; bottom: 0; z-index: 3; padding: var(--space-2) 0; }
.ticker-track { display: inline-block; animation: ticker-scroll 28s linear infinite; }
.ticker:hover .ticker-track { animation-play-state: paused; }
@keyframes ticker-scroll { from { transform: translateX(0); } to { transform: translateX(-50%); } }
@media (prefers-reduced-motion: reduce) { .ticker-track { animation: none; } }
```

Duplicate the ticker's content once in the markup (render the same list of items twice back to back) so the `-50%` loop point lines up seamlessly.

**Floating overlay card**, anchored to a hero corner, real content only:

```css
.hero-float-card {
  position: absolute; right: var(--space-6); bottom: calc(var(--space-6) + 40px); z-index: 3;
  background: #fff; border-radius: var(--radius-md); padding: var(--space-3); display: flex; gap: var(--space-3);
  align-items: center; box-shadow: var(--shadow-2); max-width: 280px;
}
```
