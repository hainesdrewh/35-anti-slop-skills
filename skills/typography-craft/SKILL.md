---
name: typography-craft
description: 'Use this skill whenever setting up typography for a site (font choice, heading scale, line-height, body text width) and whenever a user says text "is hard to read," "looks cramped," or asks to "fix the fonts" or "improve readability." Apply it by default whenever writing the CSS that governs text, not only when explicitly asked about typography, since most readability problems come from decisions (line length, leading, font loading) that nobody consciously made rather than from the font choice itself.'
---

# Typography Craft

## Why this matters

Font choice gets most of the attention, but the details that actually determine whether text is comfortable to read are line length, line height, and a real size scale, none of which show up in a quick glance at a design but all of which are felt immediately by anyone actually reading the page. A site can use a beautiful typeface and still be uncomfortable to read because paragraphs stretch the full width of a wide screen or the heading sizes don't have enough contrast to establish real hierarchy.

## Do this

### Cap line length for readability

Body text should generally sit between 50 and 75 characters per line (roughly 60-75ch as a CSS max-width on the text container). A paragraph stretching the full width of a wide monitor forces the eye to travel too far per line and makes tracking to the next line harder.

```css
.prose { max-width: 65ch; }
```

### Scale line-height with font size, don't use one fixed value everywhere

Larger text generally needs relatively tighter line-height, smaller text needs relatively looser line-height. A single `line-height: 1.5` applied to both a 3rem headline and a 0.875rem caption will make the headline feel loose and disconnected and the caption feel cramped.

```css
h1 { line-height: 1.1; }
h2 { line-height: 1.2; }
body, p { line-height: 1.6; }
small, .caption { line-height: 1.5; }
```

### Build a real type scale

Heading sizes should follow a deliberate ratio (a modular scale, e.g. each level roughly 1.25-1.5x the one below it) rather than arbitrary values, so hierarchy is immediately legible rather than requiring the reader to notice which text is technically bold.

```css
:root {
  --text-sm: 0.875rem;
  --text-base: 1rem;
  --text-lg: 1.25rem;
  --text-xl: 1.75rem;
  --text-2xl: 2.5rem;
  --text-3xl: 3.5rem;
}
```

### Prevent widows and orphans on headlines

A headline that wraps leaving a single short word alone on the last line looks accidental. Use a non-breaking space between the last two words of important headlines, or the CSS `text-wrap: balance` property (supported in modern browsers, with graceful fallback) to let the browser balance line breaks automatically.

```css
h1, h2 { text-wrap: balance; }
```

### Handle font loading deliberately

Choose `font-display: swap` (or preload the font file) so text renders immediately in a fallback font rather than staying invisible while a webfont loads (flash of invisible text), and choose a fallback font with similar metrics to minimize the visible reflow when the real font swaps in.

```css
@font-face {
  font-family: 'Custom Sans';
  src: url('/fonts/custom-sans.woff2') format('woff2');
  font-display: swap;
}
```

### Truncate text intentionally, never mid-word by accident

Where text must be limited to fit a fixed space (a card title, a table cell), use `text-overflow: ellipsis` with `overflow: hidden` and `white-space: nowrap` for single-line truncation, or the `-webkit-line-clamp` property for multi-line truncation, rather than letting a layout silently cut text off with no visual indication that it's been shortened.

```css
.card-title {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
```

## Never do this

- Never let body paragraphs stretch to the full width of a wide viewport with no max-width constraint.
- Never apply one line-height value to every text size on the page regardless of how large or small it is.
- Never size headings by eyeballing pixel values with no underlying scale; a reader should be able to tell heading hierarchy from size alone.
- Never let a webfont load in a way that leaves text invisible (flash of invisible text) for a noticeable period.
- Never let text get cut off mid-word or mid-character with no ellipsis or other visual indication it was truncated.

## Verification checklist

- [ ] Body text line length stays within roughly 50-75 characters per line at typical reading widths
- [ ] Line-height is set relative to font size, tighter for large headings, looser for small body/caption text
- [ ] Heading sizes follow a defined scale, not ad hoc pixel values
- [ ] Important headlines are checked for widows/orphans and corrected
- [ ] Web fonts use `font-display: swap` or are preloaded so text is never invisible while loading
- [ ] Any truncated text uses ellipsis or line-clamp, never a silent hard cutoff
