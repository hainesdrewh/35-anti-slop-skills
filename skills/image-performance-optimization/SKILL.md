---
name: image-performance-optimization
description: 'Use this skill whenever adding images to any web page, and whenever a user asks to "make the site load faster," "optimize images," or "improve page speed." Also apply it by default any time an image is added, since unoptimized images are the single most common cause of slow page loads on otherwise well-built sites, and the fix costs nothing once it''s a default habit rather than an afterthought.'
---

# Image and Performance Optimization

## Why this matters

Images are typically the largest assets on a page by a wide margin, and an uncompressed, oversized, or wrongly-formatted image can single-handedly dominate a page's load time regardless of how efficient the rest of the code is. Slow load times directly hurt both conversion (visitors leave before the page finishes loading) and SEO, since Core Web Vitals (load performance, specifically Largest Contentful Paint) are a real ranking factor.

## Do this

### Compress every image

Run every image through compression before it ships, never upload a camera or design-tool export directly. Aim for the smallest file size that doesn't introduce visible quality loss for that image's actual display size; a hero image displayed at 1600px wide gains nothing from being a 6000px, multi-megabyte original.

### Use modern formats

Serve WebP (or AVIF where broadly supported) instead of JPEG/PNG where possible, which typically cuts file size significantly at equivalent visual quality. Use the `<picture>` element to provide a fallback for any edge case where modern format support matters.

```html
<picture>
  <source srcset="hero.avif" type="image/avif">
  <source srcset="hero.webp" type="image/webp">
  <img src="hero.jpg" alt="Technician repairing a rooftop AC unit">
</picture>
```

### Lazy-load below-the-fold images

Use native lazy loading for any image not visible on initial page load, so the browser doesn't spend bandwidth fetching images the visitor may never scroll to see.

```html
<img src="gallery-photo.jpg" alt="Completed landscaping project" loading="lazy">
```

Never lazy-load the hero/above-the-fold image; that delays the most important visual content on the page and actively hurts Largest Contentful Paint.

### Responsive images with srcset

Serve an appropriately sized image per device rather than shipping the same large desktop image to a phone.

```html
<img
  srcset="photo-400.jpg 400w, photo-800.jpg 800w, photo-1600.jpg 1600w"
  sizes="(max-width: 600px) 400px, (max-width: 1200px) 800px, 1600px"
  src="photo-800.jpg"
  alt="Before and after landscaping transformation"
>
```

### Explicit dimensions

Set `width` and `height` attributes (or the CSS `aspect-ratio` equivalent) on every image so the browser reserves the correct space before the image loads, preventing layout shift that pushes content around as images pop in (a Core Web Vitals metric, Cumulative Layout Shift, penalizes this directly).

## Never do this

- Never upload an unoptimized, camera-resolution image directly to a live page.
- Never lazy-load the hero or other above-the-fold image.
- Never ship the same full-size desktop image to every device regardless of screen size.
- Never omit width/height (or `aspect-ratio`) on images, leaving content to visibly shift as they load in.

## Verification checklist

- [ ] Every image is compressed appropriately for its actual display size
- [ ] Modern formats (WebP/AVIF) are used with a fallback
- [ ] Below-the-fold images use `loading="lazy"`; the hero/above-the-fold image does not
- [ ] Responsive images use `srcset`/`sizes` rather than one fixed size for all devices
- [ ] Every image has explicit dimensions or an `aspect-ratio` to prevent layout shift
