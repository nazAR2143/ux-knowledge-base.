---
name: ux-audit
description: >-
  Use this skill when the user asks to run a UX audit, accessibility check,
  or quality review on a website or web project. Activated by phrases like
  "run a UX audit", "check accessibility", "audit this site", "перевір UX",
  "зроби аудит". Performs a full structured audit across 10 UX aspects:
  Navigation, Visual Design, Accessibility (WCAG 2.2), Mobile, Performance,
  Forms, Content, Testing, Sources, and Checklists. Produces a severity-rated
  report with persona, user journey, findings, and prioritized fixes.
---

# UX Audit Skill

This skill performs a comprehensive UX audit on a web project or repository.
It generates a structured report covering 10 aspects, with a user persona,
journey map, checklist results, and prioritized bug registry.

---

## When to Activate

Activate when the user says any of:
- "run a UX audit on [site/project]"
- "audit the UX of [project]"
- "check accessibility of [site]"
- "перевір UX сайту"
- "зроби UX аудит"
- "run the checklist on [project]"

---

## Step-by-Step Audit Procedure

### STEP 1 — Identify the Target

Ask or infer:
1. What is the URL or local path of the site/project to audit?
2. Who is the primary user? (role, tech level, device)
3. Any specific areas of concern? (forms, mobile, performance, a11y)

If no URL provided, audit the current workspace project's HTML/CSS/JS files.

### STEP 2 — Create the Persona

Build a persona table with:
- Name, age, role, location, experience
- Goals (3–4 items)
- Pain points (3–4 items)
- Technical level (bar chart)
- Primary device

Format as ASCII table (see [references/persona-template.md](./references/persona-template.md))

### STEP 3 — Plan the User Journey

Map 6–10 screens/pages the persona would visit, in order:
```
📍 SCREEN 1: [page name]
   ↓ Goal: [what user wants here]
   ↓ Action: [what they do]
```
Include an emotional curve at the end (★★★★★ rating per screen).

### STEP 4 — Run the 10-Aspect Checklist

For each aspect below, evaluate each criterion and assign:
- ✅ Pass | ⚠️ Needs Work | ❌ Fail | ➖ N/A

Read the full checklist from:
[references/checklist-full.md](./references/checklist-full.md)

**The 10 Aspects:**
1. Navigation & Information Architecture
2. Visual Design (typography, color, spacing)
3. Accessibility — WCAG 2.2 AA
4. Mobile & Responsive
5. Performance UX (Core Web Vitals)
6. Forms & Inputs
7. Content & UX Writing
8. Testing & Research readiness
9. Sources & Documentation quality
10. Checklists & Audit coverage

For each aspect: count Pass/Total and calculate percentage.

### STEP 5 — Build the Bug Registry

For every ⚠️ or ❌ finding, create a bug entry:

```markdown
| ID | Severity | Description | Location | Fix |
|----|---------|-------------|----------|-----|
| ERR-001 | 🔴 Serious (3) | ... | file/section | ... |
```

**Severity Scale:**
- 🔴 **4 — Critical:** Task failure or legal compliance issue
- 🔴 **3 — Serious:** Major friction, significant user impact
- 🟡 **2 — Moderate:** Noticeable issue, users can recover
- 🟢 **1 — Minor:** Small friction, cosmetic
- ⚪ **0 — Cosmetic:** Polish only

### STEP 6 — Generate the Summary Scorecard

```
┌─────────────────────────────────────────────┐
│  AUDIT SUMMARY                              │
├─────────────────────────────────────────────┤
│  Overall: XX/60 = XX%                       │
│  [Aspect table with scores]                 │
│  Critical bugs: X | Moderate: X | Minor: X  │
│  VERDICT: [PASS / NEEDS WORK / FAIL]        │
└─────────────────────────────────────────────┘
```

Verdict thresholds:
- ≥ 90%: **PASS ✅** — Ready for production
- 75–89%: **GOOD ✅** — Publish with minor fixes
- 60–74%: **NEEDS WORK ⚠️** — Fix before launch
- < 60%: **FAIL ❌** — Major rework required

### STEP 7 — Create the Sprint Plan

Organize bugs into 3 groups:
- **Sprint 1 (before launch):** All Severity 3–4 items
- **Sprint 2 (week 1 post-launch):** All Severity 2 items
- **Backlog:** All Severity 0–1 items

### STEP 8 — Output the Full Report

Write the complete report as a Markdown artifact with:
1. Header (project, date, auditor, method)
2. Persona block
3. User Journey Map
4. 10-Aspect Checklist Results (tables)
5. Bug Registry (sorted by severity)
6. Summary Scorecard
7. Sprint Plan

Save to: `[project-root]/docs/audit/UX-AUDIT-REPORT-[YYYY-MM-DD].md`
Also save to artifact directory for user viewing.

---

## Validation

After completing the audit:
- [ ] All 10 aspects have been evaluated
- [ ] Every ⚠️/❌ has a corresponding bug entry in the registry
- [ ] Bug entries have severity, location, and actionable fix
- [ ] Scorecard totals are mathematically correct
- [ ] Sprint plan covers all bugs
- [ ] Report saved to artifact directory

---

## Example Invocations

```
User: "Run a UX audit on my site at localhost:3000"
User: "Audit the UX of this project"
User: "Check accessibility of docs/index.html"
User: "Зроби UX аудит мого сайту"
User: "Перевір доступність та форми"
```

---

## References

- Full checklist: [references/checklist-full.md](./references/checklist-full.md)
- Persona template: [references/persona-template.md](./references/persona-template.md)
- Severity guide: [references/severity-guide.md](./references/severity-guide.md)
- WCAG 2.2 criteria: https://www.w3.org/WAI/WCAG22/quickref/
- Core Web Vitals: https://web.dev/vitals/
