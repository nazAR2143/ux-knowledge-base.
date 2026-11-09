# 10 — Checklists & Audit Templates

> **A checklist is not a substitute for expertise — it is a safeguard against forgetting. Use these before every release, redesign, and audit.**

---

## Table of Contents
1. [Pre-Launch UX Checklist](#1-pre-launch-ux-checklist)
2. [Accessibility Audit Template](#2-accessibility-audit-template)
3. [Performance Audit Template](#3-performance-audit-template)
4. [Mobile UX Audit](#4-mobile-ux-audit)
5. [Forms Audit Template](#5-forms-audit-template)
6. [Content Audit Template](#6-content-audit-template)
7. [Heuristic Evaluation Template](#7-heuristic-evaluation-template)
8. [Design Handoff Checklist](#8-design-handoff-checklist)
9. [Sources & Further Reading](#sources--further-reading)

---

## 1. Pre-Launch UX Checklist

> Run this checklist for every major release. Score each item: ✅ Pass | ⚠️ Needs work | ❌ Fail | N/A

### Foundations
- [ ] Clear value proposition on homepage (above the fold)
- [ ] Primary CTA visible without scrolling
- [ ] Page titles are unique and descriptive
- [ ] Favicon and Open Graph meta tags set
- [ ] 404 page helpful (search + navigation)
- [ ] Privacy policy and terms linked in footer
- [ ] Contact information easily findable

### Navigation
- [ ] Primary nav ≤ 7 items
- [ ] Active page indicated in navigation (`aria-current="page"`)
- [ ] Breadcrumbs on pages ≥ 3 levels deep
- [ ] Logo links to homepage
- [ ] Skip-to-content link present and working
- [ ] All navigation keyboard accessible
- [ ] Mobile navigation tested on real devices
- [ ] Search works and returns relevant results

### Visual Design
- [ ] Typography: body ≥ 16px, line-height ≥ 1.5
- [ ] Text contrast ≥ 4.5:1 on all backgrounds
- [ ] UI component contrast ≥ 3:1 (borders, icons)
- [ ] Color not the only way to convey information
- [ ] Consistent spacing (8pt grid system)
- [ ] Visual hierarchy clear (H1 → H2 → H3)
- [ ] Design tested in dark mode (if supported)
- [ ] Favicon and brand assets consistent

### Accessibility (WCAG 2.2 AA)
- [ ] All images have alt text (or empty alt for decorative)
- [ ] All form inputs have visible labels
- [ ] Heading hierarchy is logical (no skipped levels)
- [ ] Focus indicators visible on all interactive elements
- [ ] No `outline: none` without replacement
- [ ] `lang` attribute on `<html>` element
- [ ] Landmark regions present (`<main>`, `<nav>`, `<header>`, `<footer>`)
- [ ] ARIA used only where native HTML insufficient
- [ ] Site tested with NVDA or VoiceOver
- [ ] Automated a11y test run (axe, Lighthouse)

### Forms
- [ ] All inputs have top-aligned visible labels
- [ ] Placeholder text supplements (not replaces) labels
- [ ] Required fields marked with asterisk + legend
- [ ] Appropriate `type` attribute on all inputs
- [ ] `autocomplete` attributes on all relevant fields
- [ ] Input `font-size` ≥ 16px (prevents iOS zoom)
- [ ] Validation happens on blur (not aggressive real-time)
- [ ] Error messages: specific, actionable, polite
- [ ] `aria-invalid="true"` set on invalid fields
- [ ] Error icon + color + text (not color alone)
- [ ] Submit button shows loading state

### Performance
- [ ] Lighthouse score ≥ 90 (Performance, Accessibility, Best Practices)
- [ ] LCP ≤ 2.5s (PageSpeed Insights Mobile)
- [ ] CLS ≤ 0.1
- [ ] INP ≤ 200ms
- [ ] All images have `width` and `height` attributes
- [ ] Images use WebP/AVIF format
- [ ] `loading="lazy"` on below-fold images
- [ ] LCP element has `fetchpriority="high"`
- [ ] Web fonts use `font-display: swap`
- [ ] No render-blocking scripts in `<head>` (use `defer`/`async`)

### Mobile
- [ ] Viewport meta tag correct (no `user-scalable=no`)
- [ ] No horizontal scroll on any breakpoint
- [ ] Touch targets ≥ 44×44px
- [ ] iOS safe area insets applied (bottom tab bars, etc.)
- [ ] Tested on actual iOS Safari and Android Chrome
- [ ] Text readable without zooming

### Content
- [ ] No lorem ipsum in production
- [ ] No "TBD" or placeholder content
- [ ] All links have descriptive text (not "click here")
- [ ] External links open appropriately (with aria-label if new tab)
- [ ] Spelling and grammar checked
- [ ] Tone consistent with brand guidelines

---

## 2. Accessibility Audit Template

**Standard:** WCAG 2.2 Level AA  
**Testing tools:** axe DevTools, WAVE, NVDA/VoiceOver, Keyboard-only  
**Auditor:** ____________ | **Date:** ____________ | **URL:** ____________

### POUR Principles

#### Perceivable
| Criterion | Level | Description | Status | Notes |
|-----------|-------|-------------|--------|-------|
| 1.1.1 Non-text Content | A | Alt text for images | | |
| 1.2.1 Audio-only/Video-only | A | Transcript/alternative | | |
| 1.2.2 Captions | A | Synchronized captions | | |
| 1.2.3 Audio Description | A | Alt for video | | |
| 1.3.1 Info and Relationships | A | Semantic HTML structure | | |
| 1.3.2 Meaningful Sequence | A | Logical reading order | | |
| 1.3.3 Sensory Characteristics | A | No shape/color-only instructions | | |
| 1.3.4 Orientation | AA | No locked orientation | | |
| 1.3.5 Input Purpose | AA | Autocomplete attributes | | |
| 1.4.1 Use of Color | A | Color not sole indicator | | |
| 1.4.2 Audio Control | A | Auto-playing audio control | | |
| 1.4.3 Contrast (Minimum) | AA | 4.5:1 text, 3:1 large | | |
| 1.4.4 Resize Text | AA | Zoom to 200% works | | |
| 1.4.5 Images of Text | AA | No images of text | | |
| 1.4.10 Reflow | AA | Scroll one direction at 320px | | |
| 1.4.11 Non-text Contrast | AA | 3:1 for UI components | | |
| 1.4.12 Text Spacing | AA | Custom spacing doesn't break | | |
| 1.4.13 Content on Hover/Focus | AA | Hover content dismissable | | |

#### Operable
| Criterion | Level | Description | Status | Notes |
|-----------|-------|-------------|--------|-------|
| 2.1.1 Keyboard | A | All functionality via keyboard | | |
| 2.1.2 No Keyboard Trap | A | Focus not trapped | | |
| 2.2.1 Timing Adjustable | A | Extend time limits | | |
| 2.2.2 Pause, Stop, Hide | A | Control moving content | | |
| 2.3.1 Three Flashes | A | No seizure-inducing content | | |
| 2.4.1 Bypass Blocks | A | Skip navigation link | | |
| 2.4.2 Page Titled | A | Descriptive page titles | | |
| 2.4.3 Focus Order | A | Logical focus sequence | | |
| 2.4.4 Link Purpose | A | Descriptive link text | | |
| 2.4.6 Headings and Labels | AA | Descriptive headings | | |
| 2.4.7 Focus Visible | AA | Visible focus indicator | | |
| 2.4.11 Focus Not Obscured | AA | Focused item not fully hidden | | |
| 2.5.3 Label in Name | A | Accessible name contains visible label | | |
| 2.5.7 Dragging Movements | AA | Alternative to drag & drop | | |
| 2.5.8 Target Size Minimum | AA | 24×24px minimum touch target | | |

#### Understandable
| Criterion | Level | Description | Status | Notes |
|-----------|-------|-------------|--------|-------|
| 3.1.1 Language of Page | A | `lang` on `<html>` | | |
| 3.1.2 Language of Parts | AA | `lang` on content in other language | | |
| 3.2.1 On Focus | A | No unexpected context change | | |
| 3.2.2 On Input | A | No unexpected context change | | |
| 3.2.3 Consistent Navigation | AA | Nav in same location across pages | | |
| 3.2.4 Consistent Identification | AA | Same components identified same way | | |
| 3.3.1 Error Identification | A | Errors identified and described | | |
| 3.3.2 Labels or Instructions | A | Labels for inputs | | |
| 3.3.3 Error Suggestion | AA | Suggests fix for errors | | |
| 3.3.4 Error Prevention | AA | Reversible/checkable submissions | | |
| 3.3.7 Redundant Entry | A | Don't re-ask entered data | | |
| 3.3.8 Accessible Authentication | AA | No cognitive test required | | |

#### Robust
| Criterion | Level | Description | Status | Notes |
|-----------|-------|-------------|--------|-------|
| 4.1.1 Parsing | A | Valid HTML | | |
| 4.1.2 Name, Role, Value | A | ARIA correct | | |
| 4.1.3 Status Messages | AA | Status announced without focus | | |

**Summary Score:** ___ / ___ criteria pass | Critical issues: ___ | Needs work: ___

---

## 3. Performance Audit Template

**Tool:** PageSpeed Insights + WebPageTest  
**URL tested:** ____________ | **Date:** ____________ | **Device:** Mobile / Desktop

| Metric | Target | Measured | Status |
|--------|--------|---------|--------|
| **LCP** | ≤ 2.5s | | |
| **INP** | ≤ 200ms | | |
| **CLS** | ≤ 0.1 | | |
| **FCP** | ≤ 1.8s | | |
| **TTFB** | ≤ 800ms | | |
| **TBT** | ≤ 200ms | | |
| **Lighthouse Performance** | ≥ 90 | | |
| **Lighthouse Accessibility** | ≥ 90 | | |
| **Lighthouse Best Practices** | ≥ 90 | | |
| **Lighthouse SEO** | ≥ 90 | | |
| **Total page weight** | ≤ 1MB | | |
| **Number of requests** | ≤ 50 | | |
| **JavaScript size** | ≤ 200KB (gzipped) | | |
| **Image optimization** | WebP/AVIF used | | |

**Top opportunities identified:**
1. 
2. 
3. 

---

## 4. Mobile UX Audit

Conduct on **real devices**: iPhone (Safari) + Android (Chrome)

| Check | iOS Safari | Android Chrome |
|-------|-----------|----------------|
| Viewport meta correct | | |
| No horizontal scroll | | |
| Touch targets ≥ 44px | | |
| Input fonts ≥ 16px (no auto-zoom) | | |
| Bottom safe area inset (iPhone) | | |
| Zoom not disabled | | |
| Images not broken / overflow | | |
| Navigation usable on small screen | | |
| Text readable without pinch-zoom | | |
| Forms work with mobile keyboard | | |
| Appropriate keyboard types shown | | |
| Load time acceptable on 4G | | |

---

## 5. Forms Audit Template

For each major form on the site:

**Form name:** ____________ | **URL:** ____________

| Check | Status | Notes |
|-------|--------|-------|
| All inputs have visible labels (not just placeholder) | | |
| Labels positioned above inputs | | |
| Required fields clearly marked | | |
| `autocomplete` on all relevant inputs | | |
| `type` attribute appropriate | | |
| Font size ≥ 16px on inputs | | |
| Fields grouped logically with `<fieldset>` | | |
| Validation on blur (not every keystroke) | | |
| Error messages: specific + solution | | |
| `aria-invalid` on invalid inputs | | |
| `aria-describedby` linking to error messages | | |
| Error icon + color + text (not color alone) | | |
| Error summary at page top after submit failure | | |
| Focus moved to error summary | | |
| Submit button: loading state on submission | | |
| Submit button: disabled during submission | | |
| Success state clearly communicated | | |
| Data not lost on back-navigation (multi-step) | | |

---

## 6. Content Audit Template

**Purpose:** Assess quality of all user-facing copy

| Page / Component | Readability | Tone Match | Accuracy | Missing | Action |
|-----------------|-------------|------------|----------|---------|--------|
| Homepage hero | | | | | |
| Product descriptions | | | | | |
| Error messages | | | | | |
| Form labels/hints | | | | | |
| Navigation labels | | | | | |
| CTAs | | | | | |
| Email notifications | | | | | |
| 404 page | | | | | |
| Success messages | | | | | |
| Empty states | | | | | |

**Rating scale:** ✅ Good | ⚠️ Needs improvement | ❌ Rewrite required

---

## 7. Heuristic Evaluation Template

**Evaluator:** ____________ | **Date:** ____________ | **Product:** ____________

| ID | Heuristic | Location | Description | Severity (0–4) | Recommendation |
|----|-----------|---------|-------------|---------------|---------------|
| H01 | H1: Visibility | | | | |
| H02 | H2: Real World | | | | |
| H03 | H3: User Control | | | | |
| H04 | H4: Consistency | | | | |
| H05 | H5: Error Prevention | | | | |
| H06 | H6: Recognition | | | | |
| H07 | H7: Flexibility | | | | |
| H08 | H8: Minimalism | | | | |
| H09 | H9: Error Recovery | | | | |
| H10 | H10: Documentation | | | | |

**Severity scale:**  
4 = Critical (task failure) | 3 = Serious | 2 = Moderate | 1 = Cosmetic | 0 = Not an issue

---

## 8. Design Handoff Checklist

For designers handing off to developers:

### Design Specifications
- [ ] All screen sizes designed (mobile, tablet, desktop)
- [ ] Interactive states: default, hover, focus, active, disabled, error, loading
- [ ] All typography styles defined with tokens
- [ ] All colors defined with tokens and contrast ratios noted
- [ ] Spacing values documented (use design system tokens)
- [ ] Grid/layout specifications provided
- [ ] Animation specs: duration, easing, trigger

### Component Specs
- [ ] Component names match design system naming
- [ ] All variants documented
- [ ] Edge cases: long text, empty state, single item, max items
- [ ] Responsive behavior documented
- [ ] Motion/animation behavior documented

### Accessibility Notes
- [ ] Focus order documented for complex components
- [ ] ARIA roles and attributes specified
- [ ] Screen reader announcements documented
- [ ] Color contrast ratios verified and noted
- [ ] Touch target sizes specified (minimum 44px)

### Assets
- [ ] Icons exported as SVG
- [ ] Images provided in correct formats (WebP + fallback)
- [ ] Multiple resolutions for responsive images
- [ ] Alt text written for all images
- [ ] Design file organized with consistent naming

---

## Sources & Further Reading

| Resource | URL |
|----------|-----|
| WCAG Quick Reference | https://www.w3.org/WAI/WCAG22/quickref/ |
| Lighthouse | https://developer.chrome.com/docs/lighthouse/ |
| PageSpeed Insights | https://pagespeed.web.dev/ |
| axe DevTools | https://www.deque.com/axe/ |
| WebAIM Checklist | https://webaim.org/standards/wcag/checklist |
| A11y Project Checklist | https://www.a11yproject.com/checklist/ |
| Baymard UX Benchmarks | https://baymard.com/ux-benchmark |
| NNGroup UX Standards | https://www.nngroup.com/articles/standards-guidelines/ |

---

*Last verified: November 2026*

---

[< Testing & Research](../09-testing-research/README.md) | [< Back to Knowledge Map](../../README.md)
