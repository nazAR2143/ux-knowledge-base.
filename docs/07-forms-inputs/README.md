# 07 — Forms & Input Design

> **Forms are where users give you their most valuable data — and where most abandonment happens. Good form design reduces friction, prevents errors, and builds trust.**

---

## Table of Contents
1. [Form Layout Principles](#1-form-layout-principles)
2. [Labels & Placeholders](#2-labels--placeholders)
3. [Input Types & Attributes](#3-input-types--attributes)
4. [Validation & Error Handling](#4-validation--error-handling)
5. [Multi-Step Forms](#5-multi-step-forms)
6. [Password Fields](#6-password-fields)
7. [Autocomplete & Autofill](#7-autocomplete--autofill)
8. [File Uploads](#8-file-uploads)
9. [Form Accessibility Summary](#9-form-accessibility-summary)
10. [Checklist](#checklist)
11. [Sources & Further Reading](#sources--further-reading)

---

## 1. Form Layout Principles

**Source:** [NNGroup Form Design](https://www.nngroup.com/articles/web-form-design/) | [Luke Wroblewski: Web Form Design](https://www.lukew.com/resources/web_form_design.asp)

### Single-Column Layout
```
✅ Single column (best):        ❌ Two columns (avoid):
┌──────────────────────┐       ┌──────────┐ ┌──────────┐
│ First name           │       │ First    │ │ Last     │
│ [____________]       │       │ [______] │ │ [______] │
│ Last name            │       │ Email    │ │ Phone    │
│ [____________]       │       │ [______] │ │ [______] │
│ Email                │       └──────────┘ └──────────┘
│ [____________]       │
└──────────────────────┘
```

**Research finding:** Single-column forms are completed **15.4 seconds faster** than multi-column (Baymard Institute).

**Exceptions where 2 columns are acceptable:**
- Short related fields side-by-side: First Name | Last Name
- Address fields: City | State | ZIP
- Credit card: Number | Expiry | CVV

### Field Ordering
Follow the natural mental model and conversation flow:
1. Identity (name, email)
2. Contact (phone, address)
3. Account security (password)
4. Payment (last — builds trust first)

### Group Related Fields
```html
<fieldset>
  <legend>Shipping address</legend>
  <div class="form-group">
    <label for="street">Street address</label>
    <input type="text" id="street" name="street" autocomplete="street-address">
  </div>
  <div class="form-row">
    <div class="form-group">
      <label for="city">City</label>
      <input type="text" id="city" name="city" autocomplete="address-level2">
    </div>
    <div class="form-group form-group--sm">
      <label for="zip">ZIP code</label>
      <input type="text" id="zip" name="postal-code" inputmode="numeric" 
             pattern="[0-9]{5}" autocomplete="postal-code">
    </div>
  </div>
</fieldset>
```

---

## 2. Labels & Placeholders

**Source:** [NNGroup Placeholders](https://www.nngroup.com/articles/form-design-placeholders/) | [WebAIM: Labels](https://webaim.org/techniques/forms/controls)

### Label Placement
| Position | Completion Time | Eye Tracking |
|----------|----------------|-------------|
| **Top of field** ✅ | Fastest | Best — 2 fixations |
| Left-aligned left | Moderate | Okay — good for scannable forms |
| Right-aligned left | Slower | Harder — mismatched reading flow |
| Inside field (placeholder) | ❌ Worst | Disappears on focus |

```css
/* ✅ Top-aligned label (recommended) */
.form-group {
  display: flex;
  flex-direction: column;
  gap: var(--space-1);
}

label {
  font-weight: 500;
  font-size: var(--text-sm);
  color: var(--color-text);
}

input {
  padding: var(--space-3) var(--space-4);
  border: 2px solid var(--color-border);
  border-radius: 6px;
  font-size: var(--text-base);  /* ≥ 16px to prevent iOS zoom */
  transition: border-color 150ms ease;
}

input:focus {
  outline: none;
  border-color: var(--color-primary);
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.15);
}
```

### Placeholder Rules
```html
<!-- ✅ Placeholder as EXAMPLE, not label -->
<label for="email">Email address</label>
<input type="email" id="email" placeholder="name@company.com">

<!-- ✅ Required field indication -->
<label for="name">
  Full name
  <span class="required" aria-hidden="true">*</span>
  <span class="sr-only">(required)</span>
</label>
<input type="text" id="name" required aria-required="true">

<!-- Note at form top -->
<p class="form-note">Fields marked with <span aria-hidden="true">*</span> are required.</p>

<!-- ❌ Placeholder as label replacement — NEVER -->
<input type="email" placeholder="Enter your email address">
```

---

## 3. Input Types & Attributes

**Source:** [MDN Input Types](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input) | [HTML Living Standard](https://html.spec.whatwg.org/multipage/input.html)

### Use Semantic Input Types
```html
<!-- Mobile keyboards adapt to input type! -->
<input type="email">      <!-- @ key on mobile keyboard -->
<input type="tel">        <!-- Number pad on mobile -->
<input type="number">     <!-- Number pad -->
<input type="url">        <!-- .com key on mobile -->
<input type="search">     <!-- Search return key -->
<input type="date">       <!-- Date picker -->
<input type="time">       <!-- Time picker -->
<input type="color">      <!-- Color picker -->
<input type="range">      <!-- Slider -->
<input type="file">       <!-- File picker -->
<input type="password">   <!-- Hidden characters -->
<input type="checkbox">   <!-- Multiple choice -->
<input type="radio">      <!-- Single choice -->
```

### inputmode — Fine-tune Mobile Keyboard
```html
<!-- Use inputmode for semantic control of keyboard type -->
<input type="text" inputmode="numeric">   <!-- Numbers without input validation -->
<input type="text" inputmode="decimal">   <!-- Decimal keyboard (prices) -->
<input type="text" inputmode="tel">       <!-- Phone keyboard -->
<input type="text" inputmode="email">     <!-- Email keyboard -->
<input type="text" inputmode="url">       <!-- URL keyboard -->
<input type="text" inputmode="search">    <!-- Search keyboard with Search button -->
<input type="text" inputmode="none">      <!-- No keyboard (custom keyboard) -->
```

### Essential Input Attributes
```html
<input 
  type="text"
  id="full-name"
  name="full-name"
  autocomplete="name"           <!-- Enables browser autofill -->
  autocapitalize="words"        <!-- Mobile: capitalize each word -->
  spellcheck="false"            <!-- For names/codes -->
  aria-required="true"          <!-- For AT -->
  required                      <!-- HTML5 validation -->
  minlength="2"
  maxlength="100"
  aria-describedby="name-hint"> <!-- Points to hint text -->
<p id="name-hint" class="form-hint">Use your legal name as it appears on ID.</p>
```

---

## 4. Validation & Error Handling

**Source:** [NNGroup Error Messages](https://www.nngroup.com/articles/error-message-guidelines/) | [Baymard Form Validation](https://baymard.com/blog/inline-form-validation)

### When to Validate

| Strategy | Timing | Best For |
|----------|--------|----------|
| **On blur** (after leaving field) | After user finishes | Most fields |
| **On input** (while typing) | Real-time | Password strength, length limits |
| **On submit** | After submit click | Final catch-all |
| **Inline on success** | After valid input | Email availability, username |

```javascript
// ✅ Validate on blur, not on every keystroke (except special cases)
input.addEventListener('blur', () => {
  validateField(input);
});

// ✅ For password strength — real-time is appropriate
passwordInput.addEventListener('input', () => {
  updatePasswordStrength(passwordInput.value);
});
```

### Error Message Pattern
```html
<!-- ✅ WCAG-compliant error display -->
<div class="form-group has-error">
  <label for="email">Email address</label>
  <input 
    type="email" 
    id="email"
    value="john@"
    aria-invalid="true"
    aria-describedby="email-error email-hint">
  
  <!-- Error message: specific + solution -->
  <p id="email-error" class="field-error" role="alert">
    <span aria-hidden="true">⚠</span>
    Please enter a complete email address (e.g., name@example.com).
  </p>
  
  <p id="email-hint" class="form-hint">We'll send your confirmation here.</p>
</div>
```

```css
.field-error {
  color: var(--color-error);
  font-size: var(--text-sm);
  margin-top: var(--space-1);
  display: flex;
  align-items: center;
  gap: var(--space-1);
}

input[aria-invalid="true"] {
  border-color: var(--color-error);
  /* ✅ Not only color — also icon in background */
  background-image: url("data:image/svg+xml,...");
  background-repeat: no-repeat;
  background-position: right var(--space-3) center;
  padding-right: var(--space-10);
}
```

### Error Summary (Multi-Field Forms)
```html
<!-- ✅ Show summary at top AND inline errors -->
<div 
  id="error-summary" 
  role="alert" 
  aria-live="assertive"
  class="error-summary"
  tabindex="-1">
  <h2>Please fix 3 errors to continue:</h2>
  <ul>
    <li><a href="#email">Email: Please enter a valid email address.</a></li>
    <li><a href="#password">Password: Must be at least 8 characters.</a></li>
    <li><a href="#phone">Phone: Format should be +1 (555) 000-0000.</a></li>
  </ul>
</div>
```

```javascript
// Move focus to error summary after failed submission
document.getElementById('error-summary').focus();
```

### Error Message Writing Rules
1. **Be specific:** "Email is invalid" ❌ → "Enter a valid email (name@example.com)" ✅
2. **Don't blame the user:** "You failed to..." ❌ → "Please check..." ✅
3. **Explain what to do:** Not just what went wrong
4. **Plain language:** No error codes, no technical terms
5. **Be polite:** No exclamation marks, no CAPS

---

## 5. Multi-Step Forms

**Source:** [NNGroup Multi-Step Forms](https://www.nngroup.com/articles/wizard-design-pattern/)

```html
<!-- ✅ Progress indicator -->
<nav aria-label="Form progress">
  <ol class="step-indicator">
    <li class="step step--complete" aria-label="Step 1: Personal info, completed">
      <span class="step-number" aria-hidden="true">✓</span>
      Personal Info
    </li>
    <li class="step step--active" aria-label="Step 2: Shipping address, current step">
      <span class="step-number" aria-hidden="true">2</span>
      Shipping
    </li>
    <li class="step" aria-label="Step 3: Payment, not started">
      <span class="step-number" aria-hidden="true">3</span>
      Payment
    </li>
  </ol>
</nav>

<form>
  <h1>Step 2 of 3: Shipping Address</h1>
  <!-- form fields -->
  <div class="form-actions">
    <button type="button" onclick="previousStep()">← Back</button>
    <button type="submit">Continue →</button>
  </div>
</form>
```

**Multi-step best practices:**
- Persist data between steps (don't lose input on back navigation)
- Show step count ("Step 2 of 3")
- Allow going back to previous steps
- Save progress for long forms

---

## 6. Password Fields

```html
<div class="form-group">
  <label for="password">Password</label>
  
  <div class="password-wrapper">
    <input 
      type="password" 
      id="password"
      name="new-password"
      autocomplete="new-password"
      aria-describedby="pwd-strength pwd-requirements"
      minlength="8"
      required>
    
    <!-- Show/hide toggle -->
    <button 
      type="button" 
      class="password-toggle"
      aria-pressed="false"
      aria-label="Show password"
      onclick="togglePassword(this)">
      <svg aria-hidden="true"><!-- eye icon --></svg>
    </button>
  </div>
  
  <!-- Strength indicator -->
  <div id="pwd-strength" aria-live="polite" class="strength-meter">
    <div class="strength-bar" data-strength="2"></div>
    <span>Password strength: Fair</span>
  </div>
  
  <!-- Requirements -->
  <ul id="pwd-requirements" class="requirements-list">
    <li id="req-length" aria-label="8 characters: not met">✗ At least 8 characters</li>
    <li id="req-number" aria-label="One number: not met">✗ Contains a number</li>
    <li id="req-upper" aria-label="Uppercase letter: not met">✗ Contains uppercase</li>
  </ul>
</div>
```

---

## 7. Autocomplete & Autofill

**Source:** [MDN Autocomplete Attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/autocomplete) | [WCAG 1.3.5](https://www.w3.org/WAI/WCAG22/Understanding/identify-input-purpose)

Using correct autocomplete values is **required by WCAG 1.3.5** and improves conversion significantly:

```html
<!-- Identity -->
<input autocomplete="name">
<input autocomplete="given-name">
<input autocomplete="family-name">
<input autocomplete="email">
<input autocomplete="tel">

<!-- Address -->
<input autocomplete="street-address">
<input autocomplete="address-level2">  <!-- City -->
<input autocomplete="address-level1">  <!-- State -->
<input autocomplete="postal-code">
<input autocomplete="country">

<!-- Payment -->
<input autocomplete="cc-name">
<input autocomplete="cc-number">
<input autocomplete="cc-exp">
<input autocomplete="cc-csc">

<!-- Authentication -->
<input autocomplete="username">
<input autocomplete="current-password">
<input autocomplete="new-password">
<input autocomplete="one-time-code">   <!-- OTP SMS code -->
```

---

## 8. File Uploads

```html
<!-- ✅ Accessible file upload with drag-and-drop -->
<div class="file-upload">
  <label for="file-input" class="file-label">
    <div class="drop-zone" role="button" tabindex="0" 
         aria-label="Upload file — drag and drop or click to browse"
         ondragover="highlight(this)" ondrop="handleDrop(event, this)">
      <svg aria-hidden="true"><!-- upload icon --></svg>
      <p>Drag & drop files here, or <strong>browse</strong></p>
      <p class="file-hint">Accepted: PDF, PNG, JPG — Max 10MB per file</p>
    </div>
  </label>
  <input 
    type="file" 
    id="file-input"
    name="documents"
    accept=".pdf,.png,.jpg,.jpeg"
    multiple
    class="sr-only"
    aria-describedby="file-constraints"
    onchange="handleFiles(this.files)">
  <p id="file-constraints" class="form-hint">Maximum 5 files, 10MB each.</p>
</div>
```

---

## 9. Form Accessibility Summary

| Requirement | Implementation | WCAG |
|------------|---------------|------|
| Labels for all inputs | `<label for="id">` | 1.3.1 |
| Error identification | `aria-invalid="true"` + error message | 3.3.1 |
| Error description | `aria-describedby` pointing to error | 3.3.1 |
| Error suggestion | Error message explains fix | 3.3.3 |
| Required fields marked | `required` + `aria-required` + visual indicator | 3.3.2 |
| Input purpose | `autocomplete` attributes | 1.3.5 |
| No timeout (or extendable) | Session extension warning | 2.2.1 |
| Redundant entry prevented | Don't re-ask previously entered data | 3.3.7 |

---

## Checklist

- [ ] All inputs have visible top-aligned labels (not just placeholder)
- [ ] Required fields clearly indicated (asterisk + legend explaining it)
- [ ] Appropriate input `type` used (email, tel, number, etc.)
- [ ] `inputmode` set for numeric/decimal fields
- [ ] `autocomplete` attributes on all relevant fields
- [ ] Font size ≥ 16px on inputs (prevents iOS auto-zoom)
- [ ] Validation on blur (not on every keystroke for most fields)
- [ ] Error messages: specific, polite, explain the solution
- [ ] `aria-invalid="true"` set on invalid inputs
- [ ] Error summary at top of form after failed submission
- [ ] Focus moved to error summary after submission failure
- [ ] Error icon + color + text (not color alone)
- [ ] Multi-step forms show progress and allow going back
- [ ] Password show/hide toggle present
- [ ] Submit button disabled during submission with loading state
- [ ] Success state clearly communicated after submission

---

## Sources & Further Reading

| Resource | URL |
|----------|-----|
| NNGroup Form Design (book) | https://www.nngroup.com/articles/web-form-design/ |
| NNGroup Placeholders | https://www.nngroup.com/articles/form-design-placeholders/ |
| Baymard Inline Validation | https://baymard.com/blog/inline-form-validation |
| MDN Input Types | https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input |
| MDN Autocomplete | https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/autocomplete |
| WCAG 1.3.5 Input Purpose | https://www.w3.org/WAI/WCAG22/Understanding/identify-input-purpose |
| Luke W: Web Form Design | https://www.lukew.com/resources/web_form_design.asp |
| WebAIM Form Labels | https://webaim.org/techniques/forms/controls |

---

*Last verified: November 2026*

---

[< Performance UX](../06-performance-ux/README.md) | [< Back to Knowledge Map](../../README.md) | [Next: Content & Writing >](../08-content-writing/README.md)
