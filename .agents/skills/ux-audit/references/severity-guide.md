# Severity Guide for UX Audit Bug Registry

## Severity Scale (0–4)

| Level | Label | Symbol | Definition | Action |
|-------|-------|--------|------------|--------|
| 4 | Critical | 🔴 | Task failure or legal compliance violation (e.g., WCAG fail blocking access) | Fix immediately — block launch |
| 3 | Serious | 🔴 | Major friction, significant percentage of users affected, significant business impact | Fix before launch (Sprint 1) |
| 2 | Moderate | 🟡 | Noticeable problem but users can recover; reduces satisfaction or efficiency | Fix within 1 week of launch (Sprint 2) |
| 1 | Minor | 🟢 | Small friction, easy to work around, low user impact | Fix when capacity allows (Backlog) |
| 0 | Cosmetic | ⚪ | Visual or polish issue only; no functional impact | Fix if time allows |

## Bug Registry Format

```markdown
| ID | Severity | Description | Location | Recommended Fix |
|----|---------|-------------|----------|----------------|
| ERR-001 | 🔴 Critical (4) | No keyboard access to main dropdown | nav/header.html | Add keydown handler for Enter/Space/Arrow keys |
| ERR-002 | 🔴 Serious (3) | Form error messages not announced to screen readers | forms/signup.html | Add role="alert" and aria-live="assertive" |
| ERR-003 | 🟡 Moderate (2) | Search box missing role="search" | search/index.html | Add role="search" to <form> wrapper |
| ERR-004 | 🟢 Minor (1) | Visited link color same as unvisited | global/styles.css | Add :visited { color: #7c3aed } |
| ERR-005 | ⚪ Cosmetic (0) | Footer logo slightly misaligned on 1440px | footer.html | Adjust margin-right by 2px |
```

## Sprint Assignment Rules

| Severity | Sprint |
|---------|--------|
| 4 — Critical | Sprint 1 (before launch, blocker) |
| 3 — Serious | Sprint 1 (before launch) |
| 2 — Moderate | Sprint 2 (1 week post-launch) |
| 1 — Minor | Backlog |
| 0 — Cosmetic | Backlog (low priority) |

## Verdict Thresholds

| Score | Verdict |
|-------|---------|
| ≥ 90% and 0 Critical bugs | ✅ PASS — Production ready |
| 75–89% or any Serious bugs | ✅ GOOD — Publish with fixes planned |
| 60–74% | ⚠️ NEEDS WORK — Fix before launch |
| Any Critical (4) bugs | ❌ BLOCKED — Must fix before any release |
| < 60% | ❌ FAIL — Major rework required |
