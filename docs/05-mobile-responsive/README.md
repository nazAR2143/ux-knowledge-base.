# 05 — Mobile & Responsive Design

> **Mobile-first is not just a CSS strategy — it's a mindset. 60%+ of web traffic is mobile. Design for constraints first, then enhance for larger screens.**

---

## Table of Contents
1. [Mobile-First Philosophy](#1-mobile-first-philosophy)
2. [Responsive Breakpoints & Media Queries](#2-responsive-breakpoints--media-queries)
3. [Touch Targets & Gestures](#3-touch-targets--gestures)
4. [Mobile Typography](#4-mobile-typography)
5. [Mobile Navigation Patterns](#5-mobile-navigation-patterns)
6. [Images & Media on Mobile](#6-images--media-on-mobile)
7. [Performance on Mobile](#7-performance-on-mobile)
8. [Progressive Web Apps (PWA)](#8-progressive-web-apps-pwa)
9. [Checklist](#checklist)
10. [Sources & Further Reading](#sources--further-reading)

---

## 1. Mobile-First Philosophy

**Source:** [Luke Wroblewski: Mobile First](https://www.lukew.com/ff/entry.asp?933) | [Google Mobile-First Indexing](https://developers.google.com/search/docs/crawling-indexing/mobile/mobile-sites-mobile-first-indexing)

### Why Mobile-First?
1. **Traffic:** 60–65% of global web traffic is mobile (Statcounter 2024)
2. **SEO:** Google uses mobile version for indexing and ranking
3. **Constraints breed creativity:** Designing for small screens forces prioritization
4. **Progressive enhancement:** Add complexity for larger screens; start simple

### Mobile-First CSS Strategy
```css
/* ✅ Mobile-first: Base styles apply to all screens */
.card {
  display: flex;
  flex-direction: column;  /* Stacked on mobile */
  padding: var(--space-4);
  gap: var(--space-3);
}

/* Enhance for tablet */
@media (min-width: 768px) {
  .card {
    flex-direction: row;  /* Side-by-side on larger screens */
    padding: var(--space-6);
  }
}

/* Enhance for desktop */
@media (min-width: 1024px) {
  .card { padding: var(--space-8); }
}

/* ❌ Desktop-first (requires overriding) */
.card {
  flex-direction: row;    /* Start desktop */
}
@media (max-width: 768px) {
  .card { flex-direction: column; }  /* Override — more brittle */
}
```

---

## 2. Responsive Breakpoints & Media Queries

**Source:** [CSS Media Queries Level 4](https://www.w3.org/TR/mediaqueries-4/) | [Tailwind CSS Breakpoints](https://tailwindcss.com/docs/responsive-design)

### Standard Breakpoints

```css
:root {
  --bp-sm: 640px;    /* Large mobile / small tablet */
  --bp-md: 768px;    /* Tablet */
  --bp-lg: 1024px;   /* Laptop */
  --bp-xl: 1280px;   /* Desktop */
  --bp-2xl: 1536px;  /* Large desktop */
}

/* Use ranges to avoid conflicts */
@media (min-width: 768px) and (max-width: 1023px) {
  /* Tablet-only styles */
}
```

### Modern CSS — Container Queries
```css
/* ✅ Container queries: component-based responsive (2023+) */
.card-container {
  container-type: inline-size;
  container-name: card;
}

@container card (min-width: 400px) {
  .card-content {
    display: grid;
    grid-template-columns: 1fr 2fr;
  }
}
```

### Fluid Typography
```css
/* Fluid font size: scales between mobile and desktop */
/* clamp(minimum, preferred, maximum) */
h1 { font-size: clamp(1.75rem, 4vw + 1rem, 3.052rem); }
h2 { font-size: clamp(1.5rem, 3vw + 0.75rem, 2.441rem); }
p  { font-size: clamp(1rem, 1.5vw + 0.75rem, 1.125rem); }
```

---

## 3. Touch Targets & Gestures

**Sources:** [Apple HIG: Targets](https://developer.apple.com/design/human-interface-guidelines/buttons) | [Material Design: Touch Targets](https://m3.material.io/foundations/accessible-design/accessibility-basics) | [WCAG 2.5.8](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum)

### Touch Target Sizes

| Standard | Minimum | Recommended |
|----------|---------|-------------|
| WCAG 2.5.8 (AA) | 24×24px | — |
| Apple HIG | 44×44pt | 44×44pt |
| Material Design | 48×48dp | 48×48dp |
| **Our recommendation** | **44×44px** | **48×48px** |

```css
/* ✅ Ensure touch target size without enlarging visual element */
.icon-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  /* Visual size */
  width: 24px;
  height: 24px;
  /* Touch target expansion */
  padding: 10px;  /* 24 + 10×2 = 44px touch target */
  /* Or use min-width/min-height */
  min-width: 44px;
  min-height: 44px;
}
```

### Touch Gesture Guidelines
| Gesture | Use For | Requirement |
|---------|---------|-------------|
| **Tap** | Activate button/link | Always available |
| **Swipe horizontal** | Carousels, navigation | Also provide button controls |
| **Swipe vertical** | Scroll (default) | Don't hijack |
| **Pinch/zoom** | Images, maps | Never disable with `user-scalable=no` |
| **Long press** | Contextual menus | Always have alternative |
| **Pull to refresh** | List updates | Also provide button |

```html
<!-- ✅ NEVER disable user zoom -->
<meta name="viewport" content="width=device-width, initial-scale=1">

<!-- ❌ This violates WCAG 1.4.4 and breaks accessibility -->
<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no">
```

---

## 4. Mobile Typography

```css
/* Mobile-first typography adjustments */
body {
  font-size: 16px;          /* Minimum — iOS zooms inputs below 16px! */
  -webkit-text-size-adjust: 100%;  /* Prevent font inflation on rotation */
}

/* iOS input font size hack: prevents auto-zoom on focus */
input, select, textarea {
  font-size: max(16px, 1rem); /* Never below 16px on mobile */
}

/* Improve text rendering */
body {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-rendering: optimizeLegibility;
}
```

---

## 5. Mobile Navigation Patterns

**Source:** [NNGroup Mobile Navigation](https://www.nngroup.com/articles/mobile-navigation-patterns/)

### Bottom Tab Bar (Recommended for Mobile Apps)
```html
<nav aria-label="Main navigation" class="bottom-nav">
  <a href="/" aria-current="page" class="nav-tab">
    <svg aria-hidden="true"><!-- home icon --></svg>
    <span>Home</span>
  </a>
  <a href="/search" class="nav-tab">
    <svg aria-hidden="true"><!-- search icon --></svg>
    <span>Search</span>
  </a>
  <a href="/cart" class="nav-tab">
    <svg aria-hidden="true"><!-- cart icon --></svg>
    <span>Cart</span>
    <span class="badge" aria-label="3 items in cart">3</span>
  </a>
  <a href="/profile" class="nav-tab">
    <svg aria-hidden="true"><!-- profile icon --></svg>
    <span>Profile</span>
  </a>
</nav>

<style>
.bottom-nav {
  position: fixed;
  bottom: 0; left: 0; right: 0;
  display: flex;
  background: white;
  border-top: 1px solid var(--color-border);
  /* Safe area inset for iPhone notch */
  padding-bottom: env(safe-area-inset-bottom);
  z-index: 100;
}
.nav-tab {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: var(--space-2);
  min-height: 44px;
  font-size: var(--text-xs);
  gap: 2px;
}
</style>
```

### Hamburger Menu Pattern
```html
<button 
  id="menu-toggle"
  aria-expanded="false"
  aria-controls="mobile-menu"
  aria-label="Open menu"
  class="hamburger">
  <span class="hamburger-line" aria-hidden="true"></span>
  <span class="hamburger-line" aria-hidden="true"></span>
  <span class="hamburger-line" aria-hidden="true"></span>
</button>

<div id="mobile-menu" hidden role="dialog" aria-modal="true" aria-label="Navigation menu">
  <nav>...</nav>
</div>
```

---

## 6. Images & Media on Mobile

```html
<!-- ✅ Responsive images using srcset -->
<img 
  src="photo-800.jpg"
  srcset="photo-400.jpg 400w,
          photo-800.jpg 800w,
          photo-1200.jpg 1200w"
  sizes="(max-width: 768px) 100vw,
         (max-width: 1024px) 50vw,
         33vw"
  alt="Description"
  loading="lazy"
  decoding="async"
  width="800" height="600">
```

```css
/* Fluid video embeds */
.video-wrapper {
  position: relative;
  padding-top: 56.25%; /* 16:9 ratio */
}
.video-wrapper iframe {
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 100%;
}
```

---

## 7. Performance on Mobile

Mobile networks are slower. See [Performance UX](../06-performance-ux/README.md) for full details.

**Mobile-specific priorities:**
- Serve smaller images via `srcset`
- Avoid heavy JavaScript frameworks for simple sites
- Use `font-display: swap` for web fonts
- Target < 3s load time on 4G (Lighthouse Mobile)
- Prioritize LCP element loading

---

## 8. Progressive Web Apps (PWA)

**Source:** [web.dev PWA](https://web.dev/progressive-web-apps/) | [MDN PWA Guide](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps)

### Core PWA Requirements
1. **HTTPS** — Required for service workers
2. **Web App Manifest** — Makes it installable
3. **Service Worker** — Enables offline functionality

```json
// manifest.json
{
  "name": "My App",
  "short_name": "App",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#2563eb",
  "icons": [
    { "src": "/icons/192.png", "sizes": "192x192", "type": "image/png" },
    { "src": "/icons/512.png", "sizes": "512x512", "type": "image/png" }
  ]
}
```

```html
<link rel="manifest" href="/manifest.json">
<meta name="theme-color" content="#2563eb">
<link rel="apple-touch-icon" href="/icons/apple-touch-icon.png">
```

---

## Checklist

- [ ] Mobile viewport meta tag present (without `user-scalable=no`)
- [ ] Mobile-first CSS approach (min-width media queries)
- [ ] All inputs have `font-size: 16px` minimum (prevents iOS zoom)
- [ ] Touch targets ≥ 44×44px for all interactive elements
- [ ] Bottom safe area respected on iOS (`env(safe-area-inset-bottom)`)
- [ ] Images use `srcset` and `sizes` for responsive serving
- [ ] Fluid typography with `clamp()`
- [ ] Mobile navigation tested on real devices (not just emulator)
- [ ] No horizontal scroll on mobile
- [ ] No disabled zoom (`user-scalable=no` absent)
- [ ] Tested on iOS Safari and Android Chrome
- [ ] Performance: LCP < 2.5s on 4G (Lighthouse Mobile)

---

## Sources & Further Reading

| Resource | URL |
|----------|-----|
| Luke Wroblewski: Mobile First | https://www.lukew.com/ff/entry.asp?933 |
| Google Mobile-First Indexing | https://developers.google.com/search/docs/crawling-indexing/mobile/mobile-sites-mobile-first-indexing |
| WCAG 2.5.8 Target Size | https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum |
| Apple HIG: Touch Targets | https://developer.apple.com/design/human-interface-guidelines/buttons |
| Material Design: Touch Targets | https://m3.material.io/foundations/accessible-design/accessibility-basics |
| MDN Responsive Images | https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images |
| CSS Container Queries | https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_containment/Container_queries |
| web.dev PWA | https://web.dev/progressive-web-apps/ |
| NNGroup Mobile Navigation | https://www.nngroup.com/articles/mobile-navigation-patterns/ |

---

*Last verified: November 2026*

---

[< Navigation & IA](../04-navigation-ia/README.md) | [< Back to Knowledge Map](../../README.md) | [Next: Performance UX >](../06-performance-ux/README.md)
