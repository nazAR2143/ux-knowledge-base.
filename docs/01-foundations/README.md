# 01 — UX Foundations: Core Principles & Psychology

> **This section covers the fundamental principles that underpin all good UX design, including cognitive psychology, usability heuristics, and mental models.**

---

## Table of Contents
1. [Nielsen's 10 Usability Heuristics](#1-nielsens-10-usability-heuristics)
2. [Cognitive Load Theory](#2-cognitive-load-theory)
3. [Gestalt Principles](#3-gestalt-principles)
4. [Mental Models](#4-mental-models)
5. [Laws of UX (Psychology)](#5-laws-of-ux-psychology)
6. [The 3-Click Rule & Beyond](#6-the-3-click-rule--beyond)
7. [Hick's Law & Decision Making](#7-hicks-law--decision-making)
8. [Checklist](#checklist)
9. [Sources & Further Reading](#sources--further-reading)

---

## 1. Nielsen's 10 Usability Heuristics

**Source:** [Nielsen Norman Group](https://www.nngroup.com/articles/ten-usability-heuristics/) — Jakob Nielsen, 1994 (updated 2020)

These 10 general principles describe properties of usable interfaces. They are called "heuristics" because they are broad rules of thumb, not specific guidelines.

### H1 — Visibility of System Status
> Always keep users informed about what is going on through appropriate feedback within reasonable time.

**Implementation:**
- Show loading spinners/progress bars for operations > 1 second
- Highlight active navigation items
- Display confirmation messages after form submissions
- Use breadcrumbs to show location within the site

```html
<!-- ✅ Good: Clear loading state -->
<button aria-busy="true" disabled>
  <span class="spinner" aria-hidden="true"></span>
  Saving...
</button>

<!-- ❌ Bad: No feedback -->
<button onclick="saveData()">Save</button>
```

---

### H2 — Match Between System and Real World
> Use words, phrases, and concepts familiar to the user, rather than system-oriented terms.

**Implementation:**
- Use plain language (see [Content Writing](../08-content-writing/README.md))
- Use familiar icons (shopping cart, not "purchase container")
- Order information naturally (e.g., date formats matching user locale)
- Avoid technical jargon in user-facing copy

```html
<!-- ✅ Good: Real-world language -->
<label>Your email address</label>

<!-- ❌ Bad: System-oriented language -->
<label>User identifier (email format, RFC 5321)</label>
```

---

### H3 — User Control and Freedom
> Users often choose system functions by mistake and need a clearly marked "emergency exit".

**Implementation:**
- Provide Undo/Redo functionality
- Allow easy cancellation of multi-step processes
- Confirm destructive actions (delete, overwrite)
- Use confirmation dialogs, not auto-delete

```html
<!-- ✅ Good: Reversible action with undo -->
<div role="alert" class="toast">
  Item deleted. 
  <button onclick="undoDelete()">Undo</button>
</div>
```

---

### H4 — Consistency and Standards
> Users should not have to wonder whether different words, situations, or actions mean the same thing.

**Implementation:**
- Follow platform conventions (e.g., blue underlined = link)
- Keep button labels consistent site-wide ("Submit" vs. "Send" vs. "Go")
- Use a design system or component library
- Align with [Jakob's Law](https://lawsofux.com/jakobs-law/): users spend most time on other sites

---

### H5 — Error Prevention
> Even better than good error messages is a careful design that prevents a problem from occurring.

**Implementation:**
- Validate input as user types (inline validation)
- Provide constraints (date pickers instead of free text)
- Warn before irreversible actions
- Use smart defaults

```html
<!-- ✅ Good: Constrained input prevents errors -->
<input type="date" min="2024-01-01" max="2030-12-31">

<!-- ✅ Good: Confirmation before destructive action -->
<button 
  onclick="confirm('Delete account? This cannot be undone.') && deleteAccount()"
  class="btn-danger">
  Delete Account
</button>
```

---

### H6 — Recognition Over Recall
> Minimize the user's memory load by making objects, actions, and options visible.

**Implementation:**
- Show recently viewed items
- Provide autocomplete suggestions
- Display visible labels (not just placeholder text)
- Keep menus visible, not hidden in hamburgers when possible

---

### H7 — Flexibility and Efficiency of Use
> Accelerators — unseen by novice users — may speed up interaction for expert users.

**Implementation:**
- Keyboard shortcuts for power users
- Saved preferences and templates
- Bulk actions in admin interfaces
- Advanced search/filter options

---

### H8 — Aesthetic and Minimalist Design
> Dialogues should not contain irrelevant or rarely needed information.

**Implementation:**
- Remove unnecessary content
- One primary CTA per screen
- Progressive disclosure for complex information
- White space is functional, not wasted

---

### H9 — Help Users Recognize, Diagnose, and Recover from Errors
> Error messages should be expressed in plain language, precisely indicate the problem, and constructively suggest a solution.

**Implementation:**
```html
<!-- ✅ Good error message -->
<p class="error" role="alert">
  ❌ The email address you entered isn't valid. 
  Please use the format: name@example.com
</p>

<!-- ❌ Bad error message -->
<p class="error">Error 422: Validation failed on field[2]</p>
```

---

### H10 — Help and Documentation
> Even though it's better if the system can be used without documentation, it may be necessary to provide help.

**Implementation:**
- Contextual help tooltips
- Inline hints and examples
- Searchable FAQ/documentation
- Progressive onboarding

---

## 2. Cognitive Load Theory

**Source:** [John Sweller, 1988](https://doi.org/10.1207/s15516709cog1202_4) | [NNGroup: Minimize Cognitive Load](https://www.nngroup.com/articles/minimize-cognitive-load/)

**Types of Cognitive Load:**

| Type | Description | UX Strategy |
|------|-------------|-------------|
| **Intrinsic** | Complexity inherent to the task | Chunk information, progressive disclosure |
| **Extraneous** | Load caused by poor design | Simplify layouts, remove noise |
| **Germane** | Load that creates learning/schemas | Consistent patterns, clear metaphors |

**Reduction Techniques:**
- **Chunking:** Group related items (max 7±2 items per group — Miller's Law)
- **Progressive Disclosure:** Show only what's needed; reveal more on demand
- **Defaults:** Pre-fill smart defaults to reduce decision fatigue
- **Visual Hierarchy:** Guide attention with size, weight, contrast

---

## 3. Gestalt Principles

**Source:** [Gestalt Psychology](https://www.interaction-design.org/literature/topics/gestalt-principles)

| Principle | Description | UI Application |
|-----------|-------------|----------------|
| **Proximity** | Elements close together appear related | Group form fields, card layouts |
| **Similarity** | Similar elements appear related | Consistent button styles, link colors |
| **Continuity** | Eye follows smooth paths | Line animations, visual flow |
| **Closure** | Mind completes incomplete shapes | Progress rings, skeleton loaders |
| **Figure/Ground** | Foreground vs. background distinction | Modals, tooltips, z-index usage |
| **Common Fate** | Elements moving together are related | Coordinated animations |
| **Prägnanz** | Mind perceives simplest form | Simple icon design, clean layouts |

---

## 4. Mental Models

**Source:** [NNGroup: Mental Models](https://www.nngroup.com/articles/mental-models/)

> A mental model is an explanation of someone's thought process about how something works in the real world.

**Key Applications:**
- Match your UI to users' existing mental models (e.g., shopping cart = real cart)
- When breaking mental models, provide clear onboarding
- Research mental models through user interviews and card sorting
- Use familiar metaphors (desktop, files, folders, trash)

---

## 5. Laws of UX (Psychology)

**Source:** [Laws of UX by Jon Yablonski](https://lawsofux.com/)

| Law | Summary | Application |
|-----|---------|-------------|
| **Fitts's Law** | Time to target ∝ distance/size | Large touch targets, nearby related actions |
| **Hick's Law** | Decision time ∝ number of choices | Limit menu items, use progressive disclosure |
| **Jakob's Law** | Users prefer familiar conventions | Follow platform standards |
| **Miller's Law** | People can hold 7±2 items in working memory | Chunk content in groups of 5–9 |
| **Doherty Threshold** | Productivity increases when < 400ms response | Optimize performance, use loading states |
| **Zeigarnik Effect** | People remember uncompleted tasks better | Progress bars, save progress features |
| **Von Restorff Effect** | Distinctive items are better remembered | Highlight primary CTA, use contrast |
| **Peak–End Rule** | We judge experiences by their peak and end | Celebrate success states, smooth offboarding |
| **Aesthetic–Usability Effect** | Beautiful design is perceived as more usable | Invest in visual polish |
| **Tesler's Law** | Every application has an irreducible complexity | Don't oversimplify; push complexity to developers |

---

## 6. The 3-Click Rule & Beyond

**Source:** [NNGroup: 3-Click Rule Debunked](https://www.nngroup.com/articles/3-click-rule/)

The "3-click rule" (all content reachable in 3 clicks) is a **myth** — research shows click *count* matters less than:
- **Clarity:** Users know what to click at each step
- **Progress:** Users feel they're moving toward their goal
- **Confidence:** Users aren't lost or confused

**Better metric:** **Task completion rate** and **time on task**

---

## 7. Hick's Law & Decision Making

**Formula:** $RT = b \cdot \log_2(n + 1)$

Where *RT* = reaction time, *b* = empirical constant, *n* = number of choices.

**Practical rules:**
- Navigation: **5–7 primary items** maximum
- Forms: Use multi-step wizards for > 7 fields
- Product pages: Highlight 1 recommended option
- Pricing: Maximum 3–4 plans

---

## Checklist

- [ ] All interactions provide system status feedback
- [ ] Language matches user's vocabulary (not technical jargon)
- [ ] Destructive actions are reversible or confirmed
- [ ] Error messages are specific, human-readable, and suggest solutions
- [ ] Primary navigation has ≤ 7 items
- [ ] Forms use progressive disclosure for complex tasks
- [ ] Consistent patterns used throughout the interface
- [ ] Cognitive load minimized with chunking and visual hierarchy

---

## Sources & Further Reading

| Resource | URL | Author / Organization |
|----------|-----|----------------------|
| 10 Usability Heuristics | https://www.nngroup.com/articles/ten-usability-heuristics/ | Nielsen Norman Group |
| Laws of UX | https://lawsofux.com/ | Jon Yablonski |
| Cognitive Load Theory | https://www.nngroup.com/articles/minimize-cognitive-load/ | Nielsen Norman Group |
| Gestalt Principles in UX | https://www.interaction-design.org/literature/topics/gestalt-principles | Interaction Design Foundation |
| Mental Models | https://www.nngroup.com/articles/mental-models/ | Nielsen Norman Group |
| Don't Make Me Think | https://www.amazon.com/Dont-Make-Think-Revisited-Usability/dp/0321965515 | Steve Krug (Book) |
| The Design of Everyday Things | https://www.amazon.com/Design-Everyday-Things-Revised-Expanded/dp/0465050654 | Don Norman (Book) |

---

*Last verified: November 2026*

---

[← Back to Knowledge Map](../../README.md) | [Next: Visual Design →](../02-visual-design/README.md)
