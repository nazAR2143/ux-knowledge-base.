# 08 — Content & UX Writing

> **UX writing is the practice of designing the words users encounter in digital products. Good UX writing reduces support tickets, increases conversion, and builds user confidence.**

---

## Table of Contents
1. [UX Writing Principles](#1-ux-writing-principles)
2. [Plain Language Guidelines](#2-plain-language-guidelines)
3. [Microcopy Patterns](#3-microcopy-patterns)
4. [Error Messages](#4-error-messages)
5. [Empty States](#5-empty-states)
6. [Onboarding Copy](#6-onboarding-copy)
7. [Button & CTA Labels](#7-button--cta-labels)
8. [Tone & Voice](#8-tone--voice)
9. [Inclusive Language](#9-inclusive-language)
10. [Internationalization (i18n) Basics](#10-internationalization-i18n-basics)
11. [Checklist](#checklist)
12. [Sources & Further Reading](#sources--further-reading)

---

## 1. UX Writing Principles

**Source:** [Google UX Writing Fundamentals](https://uxwriting.google/) | [Microsoft Writing Style Guide](https://learn.microsoft.com/en-us/style-guide/welcome/)

### The 3 Core Principles

| Principle | Meaning | Example |
|-----------|---------|---------|
| **Clear** | No jargon; users understand it instantly | "Save" not "Persist changes" |
| **Concise** | Use as few words as needed | "Delete" not "Click here to delete this item" |
| **Useful** | Helps users complete tasks | "Invalid email" ❌ vs "Enter a valid email (name@example.com)" ✅ |

### Writing for Cognition
- **Front-load key information** — first 11 characters visible in most UI patterns
- **Use active voice** — "You can download the file" not "The file can be downloaded"
- **Present tense** — "Your password is saved" not "Your password will be saved"
- **Second person ("you")** — Conversational; builds rapport
- **Avoid double negatives** — "Only admins can edit" not "Non-admins cannot edit"

---

## 2. Plain Language Guidelines

**Source:** [PlainLanguage.gov](https://www.plainlanguage.gov/) | [Hemingway App](https://hemingwayapp.com/)

### Reading Level Target
- **Target:** Grade 6–8 reading level (Flesch-Kincaid)
- **Tool:** [Hemingway Editor](https://hemingwayapp.com/) for readability analysis
- **Why:** Even expert users prefer simpler language under cognitive load

### Word Choices

| ❌ Avoid | ✅ Use Instead |
|---------|--------------|
| Utilize | Use |
| Commence | Start |
| Terminate | End / Stop |
| Endeavour | Try |
| In order to | To |
| At this point in time | Now |
| Prior to | Before |
| Subsequent to | After |
| In the event that | If |
| Facilitate | Help |
| Leverage | Use |
| Navigate to | Go to |
| Populate the field | Fill in |

### Sentence Structure
```
❌ Long sentence:
"In order to ensure that your account information is properly synchronized 
across all of your devices, you will need to enable the synchronization 
feature in the settings panel before proceeding."

✅ Revised:
"To sync your account across devices:
1. Open Settings
2. Turn on Sync"
```

### Scannable Content Structure
- **Headers:** Every major section gets a header (use proper H2, H3 hierarchy)
- **Bullet lists:** 3–7 items; parallel structure
- **Short paragraphs:** 1–3 sentences maximum in UI; 3–5 for help docs
- **Bold key terms:** Not for decoration — for scanability
- **Tables:** For comparison of 3+ items with 3+ attributes

---

## 3. Microcopy Patterns

**Source:** [Microcopy: Discover How Tiny Words Make Huge Impact](https://www.microcopybook.com/) — Kinneret Yifrah

### Form Hints
```
Label:   Email address
Hint:    We'll send your receipt here. No spam, unsubscribe anytime.
Input:   [________________________]

Label:   Phone number (optional)
Hint:    For delivery updates only
Input:   [________________________]
```

### Empty Form Fields vs. Defaults
```html
<!-- ✅ Hint text that disappears on focus — set as placeholder -->
<input type="text" placeholder="e.g. John Smith">

<!-- ✅ For amounts — use the most common default -->
<input type="number" value="1" min="1" max="99">

<!-- ✅ For dates — default to reasonable future date -->
<input type="date" value="2025-01-15">
```

### Tooltips & Help Text
```
📋 Tooltip example:
[ ? ] ← hover/focus this icon

Tooltip content:
"CVV is the 3-digit code on the back of your card.
American Express cards have a 4-digit code on the front."
```

**Tooltip rules:**
- Max 1–2 sentences
- Triggered by hover AND focus (keyboard accessible)
- Never put critical info only in tooltips
- Use `role="tooltip"` and `aria-describedby`

### Confirmation Messages
```
✅ Good confirmations:
After saving:    "Changes saved"           (brief, positive)
After deleting:  "Post deleted. Undo"      (reversible action shown)
After sending:   "Email sent to john@example.com"  (confirms the action)
After signup:    "Welcome! Check your email to confirm your account."

❌ Bad confirmations:
"Operation completed successfully"   (Jargon + vague)
"Done!"                              (Too terse — what's done?)
"Your data has been persisted."      (Technical jargon)
```

---

## 4. Error Messages

**Source:** [NNGroup Error Message Guidelines](https://www.nngroup.com/articles/error-message-guidelines/)

### The 4-Part Error Formula
1. **What happened** — State the problem clearly
2. **Why it happened** — Brief explanation (if helpful)
3. **How to fix it** — Actionable next step
4. **Tone** — Neutral, never blaming

```
❌ Bad:    "Invalid input"
❌ Bad:    "Error 422: Validation failed"
❌ Bad:    "You entered the wrong password!"
❌ Bad:    "INCORRECT EMAIL ADDRESS"

✅ Good:   "The email address you entered isn't valid.
            Please use the format: name@example.com"

✅ Good:   "Incorrect password.
            Forgot your password? Reset it here →"

✅ Good:   "We couldn't process your payment.
            Please check your card details and try again, or use a different payment method."
```

### System Errors (500, Network, etc.)
```
❌ "An unexpected error has occurred."

✅ "Something went wrong on our end.
    We're working to fix it. Please try again in a few minutes.
    [Try again]  [Go to homepage]"
```

### 404 Pages
```
✅ 404 page elements:
1. Acknowledge the problem without blame
2. Offer search
3. Suggest popular pages or categories
4. Provide a path home

Example:
"We can't find that page.
It might have been moved or deleted.

[Search: ____________ ]

Popular pages:
• Products
• Help Center
• Contact Us

← Back to homepage"
```

---

## 5. Empty States

**Source:** [NNGroup Empty States](https://www.nngroup.com/articles/empty-state-mobile-app-design/)

An empty state appears when there's no data to display. It's an opportunity — not dead space.

### Empty State Formula
```
[Illustration or Icon]
     [What is empty]
  [Why it matters / Value proposition]
       [CTA to fill it]
```

### Examples by Context

**First-time empty state (onboarding):**
```
📋 Your task list is empty

Stay organized — add your first task to get started.

[+ Add Task]
```

**Search/filter empty state:**
```
🔍 No results for "macbok pro"

Did you mean "MacBook Pro"? →

Or try:
• Using fewer keywords
• Checking your spelling
• Browsing all products →
```

**Error empty state:**
```
⚠ Couldn't load your messages

Check your connection and try again.

[Try Again]
```

---

## 6. Onboarding Copy

**Source:** [NNGroup Onboarding UX](https://www.nngroup.com/articles/mobile-onboarding/)

### Onboarding Principles
- **Value-first:** Explain what users GET, not what they DO
- **Progressive:** Reveal information as it becomes relevant
- **Skippable:** Always allow skipping; don't force reading
- **Action-oriented:** Every step ends with an action, not just information

```
❌ Feature-focused:
"Our app uses AI-powered machine learning algorithms to analyze your 
spending patterns and generate comprehensive financial reports."

✅ Benefit-focused:
"See exactly where your money goes — in seconds.

Connect your bank (takes 2 minutes) and we'll show you a breakdown 
of your spending, automatically categorized."

[Connect Bank]        [I'll do this later]
```

### Permission Requests
Request permissions **in context**, just before you need them:
```
❌ Ask on first launch: "Allow notifications?" [Yes/No]

✅ Ask at relevant moment:
"Get notified when your package ships?

[📦 Turn on shipping alerts]    [Not now]
```

---

## 7. Button & CTA Labels

**Source:** [NNGroup Button Labels](https://www.nngroup.com/articles/ok-cancel-or-cancel-ok/)

### Button Label Rules
- **Verb + noun pattern:** "Save changes", "Create account", "Delete post"
- **Be specific:** "Get started" ❌ → "Create free account" ✅
- **Match user's mental model:** "Buy now" (e-commerce) vs "Subscribe" (SaaS)
- **Avoid vague labels:** "OK", "Yes/No", "Submit", "Click here"
- **Primary action first:** Most important action on the left or top

```
❌ Vague:
[OK]    [Cancel]

✅ Specific:
[Delete account]    [Keep my account]

✅ For destructive confirmation:
[Delete]    [Cancel]
           ↑ default/focused
```

### Button Hierarchy in UI
```
Page has ONE primary action:
[Primary CTA]       ← Filled, brand color
[Secondary action]  ← Outlined or ghost
[Tertiary/link]     ← Text link style

Example:
[Save changes]   [Preview]   Discard changes
```

### CTA Copy Optimization
```
❌ Generic:          ✅ Specific:
"Submit"            "Send my application"
"Sign up"           "Create free account"
"Learn more"        "See pricing"
"Get started"       "Start 14-day free trial"
"Download"          "Download for Mac (Free)"
"Buy now"           "Add to cart – $29"
```

---

## 8. Tone & Voice

**Source:** [Mailchimp Content Style Guide](https://styleguide.mailchimp.com/) | [GOV.UK Content Design](https://www.gov.uk/guidance/content-design)

### Voice vs. Tone
- **Voice:** Your brand's consistent personality (doesn't change)
- **Tone:** Adapts to context (like how you speak to friends vs. a funeral)

| Situation | Tone | Example |
|-----------|------|---------|
| Success state | Warm, celebratory | "You're all set! 🎉" |
| Error state | Calm, helpful | "Something went wrong — let's fix it." |
| Onboarding | Encouraging, clear | "You're almost there." |
| Dangerous action | Serious, direct | "Deleting your account is permanent." |
| Empty state | Friendly, motivating | "No tasks yet — add your first one!" |

### Tone Spectrum
```
Too casual ←————————————————→ Too formal
"Oopsie daisy!" | "Oops, that didn't work" | "An error has occurred."
                              ↑ Sweet spot for most products
```

---

## 9. Inclusive Language

**Source:** [Microsoft Inclusive Design](https://inclusive.microsoft.design/) | [APA Inclusive Language](https://apastyle.apa.org/style-grammar-guidelines/bias-free-language)

| ❌ Avoid | ✅ Use Instead | Reason |
|---------|--------------|--------|
| "guys" | "everyone", "folks", "team" | Gender-neutral |
| "blacklist/whitelist" | "blocklist/allowlist" | Racial connotation |
| "master/slave" | "primary/replica", "leader/follower" | Racial connotation |
| "crazy", "insane" | "unexpected", "wild", "remarkable" | Mental health stigma |
| "simple", "easy" | (avoid entirely) | Implies others are incompetent |
| "crippled" | "limited", "restricted" | Ableist |
| "dummy" | "sample", "placeholder", "example" | — |
| "sanity check" | "quick check", "review" | Mental health stigma |
| "normal users" | "users", "people" | Implies others are abnormal |

### Age-Inclusive Language
- Don't assume: "tap on your smartphone" → "click or tap"
- Don't reference age: "even your grandma can use it" ❌
- Instructions work for all device types

---

## 10. Internationalization (i18n) Basics

**Source:** [W3C i18n Activity](https://www.w3.org/International/) | [Google i18n Guide](https://developers.google.com/international/)

```html
<!-- ✅ Declare language on html element -->
<html lang="en">
<html lang="uk">   <!-- Ukrainian -->
<html lang="de">   <!-- German -->

<!-- ✅ Language change within content -->
<p>See our <span lang="fr">à la carte</span> menu.</p>
```

### Content Expansion Budget
When translating English, budget for text expansion:

| Language | Expansion vs. English |
|----------|----------------------|
| German | +35% |
| Finnish | +40% |
| Arabic | -25% (but RTL!) |
| French | +20% |
| Japanese | -50% (but needs more space due to CJK) |

```css
/* ✅ Design for text expansion */
.btn {
  /* Don't use fixed widths — allow content to determine size */
  width: auto;
  min-width: 100px;
  padding: var(--space-3) var(--space-6);
  white-space: nowrap; /* or allow wrapping with text-wrap: balance */
}
```

### Date, Time, Number Formats
```javascript
// ✅ Always use Intl API — never hard-code formats
const date = new Date();

// Date formatting
new Intl.DateTimeFormat('uk-UA').format(date);  // 09.11.2026 (Ukrainian)
new Intl.DateTimeFormat('en-US').format(date);  // 11/9/2026 (US)
new Intl.DateTimeFormat('de-DE').format(date);  // 9.11.2026 (German)

// Number/currency formatting
new Intl.NumberFormat('uk-UA', { style: 'currency', currency: 'UAH' }).format(1234.5);
// ₴ 1 234,50

new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(1234.5);
// $1,234.50
```

---

## Checklist

- [ ] All copy passes Flesch-Kincaid grade 6–8 readability test
- [ ] Active voice used throughout
- [ ] No jargon or technical terms in user-facing copy
- [ ] Button labels follow Verb + Noun pattern
- [ ] No vague CTAs ("Submit", "OK", "Click here")
- [ ] Error messages: specific, polite, explain the fix
- [ ] Empty states have context, value prop, and CTA
- [ ] Onboarding copy is benefit-focused, not feature-focused
- [ ] Inclusive language used (no "guys", no ableist terms)
- [ ] All confirmation messages specify what was confirmed
- [ ] Permission requests contextual and in-moment
- [ ] Dates/currencies use `Intl` API (not hard-coded formats)
- [ ] `lang` attribute set on `<html>` element
- [ ] UI designed with text expansion budget (German +35%)

---

## Sources & Further Reading

| Resource | URL |
|----------|-----|
| Google UX Writing Fundamentals | https://uxwriting.google/ |
| Microsoft Writing Style Guide | https://learn.microsoft.com/en-us/style-guide/welcome/ |
| Mailchimp Content Style Guide | https://styleguide.mailchimp.com/ |
| GOV.UK Content Design Guide | https://www.gov.uk/guidance/content-design |
| PlainLanguage.gov | https://www.plainlanguage.gov/ |
| NNGroup Error Messages | https://www.nngroup.com/articles/error-message-guidelines/ |
| NNGroup Empty States | https://www.nngroup.com/articles/empty-state-mobile-app-design/ |
| Hemingway Editor | https://hemingwayapp.com/ |
| W3C Internationalization | https://www.w3.org/International/ |
| Inclusive Design (Microsoft) | https://inclusive.microsoft.design/ |
| Microcopy Book | https://www.microcopybook.com/ |

---

*Last verified: November 2026*

---

[< Forms & Inputs](../07-forms-inputs/README.md) | [< Back to Knowledge Map](../../README.md) | [Next: Testing & Research >](../09-testing-research/README.md)
