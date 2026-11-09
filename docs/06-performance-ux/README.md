# 06 — Performance UX: Core Web Vitals & Perceived Speed

> **Performance IS user experience. 53% of mobile users abandon sites that take more than 3 seconds to load. A 100ms delay in load time can hurt conversion rates by 7%.**

---

## Table of Contents
1. [Core Web Vitals](#1-core-web-vitals)
2. [Largest Contentful Paint (LCP)](#2-largest-contentful-paint-lcp)
3. [Interaction to Next Paint (INP)](#3-interaction-to-next-paint-inp)
4. [Cumulative Layout Shift (CLS)](#4-cumulative-layout-shift-cls)
5. [Perceived Performance Techniques](#5-perceived-performance-techniques)
6. [Loading States & Skeletons](#6-loading-states--skeletons)
7. [Image Optimization](#7-image-optimization)
8. [JavaScript Performance](#8-javascript-performance)
9. [CSS Performance](#9-css-performance)
10. [Measuring & Monitoring](#10-measuring--monitoring)
11. [Checklist](#checklist)
12. [Sources & Further Reading](#sources--further-reading)

---

## 1. Core Web Vitals

**Source:** [web.dev Core Web Vitals](https://web.dev/vitals/) | [Google Search Central](https://developers.google.com/search/docs/appearance/core-web-vitals)

Core Web Vitals are Google's metrics for user experience quality. They directly affect **SEO rankings**.

| Metric | Measures | Good | Needs Improvement | Poor |
|--------|---------|------|------------------|------|
| **LCP** | Loading performance | ≤ 2.5s | 2.5s–4.0s | > 4.0s |
| **INP** | Interactivity | ≤ 200ms | 200ms–500ms | > 500ms |
| **CLS** | Visual stability | ≤ 0.1 | 0.1–0.25 | > 0.25 |

Additional metrics (not CWV but important):
- **TTFB** (Time to First Byte): ≤ 800ms
- **FCP** (First Contentful Paint): ≤ 1.8s
- **TBT** (Total Blocking Time): ≤ 200ms

---

## 2. Largest Contentful Paint (LCP)

**Source:** [web.dev LCP](https://web.dev/lcp/)

LCP measures **when the largest visible element finishes rendering**. Usually: hero image, H1, or above-the-fold block.

### Optimize LCP

**1. Preload the LCP element:**
```html
<!-- ✅ Preload critical above-the-fold image -->
<link rel="preload" as="image" href="/hero.webp" fetchpriority="high">

<!-- ✅ Or set fetchpriority on the img directly -->
<img src="/hero.webp" fetchpriority="high" alt="..." width="1280" height="720">
```

**2. Use modern image formats:**
```html
<picture>
  <source srcset="/hero.avif" type="image/avif">
  <source srcset="/hero.webp" type="image/webp">
  <img src="/hero.jpg" alt="..." width="1280" height="720">
</picture>
```

**3. Eliminate render-blocking resources:**
```html
<!-- Move non-critical CSS to async loading -->
<link rel="preload" href="styles.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
<noscript><link rel="stylesheet" href="styles.css"></noscript>

<!-- Defer non-critical scripts -->
<script src="analytics.js" defer></script>
<script src="chat-widget.js" defer></script>
```

**4. Optimize TTFB:**
- Use CDN for static assets
- Enable HTTP/2 or HTTP/3
- Server-side rendering (SSR) or Static Site Generation (SSG)
- Cache HTML responses aggressively

---

## 3. Interaction to Next Paint (INP)

**Source:** [web.dev INP](https://web.dev/inp/) *(Replaced FID in March 2024)*

INP measures **responsiveness**: the delay between user input and the next visual update.

### Optimize INP

**1. Break up long tasks:**
```javascript
// ❌ Long task blocks main thread
function processLargeList(items) {
  items.forEach(item => heavyOperation(item)); // Blocks for 500ms+
}

// ✅ Break into chunks with scheduler
async function processLargeListAsync(items) {
  for (const item of items) {
    heavyOperation(item);
    // Yield to allow browser to render
    if (shouldYield()) {
      await new Promise(resolve => setTimeout(resolve, 0));
    }
  }
}

// Even better: Use scheduler.yield() (Chrome 115+)
async function processWithScheduler(items) {
  for (const item of items) {
    heavyOperation(item);
    await scheduler.yield();
  }
}
```

**2. Avoid layout thrashing:**
```javascript
// ❌ Layout thrashing: read-write-read-write
elements.forEach(el => {
  const height = el.offsetHeight;    // Read (forces layout)
  el.style.height = height + 'px';  // Write (invalidates layout)
});

// ✅ Batch reads then writes
const heights = elements.map(el => el.offsetHeight);  // Batch reads
elements.forEach((el, i) => { el.style.height = heights[i] + 'px'; }); // Batch writes
```

**3. Use CSS for animations (not JS):**
```css
/* ✅ CSS animations run on compositor thread */
.animated {
  transform: translateX(100px);  /* GPU-accelerated */
  opacity: 0.5;                  /* GPU-accelerated */
  transition: transform 300ms ease, opacity 300ms ease;
}

/* ❌ These trigger layout — expensive */
.bad-animation {
  left: 100px;    /* Layout */
  width: 200px;   /* Layout */
  margin: 10px;   /* Layout */
}
```

---

## 4. Cumulative Layout Shift (CLS)

**Source:** [web.dev CLS](https://web.dev/cls/)

CLS measures **visual stability** — how much page content unexpectedly shifts.

### Prevent CLS

**1. Reserve space for images and embeds:**
```html
<!-- ✅ Always specify width + height -->
<img src="photo.jpg" width="800" height="600" alt="...">

<!-- ✅ CSS aspect-ratio for responsive images -->
<style>
img { aspect-ratio: 4/3; width: 100%; height: auto; }
</style>
```

**2. Reserve space for ads and embeds:**
```css
/* Reserve slot height before ad loads */
.ad-slot {
  min-height: 250px;  /* Standard banner height */
  background: var(--color-surface-secondary);
}
.video-embed { aspect-ratio: 16/9; }
```

**3. Never insert content above existing content:**
```javascript
// ❌ Inserting cookie banner that pushes content down
document.body.insertBefore(cookieBanner, document.body.firstChild);

// ✅ Use fixed/sticky positioning for banners
cookieBanner.style.position = 'fixed';
cookieBanner.style.bottom = '0';
```

**4. Preload web fonts:**
```css
@font-face {
  font-family: 'Inter';
  src: url('/fonts/inter.woff2') format('woff2');
  font-display: swap;  /* Show fallback immediately, swap when ready */
}
```
```html
<link rel="preload" href="/fonts/inter.woff2" as="font" type="font/woff2" crossorigin>
```

---

## 5. Perceived Performance Techniques

**Source:** [NNGroup Response Times](https://www.nngroup.com/articles/response-times-3-important-limits/)

### Response Time Thresholds
| Delay | User Perception | Required Action |
|-------|----------------|----------------|
| **< 100ms** | Instantaneous | None needed |
| **100ms–1s** | Slight delay, user stays in flow | None, but optimize |
| **1–10s** | User notices wait | Show progress indicator |
| **> 10s** | User likely to leave | Provide progress, allow cancel |

### Optimistic UI
```javascript
// ✅ Update UI before server confirms (rollback on error)
async function likePost(postId) {
  // 1. Immediately update UI
  setLiked(true);
  setLikeCount(count => count + 1);
  
  try {
    // 2. Send to server
    await api.post(`/posts/${postId}/like`);
  } catch (error) {
    // 3. Rollback on failure
    setLiked(false);
    setLikeCount(count => count - 1);
    showError('Failed to like post. Please try again.');
  }
}
```

---

## 6. Loading States & Skeletons

**Source:** [NNGroup Skeleton Screens](https://www.nngroup.com/articles/skeleton-screens/)

### When to Use Each

| Pattern | Use When | Avoid When |
|---------|----------|-----------|
| **Spinner** | Unknown duration, indeterminate | Known duration, long waits |
| **Progress bar** | Known/estimable duration | Truly indeterminate operations |
| **Skeleton screen** | Content-heavy pages (cards, feeds) | Simple operations |
| **Instant** | < 100ms operations | Never show feedback for instant ops |
| **Optimistic UI** | High confidence operations | Risky/complex operations |

```html
<!-- ✅ Skeleton screen pattern -->
<div class="card-skeleton" aria-busy="true" aria-label="Loading content">
  <div class="skeleton-line skeleton-title"></div>
  <div class="skeleton-line"></div>
  <div class="skeleton-line skeleton-short"></div>
</div>

<style>
.skeleton-line {
  height: 1em;
  background: linear-gradient(90deg, 
    var(--color-surface-secondary) 25%, 
    #e2e8f0 50%, 
    var(--color-surface-secondary) 75%);
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
  border-radius: 4px;
  margin-bottom: 0.75em;
}

@keyframes shimmer {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}

/* ✅ Respect reduced motion */
@media (prefers-reduced-motion: reduce) {
  .skeleton-line { animation: none; }
}
</style>
```

---

## 7. Image Optimization

```bash
# Recommended formats by use case
# Photos:    WebP (primary) + JPEG (fallback)  
# Graphics:  SVG (icons, logos) or WebP
# Screenshots/UI: WebP or AVIF
# Animations: CSS or AVIF (not GIF — 10x larger)
```

```html
<!-- Complete image optimization pattern -->
<picture>
  <!-- Next-gen format with responsive sizes -->
  <source
    type="image/avif"
    srcset="/img/photo-400.avif 400w, /img/photo-800.avif 800w, /img/photo-1200.avif 1200w"
    sizes="(max-width: 768px) 100vw, 50vw">
  <source
    type="image/webp"
    srcset="/img/photo-400.webp 400w, /img/photo-800.webp 800w, /img/photo-1200.webp 1200w"
    sizes="(max-width: 768px) 100vw, 50vw">
  <!-- JPEG fallback -->
  <img
    src="/img/photo-800.jpg"
    alt="Descriptive alt text"
    width="800" height="600"
    loading="lazy"       <!-- Defer off-screen images -->
    decoding="async">    <!-- Non-blocking decode -->
</picture>
```

---

## 8. JavaScript Performance

```javascript
// ✅ Dynamic imports (code splitting)
const { Chart } = await import('./chart.js');  // Load only when needed

// ✅ Web Workers for heavy computation
const worker = new Worker('./heavy-task.js');
worker.postMessage({ data: largeDataset });
worker.onmessage = (e) => updateUI(e.data);

// ✅ Debounce for search/resize
function debounce(fn, delay) {
  let timer;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => fn(...args), delay);
  };
}
const handleSearch = debounce(search, 300);
input.addEventListener('input', handleSearch);

// ✅ Throttle for scroll events
function throttle(fn, limit) {
  let inThrottle;
  return (...args) => {
    if (!inThrottle) {
      fn(...args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  };
}
window.addEventListener('scroll', throttle(handleScroll, 100));
```

---

## 9. CSS Performance

```css
/* ✅ Use CSS containment */
.card { contain: layout style; }

/* ✅ will-change only for elements you KNOW will animate */
.modal { will-change: transform; }  /* Set just before animation */

/* ✅ Use logical properties for i18n */
.card { margin-block: var(--space-4); padding-inline: var(--space-6); }

/* ✅ content-visibility for off-screen content */
.below-fold-section {
  content-visibility: auto;
  contain-intrinsic-size: 0 500px;  /* Estimated height */
}
```

---

## 10. Measuring & Monitoring

| Tool | Type | Use For |
|------|------|---------|
| [Chrome Lighthouse](https://developer.chrome.com/docs/lighthouse/) | Synthetic | Dev testing, CI integration |
| [PageSpeed Insights](https://pagespeed.web.dev/) | Synthetic + Field | Full CWV analysis |
| [WebPageTest](https://www.webpagetest.org/) | Synthetic | Deep waterfall analysis |
| [Chrome CrUX](https://developer.chrome.com/docs/crux/) | Field (real users) | Real-world performance |
| [Vercel Speed Insights](https://vercel.com/docs/speed-insights) | Field | CWV from real visitors |

```javascript
// ✅ Measure Core Web Vitals in production
import { onLCP, onINP, onCLS } from 'web-vitals';

function sendToAnalytics(metric) {
  navigator.sendBeacon('/analytics', JSON.stringify({
    name: metric.name,
    value: metric.value,
    rating: metric.rating  // 'good' | 'needs-improvement' | 'poor'
  }));
}

onLCP(sendToAnalytics);
onINP(sendToAnalytics);
onCLS(sendToAnalytics);
```

---

## Checklist

- [ ] LCP ≤ 2.5s (PageSpeed Insights)
- [ ] INP ≤ 200ms (PageSpeed Insights)
- [ ] CLS ≤ 0.1 (PageSpeed Insights)
- [ ] LCP element preloaded with `fetchpriority="high"`
- [ ] All images have `width` and `height` attributes
- [ ] Images use WebP/AVIF format
- [ ] `loading="lazy"` on below-fold images
- [ ] No `user-scalable=no` in viewport
- [ ] Web fonts use `font-display: swap`
- [ ] Critical fonts preloaded
- [ ] Third-party scripts loaded with `defer` or `async`
- [ ] No render-blocking resources in `<head>`
- [ ] Long tasks broken up (< 50ms per task)
- [ ] CSS animations use `transform`/`opacity` only
- [ ] Loading states for all async operations > 100ms
- [ ] Real User Monitoring (RUM) implemented

---

## Sources & Further Reading

| Resource | URL |
|----------|-----|
| Core Web Vitals | https://web.dev/vitals/ |
| web.dev LCP | https://web.dev/lcp/ |
| web.dev INP | https://web.dev/inp/ |
| web.dev CLS | https://web.dev/cls/ |
| NNGroup Response Times | https://www.nngroup.com/articles/response-times-3-important-limits/ |
| NNGroup Skeleton Screens | https://www.nngroup.com/articles/skeleton-screens/ |
| PageSpeed Insights | https://pagespeed.web.dev/ |
| WebPageTest | https://www.webpagetest.org/ |
| web-vitals JS library | https://github.com/GoogleChrome/web-vitals |

---

*Last verified: November 2026*

---

[< Mobile & Responsive](../05-mobile-responsive/README.md) | [< Back to Knowledge Map](../../README.md) | [Next: Forms & Inputs >](../07-forms-inputs/README.md)
