# Contributing to the UX Knowledge Base

Thank you for considering a contribution! This knowledge base is a community effort to maintain a high-quality, up-to-date reference for UX practitioners and web developers.

---

## How to Contribute

### 1. Reporting Issues
If you find outdated information, broken links, or incorrect guidelines:

1. Open a **GitHub Issue** with the label `outdated` or `incorrect`
2. Include:
   - Which file and section is affected
   - What is incorrect or outdated
   - A link to the authoritative source with the correct information

### 2. Suggesting New Content
To propose a new section or sub-topic:

1. Open an Issue with the label `enhancement`
2. Describe:
   - What topic to add
   - Why it belongs in this knowledge base
   - Suggested section placement
   - At least 2 authoritative sources

### 3. Submitting a Pull Request

**Step-by-step:**

```bash
# 1. Fork the repository on GitHub

# 2. Clone your fork
git clone https://github.com/YOUR-USERNAME/ux-knowledge-base.git

# 3. Create a feature branch
git checkout -b add/motion-design-guidelines
# or
git checkout -b fix/wcag-contrast-ratios

# 4. Make your changes following the style guide below

# 5. Commit with a descriptive message
git commit -m "docs(a11y): add ARIA live region examples for dynamic content"

# 6. Push and open a Pull Request
git push origin add/motion-design-guidelines
```

---

## Content Style Guide

### Document Structure
Every new document must follow this template:

```markdown
# [Section Number] — [Section Title]

> **[One-sentence summary of what this section covers.]**

---

## Table of Contents
1. [Section Name](#anchor)
...

---

## 1. Section Name

**Source:** [Author/Org](URL) | [Second Source](URL)

[Content with explanation]

### Subsection
[Detail]

```code examples```

---

## Checklist
- [ ] Checklist item

---

## Sources & Further Reading
| Resource | URL |
|----------|-----|
| Name | URL |
```

### Writing Standards
- **Target reading level:** Grade 6–8 (Flesch-Kincaid)
- **Voice:** Active, second person ("you")
- **Length:** Be thorough but not padded — every sentence should earn its place
- **Code examples:** Every guideline should have a ✅ good and ❌ bad example where possible
- **Sources:** Only cite authoritative sources:
  - W3C specifications (WCAG, ARIA, HTML Living Standard)
  - Nielsen Norman Group
  - MDN Web Docs
  - Google web.dev / developer.chrome.com
  - Apple Human Interface Guidelines
  - Material Design
  - Baymard Institute
  - Published books from recognized experts
  - Major platform design systems (Material, Apple HIG, Fluent)

### Markdown Formatting
- One blank line between sections
- Use `**bold**` for key terms (first mention only)
- Use ` ``` ` for all code blocks with language specified
- Tables for comparisons of 3+ items
- Use ✅ / ❌ prefix in code comments to indicate good/bad examples

---

## Commit Message Format

```
type(scope): short description

Types: docs, fix, feat, chore
Scope: a11y, visual, forms, nav, mobile, perf, content, testing, checklist

Examples:
docs(a11y): add keyboard navigation patterns for modal dialogs
fix(perf): correct CLS formula and threshold values
feat(forms): add multi-step form progress indicator pattern
```

---

## Code of Conduct

- Be respectful and constructive in all feedback
- Back up suggested changes with authoritative sources
- Acknowledge that standards evolve — provide version/date context
- Welcome contributors of all experience levels

---

## Questions?

Open a GitHub Discussion or Issue. We're happy to help!
