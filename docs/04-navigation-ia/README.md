# 04 — Navigation & Information Architecture

> **Information Architecture (IA) is the structural design of shared information environments. Good navigation lets users find what they need quickly, understand where they are, and predict where links will lead.**

---

## Table of Contents
1. [Information Architecture Principles](#1-information-architecture-principles)
2. [Navigation Patterns](#2-navigation-patterns)
3. [Mega Menus](#3-mega-menus)
4. [Breadcrumbs](#4-breadcrumbs)
5. [Search UX](#5-search-ux)
6. [Pagination & Infinite Scroll](#6-pagination--infinite-scroll)
7. [Wayfinding & Orientation](#7-wayfinding--orientation)
8. [Mobile Navigation](#8-mobile-navigation)
9. [Checklist](#checklist)
10. [Sources & Further Reading](#sources--further-reading)

---

## 1. Information Architecture Principles

**Source:** [Information Architecture for the Web (Morville & Rosenfeld)](https://www.oreilly.com/library/view/information-architecture-4th/9781491913529/) | [NNGroup IA](https://www.nngroup.com/articles/ia-vs-navigation/)

### The 3 Pillars of IA
1. **Users:** Who are they? What do they need? (User research)
2. **Content:** What information exists? How much? How does it relate?
3. **Context:** Business goals, technology constraints, environment

### Card Sorting
**Purpose:** Discover how users mentally categorize your content.

| Method | When to Use | Tool |
|--------|-------------|------|
| **Open card sort** | Early discovery — categories unknown | [Optimal Workshop](https://www.optimalworkshop.com/) |
| **Closed card sort** | Validate existing categories | [Maze](https://maze.co/), [UserZoom](https://www.userzoom.com/) |
| **Tree test** | Test navigation structure | [Treejack](https://www.optimalworkshop.com/treejack/) |

### Navigation Labeling
- **Use user vocabulary,** not internal jargon (run surveys or use Google Search Console queries)
- **Be specific:** "Products" → "Men's Clothing" is better
- **Avoid clever labels:** Clarity > creativity in navigation
- **Test with 5-second test:** Can users find key sections in 5 seconds?

---

## 2. Navigation Patterns

**Source:** [NNGroup Navigation Design](https://www.nngroup.com/articles/navigation-ia-tests/) | [UI Patterns](https://ui-patterns.com/)

### Primary Navigation Comparison

| Pattern | Best For | Drawbacks |
|---------|----------|-----------|
| **Top horizontal nav** | ≤ 7 items; most websites | Limited space on mobile |
| **Left sidebar nav** | Complex apps, documentation, dashboards | Takes horizontal space |
| **Bottom tab bar** | Mobile apps (3–5 items) | Hidden on desktop |
| **Hamburger menu** | Secondary nav on mobile | Hidden — low discoverability |
| **Mega menu** | Large e-commerce, enterprise | Complexity, mobile challenges |

### Horizontal Top Navigation
```html
<header>
  <nav aria-label="Main navigation">
    <ul role="list">
      <li>
        <a href="/" aria-current="page">Home</a>
      </li>
      <li>
        <a href="/products">Products</a>
      </li>
      <li>
        <!-- Dropdown pattern -->
        <button 
          aria-expanded="false" 
          aria-haspopup="true"
          aria-controls="about-dropdown"
          id="about-btn">
          About ▾
        </button>
        <ul 
          id="about-dropdown" 
          role="menu" 
          aria-labelledby="about-btn"
          hidden>
          <li role="none"><a href="/team" role="menuitem">Team</a></li>
          <li role="none"><a href="/careers" role="menuitem">Careers</a></li>
        </ul>
      </li>
    </ul>
  </nav>
</header>
```

```css
nav ul { 
  display: flex; 
  list-style: none; 
  gap: var(--space-6); 
  margin: 0; padding: 0;
}

nav a {
  color: inherit;
  text-decoration: none;
  padding: var(--space-2) var(--space-3);
  border-radius: 4px;
}
nav a:hover, nav a:focus-visible { background: var(--color-surface-secondary); }
nav a[aria-current="page"] { font-weight: 700; border-bottom: 2px solid currentColor; }
```

---

## 3. Mega Menus

**Source:** [NNGroup Mega Menus](https://www.nngroup.com/articles/mega-menus-work-well/)

Mega menus work **when:**
- Site has ≥ 10 top-level categories
- Categories have subcategories users need to preview
- Users benefit from seeing options simultaneously (comparison)

**Best practices:**
```html
<!-- Hover + click/keyboard to open -->
<nav class="mega-nav">
  <ul>
    <li class="has-mega">
      <button 
        aria-expanded="false"
        aria-controls="categories-panel">
        Categories
      </button>
      <div 
        id="categories-panel" 
        class="mega-panel" 
        role="region"
        aria-label="Categories menu"
        hidden>
        <div class="mega-grid">
          <section>
            <h3>Electronics</h3>
            <ul>
              <li><a href="/phones">Phones</a></li>
              <li><a href="/laptops">Laptops</a></li>
            </ul>
          </section>
          <section>
            <h3>Clothing</h3>
            <ul>
              <li><a href="/mens">Men's</a></li>
            </ul>
          </section>
        </div>
      </div>
    </li>
  </ul>
</nav>
```

**Avoid:**
- Opening on hover only (inaccessible; accidental activation)
- Mega menus with > 20 items (use filters instead)
- Animated mega menus with long delays

---

## 4. Breadcrumbs

**Source:** [NNGroup Breadcrumbs](https://www.nngroup.com/articles/breadcrumb-navigation-useful/) | [Google Breadcrumbs](https://developers.google.com/search/docs/appearance/structured-data/breadcrumb)

```html
<!-- ✅ Accessible breadcrumb with structured data -->
<nav aria-label="Breadcrumb">
  <ol itemscope itemtype="https://schema.org/BreadcrumbList">
    <li itemprop="itemListElement" itemscope itemtype="https://schema.org/ListItem">
      <a href="/" itemprop="item"><span itemprop="name">Home</span></a>
      <meta itemprop="position" content="1" />
    </li>
    <li itemprop="itemListElement" itemscope itemtype="https://schema.org/ListItem">
      <a href="/products" itemprop="item"><span itemprop="name">Products</span></a>
      <meta itemprop="position" content="2" />
    </li>
    <li itemprop="itemListElement" itemscope itemtype="https://schema.org/ListItem">
      <span itemprop="name" aria-current="page">Laptop Pro X</span>
      <meta itemprop="position" content="3" />
    </li>
  </ol>
</nav>
```

```css
.breadcrumb {
  display: flex;
  flex-wrap: wrap;
  list-style: none;
  padding: 0;
  gap: var(--space-2);
}
/* Visual separator between items */
.breadcrumb li + li::before {
  content: "/";
  color: var(--color-text-secondary);
  aria-hidden: true;
}
```

**When to use breadcrumbs:**
- Site has 3+ levels of hierarchy
- Users likely arrive from search/external links (need orientation)
- E-commerce category pages, documentation, complex apps

**When NOT to use:**
- Single-level site (homepage + pages)
- Linear flows (checkout, wizard)
- Task-based flows where backtracking is undesirable

---

## 5. Search UX

**Source:** [NNGroup Search Design](https://www.nngroup.com/articles/search-not-enough/) | [Algolia UX Guide](https://www.algolia.com/doc/guides/solutions/ecommerce/search/)

### Search Box Design
```html
<form role="search" action="/search" method="get">
  <label for="site-search">Search</label>
  <input 
    type="search" 
    id="site-search"
    name="q"
    placeholder="Search products, articles..."
    autocomplete="off"
    aria-describedby="search-hint"
    spellcheck="true">
  <span id="search-hint" class="sr-only">Press Enter or click Search button</span>
  <button type="submit" aria-label="Search">
    <svg aria-hidden="true"><!-- search icon --></svg>
  </button>
</form>
```

### Autocomplete / Typeahead
```html
<input 
  type="search"
  role="combobox"
  aria-expanded="true"
  aria-autocomplete="list"
  aria-controls="search-suggestions"
  aria-activedescendant="suggestion-2">

<ul 
  id="search-suggestions" 
  role="listbox"
  aria-label="Search suggestions">
  <li id="suggestion-1" role="option">MacBook Pro</li>
  <li id="suggestion-2" role="option" aria-selected="true">MacBook Air</li>
</ul>
```

### No Results Page — Best Practices
```html
<main>
  <h1>No results for "MacBok Pro"</h1>
  <p>Did you mean: <a href="/search?q=MacBook+Pro">MacBook Pro</a>?</p>
  <h2>Try:</h2>
  <ul>
    <li>Checking your spelling</li>
    <li>Using fewer or more general keywords</li>
  </ul>
  <h2>Popular searches</h2>
  <!-- Show trending / top searches -->
</main>
```

---

## 6. Pagination & Infinite Scroll

**Source:** [NNGroup Pagination vs. Scrolling](https://www.nngroup.com/articles/item-list-view-all/)

| Pattern | Best For | Avoid When |
|---------|----------|-----------|
| **Numbered pagination** | Search results, product lists, tasks | Very long lists |
| **Load more button** | Social feeds, galleries | Users need to find specific items |
| **Infinite scroll** | Entertainment content (social, news) | Search results, goal-oriented tasks |
| **Virtualization** | Very large datasets (10,000+ rows) | Simple lists |

```html
<!-- ✅ Accessible pagination -->
<nav aria-label="Search results pages">
  <ul class="pagination">
    <li>
      <a href="?page=1" aria-label="Previous page" rel="prev">←</a>
    </li>
    <li><a href="?page=1" aria-label="Page 1">1</a></li>
    <li><a href="?page=2" aria-label="Page 2, current page" aria-current="page">2</a></li>
    <li><a href="?page=3" aria-label="Page 3">3</a></li>
    <li>
      <a href="?page=3" aria-label="Next page" rel="next">→</a>
    </li>
  </ul>
</nav>
```

---

## 7. Wayfinding & Orientation

Users need to know:
1. **Where am I?** (Active nav state, breadcrumbs, page title)
2. **Where have I been?** (Visited link styles `:visited`)
3. **Where can I go?** (Clear nav labels, related links)

```css
/* ✅ Always style visited links differently */
a:visited { color: #7c3aed; }  /* Purple is convention */

/* ✅ Current page indicator in nav */
nav a[aria-current="page"] {
  font-weight: bold;
  border-bottom: 2px solid var(--color-primary);
}
```

---

## 8. Mobile Navigation

Covered in depth in [Mobile & Responsive](../05-mobile-responsive/README.md).

**Key principles:**
- Bottom tab bar: best for 3–5 primary destinations on mobile
- Hamburger: acceptable for secondary navigation; label it ("Menu")
- Swipe gestures: supplement, never replace, visible nav controls
- Minimum touch target: 44×44px (WCAG 2.5.8)

---

## Checklist

- [ ] Navigation tested with card sorting and/or tree testing
- [ ] ≤ 7 primary navigation items
- [ ] Active/current page clearly indicated (`aria-current="page"`)
- [ ] All nav accessible via keyboard and screen reader
- [ ] Skip-to-content link present
- [ ] Breadcrumbs on pages ≥ 3 levels deep
- [ ] Breadcrumbs include structured data (Schema.org)
- [ ] Search box uses `role="search"`
- [ ] Search autocomplete accessible with ARIA combobox pattern
- [ ] No results page provides useful suggestions
- [ ] Visited links have distinct styling
- [ ] Mobile navigation tested with touch targets ≥ 44×44px
- [ ] Dropdown menus open on click/Enter (not hover-only)

---

## Sources & Further Reading

| Resource | URL |
|----------|-----|
| Information Architecture (book) | https://www.oreilly.com/library/view/information-architecture-4th/9781491913529/ |
| NNGroup: Navigation Design | https://www.nngroup.com/articles/navigation-ia-tests/ |
| NNGroup: Mega Menus | https://www.nngroup.com/articles/mega-menus-work-well/ |
| NNGroup: Breadcrumbs | https://www.nngroup.com/articles/breadcrumb-navigation-useful/ |
| Google Search Breadcrumb Schema | https://developers.google.com/search/docs/appearance/structured-data/breadcrumb |
| ARIA Disclosure Navigation Pattern | https://www.w3.org/WAI/ARIA/apg/patterns/disclosure/examples/disclosure-navigation/ |
| Optimal Workshop (card sorting) | https://www.optimalworkshop.com/ |
| NNGroup Pagination vs Scrolling | https://www.nngroup.com/articles/item-list-view-all/ |

---

*Last verified: November 2026*

---

[< Accessibility](../03-accessibility/README.md) | [< Back to Knowledge Map](../../README.md) | [Next: Mobile & Responsive >](../05-mobile-responsive/README.md)
