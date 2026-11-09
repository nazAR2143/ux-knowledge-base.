# 02 — Visual Design: Typography, Color, Spacing & Hierarchy

> **Visual design is not decoration — it is a functional system that guides attention, communicates meaning, and builds trust.**

---

## Table of Contents
1. [Typography](#1-typography)
2. [Color Theory & Contrast](#2-color-theory--contrast)
3. [Spacing & White Space](#3-spacing--white-space)
4. [Visual Hierarchy](#4-visual-hierarchy)
5. [Grid Systems](#5-grid-systems)
6. [Icons & Imagery](#6-icons--imagery)
7. [Motion & Animation](#7-motion--animation)
8. [Design Tokens](#8-design-tokens)
9. [Checklist](#checklist)
10. [Sources & Further Reading](#sources--further-reading)

---

## 1. Typography

**Sources:** [Google Fonts Knowledge](https://fonts.google.com/knowledge) | [Butterick's Practical Typography](https://practicaltypography.com/)

### Type Scale
Use a **modular scale** to create harmonious font sizes. The [Major Third (1.25x)](https://typescale.com/) scale is a safe default:

| Level | Size (rem) | Use Case |
|-------|-----------|----------|
| `--text-xs` | 0.64rem | Captions, labels |
| `--text-sm` | 0.8rem | Secondary text, metadata |
| `--text-base` | 1rem (16px) | Body text (**minimum**) |
| `--text-lg` | 1.25rem | Lead paragraph |
| `--text-xl` | 1.563rem | H4 |
| `--text-2xl` | 1.953rem | H3 |
| `--text-3xl` | 2.441rem | H2 |
| `--text-4xl` | 3.052rem | H1 |

```css
/* Design tokens for type scale */
:root {
  --text-base: 1rem;      /* 16px — NEVER go below this for body */
  --text-lg: 1.25rem;
  --text-xl: 1.563rem;
  --text-2xl: 1.953rem;
  --text-3xl: 2.441rem;
  --text-4xl: 3.052rem;

  /* Line heights */
  --leading-tight: 1.25;   /* Headlines */
  --leading-normal: 1.5;   /* Body text — minimum for readability */
  --leading-loose: 1.75;   /* Long-form text */

  /* Measure (line length) */
  --measure: 65ch;         /* 45–75 characters is optimal */
}

body {
  font-size: var(--text-base);
  line-height: var(--leading-normal);
  max-width: var(--measure);
}
```

### Font Selection Rules
- **Legibility first:** Choose fonts optimized for screen rendering
- **Limit font families:** Maximum 2 (one serif + one sans-serif, or one display + one body)
- **System font stack** as fallback for performance:

```css
/* System font stack (fastest, best rendering) */
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 
             Oxygen, Ubuntu, sans-serif;
```

### Body Text Guidelines
| Property | Recommendation | Reason |
|----------|---------------|--------|
| Font size | ≥ 16px (1rem) | Below 16px causes eye strain |
| Line height | 1.5–1.6 | Improves readability |
| Line length | 45–75 characters | Optimal reading width |
| Font weight | 400–500 | Bold for weight < 300px screen |
| Letter spacing | 0 to 0.05em | Only adjust for ALL CAPS or small text |

---

## 2. Color Theory & Contrast

**Sources:** [WCAG 2.2 Contrast Requirements](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum) | [Refactoring UI Color](https://www.refactoringui.com/)

### WCAG Contrast Ratios (Mandatory)

| Level | Ratio | Text Size |
|-------|-------|-----------|
| **AA (minimum)** | 4.5:1 | Normal text (< 18pt/24px) |
| **AA large** | 3:1 | Large text (≥ 18pt/24px bold, ≥ 24pt/32px regular) |
| **AAA (enhanced)** | 7:1 | Normal text |
| **UI Components** | 3:1 | Borders, icons, focus rings |

**Testing tools:**
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [Colour Contrast Analyser (desktop app)](https://www.tpgi.com/color-contrast-checker/)
- [Chrome DevTools accessibility tree](https://developer.chrome.com/docs/devtools/accessibility/reference/)

### Color System Architecture

```css
:root {
  /* 1. Define primitive colors */
  --blue-50: #eff6ff;
  --blue-100: #dbeafe;
  --blue-500: #3b82f6;
  --blue-600: #2563eb;
  --blue-900: #1e3a8a;

  /* 2. Define semantic tokens */
  --color-primary: var(--blue-600);
  --color-primary-hover: var(--blue-700);
  --color-primary-text: white;        /* Must meet 4.5:1 on --color-primary */

  --color-surface: white;
  --color-surface-secondary: var(--gray-50);
  --color-text: var(--gray-900);      /* 4.5:1+ on white */
  --color-text-secondary: var(--gray-600); /* 4.5:1+ on white */
  --color-text-disabled: var(--gray-400); /* Lower contrast — decorative only */

  --color-error: #dc2626;             /* Must meet contrast on its background */
  --color-success: #16a34a;
  --color-warning: #d97706;
  --color-info: var(--blue-600);
}
```

### Color Usage Rules
1. **Never use color alone** to convey meaning (colorblind users) — always pair with text, icon, or pattern
2. **Test in grayscale** — design should still work without color
3. **8% of men** have color vision deficiency — test with [Sim Daltonism](https://michelf.ca/projects/sim-daltonism/) or [Stark](https://www.getstark.co/)
4. **Dark mode:** Define semantic tokens — don't just invert colors

```css
/* ✅ Good: Color + icon + text conveys meaning */
.error-message {
  color: var(--color-error);
}
.error-message::before {
  content: "⚠ Error: ";  /* Text label, not just icon */
}

/* ❌ Bad: Color alone */
.error-message { color: red; }
```

---

## 3. Spacing & White Space

**Source:** [8-Point Grid System](https://spec.fm/specifics/8-pt-grid) | [Space in Design Systems](https://medium.com/eightshapes-llc/space-in-design-systems-188bcbae0d62)

### The 8-Point Grid
Use multiples of 8px (or 4px base) for all spacing. This creates visual harmony and aligns with device pixel densities:

```css
:root {
  --space-1: 0.25rem;   /* 4px */
  --space-2: 0.5rem;    /* 8px */
  --space-3: 0.75rem;   /* 12px */
  --space-4: 1rem;      /* 16px */
  --space-5: 1.25rem;   /* 20px */
  --space-6: 1.5rem;    /* 24px */
  --space-8: 2rem;      /* 32px */
  --space-10: 2.5rem;   /* 40px */
  --space-12: 3rem;     /* 48px */
  --space-16: 4rem;     /* 64px */
  --space-20: 5rem;     /* 80px */
  --space-24: 6rem;     /* 96px */
}
```

### Spacing Principles
- **Proximity:** Related elements are closer; unrelated elements have more space
- **Internal vs. external:** Use padding for internal space, margin for external separation
- **Section spacing:** Major sections need 2–4× more space than element spacing
- **White space is active:** It directs the eye and reduces cognitive load

---

## 4. Visual Hierarchy

**Source:** [Visual Hierarchy in UX](https://www.nngroup.com/articles/visual-hierarchy-ux-definition/) — NNGroup

Hierarchy is established through **6 mechanisms** (in order of power):

1. **Size** — Larger = more important
2. **Weight** — Bold = important; thin = secondary
3. **Color/Contrast** — High contrast = prominent; low contrast = secondary
4. **Position** — Top-left = highest priority (F-pattern reading)
5. **Whitespace** — Isolated elements draw more attention
6. **Typography** — Different fonts signal different content types

### F-Pattern & Z-Pattern Reading

| Pattern | When It Occurs | Design Implication |
|---------|---------------|-------------------|
| **F-Pattern** | Long-form text, search results | Put key info in first 2 lines; left-align important content |
| **Z-Pattern** | Short pages, landing pages | CTA at end of Z path (bottom-right) |
| **Layer Cake** | Structured content with headers | Use clear heading hierarchy |

### Typographic Hierarchy Example
```css
h1 { font-size: var(--text-4xl); font-weight: 800; }
h2 { font-size: var(--text-3xl); font-weight: 700; }
h3 { font-size: var(--text-2xl); font-weight: 600; }
h4 { font-size: var(--text-xl);  font-weight: 600; }
p  { font-size: var(--text-base); font-weight: 400; color: var(--color-text); }
.caption { font-size: var(--text-sm); color: var(--color-text-secondary); }
```

---

## 5. Grid Systems

**Source:** [CSS Grid Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout) | [Bootstrap Grid](https://getbootstrap.com/docs/5.3/layout/grid/)

### 12-Column Grid (Most Flexible)
```css
.container {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: var(--space-6);
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 var(--space-4);
}

/* Responsive breakpoints */
@media (max-width: 768px) {
  .container { grid-template-columns: 1fr; }
}
```

### Standard Breakpoints
| Name | Width | Target |
|------|-------|--------|
| `sm` | 640px | Large mobile |
| `md` | 768px | Tablets |
| `lg` | 1024px | Small laptops |
| `xl` | 1280px | Desktops |
| `2xl` | 1536px | Large screens |

---

## 6. Icons & Imagery

**Sources:** [Icon Usability](https://www.nngroup.com/articles/icon-usability/) — NNGroup

### Icon Best Practices
- **Always label icons** unless universally understood (hamburger menu, ✕ close, ✓ check)
- **Minimum touch size:** 44×44px (Apple HIG) / 48×48dp (Material Design)
- **SVG over icon fonts** for performance, accessibility, and sharp rendering
- **Consistent stroke weight** across icon set

```html
<!-- ✅ Good: Icon with accessible label -->
<button aria-label="Open navigation menu">
  <svg aria-hidden="true" focusable="false" width="24" height="24">
    <!-- hamburger paths -->
  </svg>
</button>

<!-- ✅ Good: Icon + visible text -->
<button>
  <svg aria-hidden="true" focusable="false">...</svg>
  Save Changes
</button>
```

### Image Performance
```html
<!-- ✅ Responsive images with art direction -->
<picture>
  <source media="(max-width: 768px)" srcset="hero-mobile.webp" type="image/webp">
  <source media="(min-width: 769px)" srcset="hero-desktop.webp" type="image/webp">
  <img 
    src="hero-desktop.jpg" 
    alt="Descriptive alt text — not 'hero image'" 
    width="1280" 
    height="720"
    loading="lazy"
    decoding="async">
</picture>
```

---

## 7. Motion & Animation

**Sources:** [Google Material Motion](https://m3.material.io/styles/motion/overview) | [Reduced Motion](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion)

### Animation Principles
- **Purpose over decoration:** Every animation should communicate meaning
- **Duration:** UI transitions 150–300ms; page transitions 300–500ms
- **Easing:** `ease-out` for elements entering; `ease-in` for elements leaving

```css
/* ✅ Always respect user's motion preferences */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}

/* Standard transition */
.btn { transition: background-color 150ms ease-out, transform 150ms ease-out; }
.modal { animation: slide-up 300ms ease-out; }
```

---

## 8. Design Tokens

**Source:** [Design Tokens W3C Community Group](https://www.w3.org/community/design-tokens/) | [Style Dictionary](https://amzn.github.io/style-dictionary/)

Design tokens are the **single source of truth** for design decisions:

```json
{
  "color": {
    "primary": { "value": "#2563eb", "$type": "color" },
    "primary-hover": { "value": "#1d4ed8", "$type": "color" }
  },
  "typography": {
    "body": {
      "fontFamily": { "value": "Inter, sans-serif", "$type": "fontFamily" },
      "fontSize": { "value": "1rem", "$type": "dimension" },
      "lineHeight": { "value": 1.5, "$type": "number" }
    }
  },
  "spacing": {
    "4": { "value": "1rem", "$type": "dimension" }
  }
}
```

---

## Checklist

- [ ] Font size ≥ 16px for body text
- [ ] Line height ≥ 1.5 for body text
- [ ] Line length 45–75 characters
- [ ] Maximum 2 font families
- [ ] All text meets WCAG AA contrast (4.5:1 normal, 3:1 large)
- [ ] Color is not the sole means of conveying information
- [ ] Spacing uses consistent scale (multiples of 4 or 8)
- [ ] Visual hierarchy established with ≥ 3 levels of weight/size
- [ ] Icons ≥ 44×44px and have accessible labels
- [ ] `prefers-reduced-motion` respected in all animations
- [ ] Design tokens defined for all reusable values

---

## Sources & Further Reading

| Resource | URL |
|----------|-----|
| Google Fonts Knowledge | https://fonts.google.com/knowledge |
| Practical Typography | https://practicaltypography.com/ |
| WCAG 2.2 Contrast | https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum |
| WebAIM Contrast Checker | https://webaim.org/resources/contrastchecker/ |
| 8-Point Grid System | https://spec.fm/specifics/8-pt-grid |
| Refactoring UI | https://www.refactoringui.com/ |
| Material Design Color | https://m3.material.io/styles/color/overview |
| MDN Prefers Reduced Motion | https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion |
| Design Tokens W3C | https://www.w3.org/community/design-tokens/ |
| Icon Usability (NNGroup) | https://www.nngroup.com/articles/icon-usability/ |

---

*Last verified: November 2026*

---

[< UX Foundations](../01-foundations/README.md) | [< Back to Knowledge Map](../../README.md) | [Next: Accessibility >](../03-accessibility/README.md)
