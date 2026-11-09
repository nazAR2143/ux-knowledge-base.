# 03 — Accessibility (a11y): WCAG, ARIA & Inclusive Design

> **Accessibility is not a feature — it is a fundamental quality of good design. Web accessibility means that websites, tools, and technologies are designed so that people with disabilities can use them.**

> **Legal note:** Accessibility is required by law in many jurisdictions — including the EU Web Accessibility Directive, ADA (US), AODA (Canada), and EN 301 549 (EU).

---

## Table of Contents
1. [WCAG 2.2 — Overview & Principles](#1-wcag-22--overview--principles)
2. [Semantic HTML — The Foundation](#2-semantic-html--the-foundation)
3. [ARIA — When & How to Use](#3-aria--when--how-to-use)
4. [Keyboard Navigation](#4-keyboard-navigation)
5. [Focus Management](#5-focus-management)
6. [Screen Reader Support](#6-screen-reader-support)
7. [Images & Media](#7-images--media)
8. [Color & Contrast (a11y)](#8-color--contrast-a11y)
9. [Forms Accessibility](#9-forms-accessibility)
10. [Cognitive Accessibility](#10-cognitive-accessibility)
11. [Testing Tools & Methods](#11-testing-tools--methods)
12. [Checklist](#checklist)
13. [Sources & Further Reading](#sources--further-reading)

---

## 1. WCAG 2.2 — Overview & Principles

**Source:** [W3C WCAG 2.2](https://www.w3.org/TR/WCAG22/) | [Quick Reference](https://www.w3.org/WAI/WCAG22/quickref/)

WCAG is built on **4 principles** (POUR):

| Principle | Meaning | Key Requirement |
|-----------|---------|----------------|
| **P**erceivable | Info must be presentable to all senses | Alt text, captions, contrast |
| **O**perable | UI must be operable without specific modalities | Keyboard access, no seizure triggers |
| **U**nderstandable | Info and UI operation must be understandable | Plain language, predictable behavior |
| **R**obust | Content must work with assistive technologies | Valid HTML, ARIA, future-proof |

### Conformance Levels

| Level | Description | Legal Requirement (EU) |
|-------|-------------|----------------------|
| **A** | Minimum requirements | Partial basis |
| **AA** | Standard target — **your default goal** | Required (EN 301 549) |
| **AAA** | Enhanced — not required site-wide | Best effort |

### New in WCAG 2.2 (2023)
- **2.4.11 Focus Not Obscured (AA):** Focused component not fully hidden by sticky headers
- **2.4.12 Focus Not Obscured Enhanced (AAA):** Fully visible
- **2.5.3 Label in Name (A):** Accessible name contains visible label text
- **2.5.7 Dragging Movements (AA):** Alternative to drag-and-drop required
- **2.5.8 Target Size Minimum (AA):** Touch targets ≥ 24×24px (aim for 44×44px)
- **3.2.6 Consistent Help (A):** Help in same location across pages
- **3.3.7 Redundant Entry (A):** Don't ask for same info twice in a session
- **3.3.8 Accessible Authentication (AA):** No cognitive test required for login

---

## 2. Semantic HTML — The Foundation

**Source:** [MDN: HTML Semantics](https://developer.mozilla.org/en-US/docs/Glossary/Semantics) | [HTML Living Standard](https://html.spec.whatwg.org/)

> **Rule #1:** Always use the most semantically appropriate HTML element. `<div>` and `<span>` have no meaning — use them as a last resort.

```html
<!-- ❌ Bad: No semantic meaning -->
<div class="header">
  <div class="nav">
    <div class="nav-item" onclick="goHome()">Home</div>
  </div>
</div>

<!-- ✅ Good: Semantic HTML -->
<header>
  <nav aria-label="Main navigation">
    <ul>
      <li><a href="/">Home</a></li>
      <li><a href="/about">About</a></li>
    </ul>
  </nav>
</header>
```

### Landmark Elements
```html
<header>      <!-- Site header; wraps logo + main nav -->
<nav>         <!-- Navigation — use aria-label for multiple navs -->
<main>        <!-- Main content — ONE per page -->
<aside>       <!-- Supplementary content (sidebar, related links) -->
<footer>      <!-- Site/section footer -->
<article>     <!-- Self-contained content (blog post, card) -->
<section>     <!-- Thematic grouping — always needs a heading -->
<h1>–<h6>    <!-- Hierarchical headings — NEVER skip levels -->
<figure>      <!-- Media + caption grouping -->
<figcaption>  <!-- Caption for figure -->
```

### Heading Hierarchy
```html
<!-- ✅ Correct: One H1, logical nesting -->
<h1>Page Title</h1>
  <h2>Section A</h2>
    <h3>Subsection A.1</h3>
  <h2>Section B</h2>

<!-- ❌ Wrong: Skipped levels, multiple H1s -->
<h1>Title</h1>
<h1>Also a Title</h1>  <!-- Multiple H1s confuse screen readers -->
<h4>Random subheading</h4>  <!-- Skipped h2, h3 -->
```

---

## 3. ARIA — When & How to Use

**Source:** [WAI-ARIA 1.2](https://www.w3.org/TR/wai-aria-1.2/) | [ARIA Authoring Practices Guide (APG)](https://www.w3.org/WAI/ARIA/apg/)

### The 5 Rules of ARIA

1. **Don't use ARIA if native HTML can do it** — `<button>` is better than `<div role="button">`
2. **Don't change native semantics** — Don't add `role="heading"` to a `<button>`
3. **All interactive ARIA controls must be keyboard accessible**
4. **Don't hide focusable elements** — `aria-hidden="true"` must not be on focusable elements
5. **All interactive elements must have accessible names**

### Common ARIA Attributes

```html
<!-- aria-label: Provides accessible name when no visible label exists -->
<button aria-label="Close dialog">✕</button>

<!-- aria-labelledby: Points to element that labels this one -->
<section aria-labelledby="section-title">
  <h2 id="section-title">Recent Articles</h2>
</section>

<!-- aria-describedby: Points to additional descriptive text -->
<input 
  type="password" 
  aria-describedby="pwd-hint"
  aria-required="true">
<p id="pwd-hint">Must be 8+ characters with at least one number.</p>

<!-- aria-expanded: State for toggleable elements -->
<button aria-expanded="false" aria-controls="menu">Menu</button>
<ul id="menu" hidden>...</ul>

<!-- aria-live: Announce dynamic content changes -->
<div aria-live="polite" aria-atomic="true" id="status"></div>
<!-- Use "assertive" only for critical alerts (errors) -->

<!-- aria-current: Indicates current item -->
<nav>
  <a href="/" aria-current="page">Home</a>
  <a href="/about">About</a>
</nav>
```

### ARIA Roles Reference

| Role | Use Case | Example |
|------|---------|---------|
| `role="alert"` | Critical error messages | `<div role="alert">Error!</div>` |
| `role="status"` | Non-critical status updates | `<div role="status">Saved!</div>` |
| `role="dialog"` | Modal dialogs | `<div role="dialog" aria-modal="true">` |
| `role="tab"` | Tab component | `<button role="tab" aria-selected="true">` |
| `role="tabpanel"` | Tab content panel | `<div role="tabpanel">` |
| `role="tooltip"` | Tooltip element | `<div role="tooltip" id="tip">` |
| `role="progressbar"` | Loading progress | `<div role="progressbar" aria-valuenow="30">` |
| `role="combobox"` | Custom dropdown/autocomplete | With `aria-expanded`, `aria-activedescendant` |

---

## 4. Keyboard Navigation

**Source:** [WebAIM: Keyboard Accessibility](https://webaim.org/techniques/keyboard/) | [ARIA APG Patterns](https://www.w3.org/WAI/ARIA/apg/patterns/)

### Standard Keyboard Interactions

| Key | Action |
|-----|--------|
| `Tab` | Move focus forward through interactive elements |
| `Shift+Tab` | Move focus backward |
| `Enter` | Activate button/link |
| `Space` | Activate button; scroll page |
| `Esc` | Close dialog/modal/dropdown |
| `Arrow keys` | Navigate within widget (tabs, radio groups, menus) |
| `Home`/`End` | First/last item in a list/menu |

### Skip Links
```html
<!-- ✅ Required: Skip to main content -->
<a href="#main-content" class="skip-link">Skip to main content</a>

<style>
.skip-link {
  position: absolute;
  top: -100%;
  left: 0;
  z-index: 9999;
  padding: 0.5rem 1rem;
  background: #000;
  color: #fff;
}
/* Show on focus */
.skip-link:focus {
  top: 0;
}
</style>

<main id="main-content">...</main>
```

### Tab Order
```html
<!-- ✅ Natural DOM order = natural tab order -->
<!-- tabindex="0": Add to non-interactive elements that need focus -->
<div role="button" tabindex="0" onkeydown="handleKey(event)">Custom button</div>

<!-- tabindex="-1": Programmatically focusable but not in tab order -->
<div tabindex="-1" id="modal-container">...</div>

<!-- ❌ NEVER use tabindex > 0 — it breaks natural order -->
<button tabindex="5">This breaks the tab order!</button>
```

---

## 5. Focus Management

**Source:** [MDN: Managing Focus](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques#managing_focus)

### Visible Focus Indicators
```css
/* ✅ Never remove focus outline without replacement */
:focus {
  outline: 3px solid #2563eb;
  outline-offset: 2px;
}

/* Better: Use :focus-visible to avoid outline on mouse click */
:focus-visible {
  outline: 3px solid #2563eb;
  outline-offset: 2px;
  border-radius: 2px;
}
/* This satisfies WCAG 2.4.11 (Focus Not Obscured) in WCAG 2.2 */
```

### Modal Focus Trap
```javascript
// Focus trap pattern for modals (required by WCAG)
function trapFocus(element) {
  const focusable = element.querySelectorAll(
    'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
  );
  const first = focusable[0];
  const last = focusable[focusable.length - 1];

  element.addEventListener('keydown', (e) => {
    if (e.key === 'Tab') {
      if (e.shiftKey && document.activeElement === first) {
        e.preventDefault();
        last.focus();
      } else if (!e.shiftKey && document.activeElement === last) {
        e.preventDefault();
        first.focus();
      }
    }
    if (e.key === 'Escape') closeModal();
  });

  // Move focus into the modal
  first.focus();
}
```

---

## 6. Screen Reader Support

**Sources:** [Screen Reader Testing Guide](https://www.a11yproject.com/posts/getting-started-aria/) | [WebAIM Screen Reader Survey](https://webaim.org/projects/screenreadersurvey9/)

### Popular Screen Readers (Market Share 2024)

| Screen Reader | OS | Browser | Market Share |
|--------------|----|---------|-|
| JAWS | Windows | Chrome, Edge | ~40% |
| NVDA | Windows | Firefox, Chrome | ~35% |
| VoiceOver | macOS/iOS | Safari | ~12% |
| TalkBack | Android | Chrome | ~8% |

### Testing Shortcuts (NVDA)
```
Insert + Space    → Toggle browse/forms mode
H                 → Next heading
1-6               → Next heading by level
B                 → Next button
F                 → Next form element
Insert + F7       → List all links
```

### Announcement Patterns
```javascript
// ✅ Announce dynamic content (e.g., after AJAX load)
function announceToScreenReader(message, priority = 'polite') {
  const announcer = document.getElementById('sr-announcer');
  announcer.setAttribute('aria-live', priority);
  announcer.textContent = '';
  // Timeout ensures screen reader picks up the change
  setTimeout(() => { announcer.textContent = message; }, 100);
}
```

```html
<!-- Include this invisible element in your base template -->
<div 
  id="sr-announcer" 
  aria-live="polite" 
  aria-atomic="true"
  class="sr-only">
</div>

<style>
.sr-only {
  position: absolute;
  width: 1px; height: 1px;
  padding: 0; margin: -1px;
  overflow: hidden;
  clip: rect(0,0,0,0);
  white-space: nowrap;
  border: 0;
}
</style>
```

---

## 7. Images & Media

**Source:** [W3C Alt Text Decision Tree](https://www.w3.org/WAI/tutorials/images/decision-tree/) | [WebAIM: Alt Text](https://webaim.org/techniques/alttext/)

### Alt Text Rules

```html
<!-- ✅ Informative image: describe what it shows in context -->
<img src="chart.png" alt="Bar chart showing 40% increase in sales Q3 2024 vs Q3 2023">

<!-- ✅ Decorative image: empty alt (screen reader ignores) -->
<img src="decorative-wave.svg" alt="" role="presentation">

<!-- ✅ Functional image (button/link): describe the action -->
<a href="/"><img src="logo.png" alt="Acme Corp — Return to homepage"></a>

<!-- ✅ Complex image: use figcaption + link to full description -->
<figure>
  <img src="complex-diagram.png" alt="System architecture diagram — see description below">
  <figcaption>
    <details>
      <summary>Full description</summary>
      <p>The diagram shows three layers: frontend (React), backend (Node.js), and database (PostgreSQL)...</p>
    </details>
  </figcaption>
</figure>
```

### Video & Audio
```html
<!-- Video with captions and audio description -->
<video controls>
  <source src="video.mp4" type="video/mp4">
  <track kind="captions" src="captions-en.vtt" srclang="en" label="English" default>
  <track kind="descriptions" src="descriptions-en.vtt" srclang="en" label="Audio Description">
</video>
```

---

## 8. Color & Contrast (a11y)

Covered in depth in [Visual Design → Color Theory](../02-visual-design/README.md#2-color-theory--contrast).

**Key a11y rules:**
- Minimum 4.5:1 for normal text, 3:1 for large text (WCAG AA)
- Never rely on color alone — use patterns, icons, or text labels
- Test with color blindness simulators

---

## 9. Forms Accessibility

Covered in depth in [Forms & Inputs](../07-forms-inputs/README.md).

**Key a11y rules:**
```html
<!-- ✅ Every input must have a visible, associated label -->
<label for="email">Email address</label>
<input type="email" id="email" name="email" autocomplete="email" required>

<!-- ❌ Placeholder is NOT a label replacement -->
<input type="email" placeholder="Enter email">  <!-- No label! -->
```

---

## 10. Cognitive Accessibility

**Source:** [WCAG 2.2 Cognitive Guidance](https://www.w3.org/WAI/WCAG22/Understanding/cognitive-and-learning-disabilities) | [Cognitive Accessibility Guidance](https://www.w3.org/TR/coga-guidance/)

- **Plain language:** Use simple words, short sentences (see [Content Writing](../08-content-writing/README.md))
- **Consistent navigation:** Same location across pages (WCAG 3.2.3)
- **Error recovery:** Clear, specific error messages with suggestions
- **No time limits:** Or provide sufficient time extension (WCAG 2.2.1)
- **No unexpected changes:** Opening new windows, focus shifts (WCAG 3.2.1)
- **Redundant entry:** Don't repeat form fields already answered (WCAG 3.3.7)

---

## 11. Testing Tools & Methods

| Tool | Type | Use For |
|------|------|---------|
| [axe DevTools](https://www.deque.com/axe/) | Automated | Catch ~57% of issues automatically |
| [WAVE](https://wave.webaim.org/) | Automated | Visual accessibility feedback |
| [Lighthouse](https://developer.chrome.com/docs/lighthouse/) | Automated | Accessibility + performance audit |
| [Colour Contrast Analyser](https://www.tpgi.com/color-contrast-checker/) | Manual tool | Precise contrast testing |
| NVDA + Firefox | Manual | Screen reader testing (Windows) |
| VoiceOver + Safari | Manual | Screen reader testing (Mac/iOS) |
| Keyboard-only navigation | Manual | Full keyboard accessibility |
| [Stark](https://www.getstark.co/) | Plugin | Color blindness simulation in design |

### Automated Testing in CI
```json
// package.json — using axe-core with Playwright
{
  "scripts": {
    "test:a11y": "playwright test --project=accessibility"
  }
}
```

```javascript
// accessibility.spec.js
const { test, expect } = require('@playwright/test');
const { checkA11y } = require('axe-playwright');

test('Homepage meets WCAG 2.2 AA', async ({ page }) => {
  await page.goto('/');
  await checkA11y(page, null, {
    runOnly: { type: 'tag', values: ['wcag2a', 'wcag2aa', 'wcag22aa'] }
  });
});
```

---

## Checklist

- [ ] All images have appropriate alt text
- [ ] All form inputs have visible, associated labels
- [ ] Color contrast meets 4.5:1 (text) and 3:1 (UI components)
- [ ] Color is not the only means of conveying information
- [ ] All functionality accessible via keyboard
- [ ] Skip to main content link present
- [ ] Focus indicators visible on all interactive elements
- [ ] Heading hierarchy is logical (H1 → H2 → H3)
- [ ] One `<main>` landmark per page
- [ ] Multiple `<nav>` elements have distinct `aria-label`s
- [ ] Modals trap focus and restore on close
- [ ] Dynamic content announced via `aria-live`
- [ ] Videos have captions; podcasts have transcripts
- [ ] No time limits (or they can be extended)
- [ ] No content flashes more than 3 times/second (seizure prevention)
- [ ] Site tested with NVDA or VoiceOver
- [ ] Automated a11y tests in CI pipeline

---

## Sources & Further Reading

| Resource | URL |
|----------|-----|
| WCAG 2.2 (Full Standard) | https://www.w3.org/TR/WCAG22/ |
| WCAG Quick Reference | https://www.w3.org/WAI/WCAG22/quickref/ |
| WAI-ARIA Authoring Practices | https://www.w3.org/WAI/ARIA/apg/ |
| WebAIM Alt Text Guide | https://webaim.org/techniques/alttext/ |
| A11y Project | https://www.a11yproject.com/ |
| Deque University | https://dequeuniversity.com/ |
| MDN Accessibility | https://developer.mozilla.org/en-US/docs/Web/Accessibility |
| Inclusive Design Principles | https://inclusivedesignprinciples.org/ |
| Screen Reader Survey (WebAIM) | https://webaim.org/projects/screenreadersurvey9/ |
| axe DevTools | https://www.deque.com/axe/ |

---

*Last verified: November 2026*

---

[← Visual Design](../02-visual-design/README.md) | [← Back to Knowledge Map](../../README.md) | [Next: Navigation & IA →](../04-navigation-ia/README.md)
