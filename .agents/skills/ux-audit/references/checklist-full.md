# Full UX Audit Checklist — 10 Aspects

Use this reference when running the ux-audit skill.
Score each item: ✅ Pass | ⚠️ Needs Work | ❌ Fail | ➖ N/A

---

## Aspect 1 — Navigation & IA
- [ ] 1.1 Clear knowledge/site map on homepage
- [ ] 1.2 All sections visible in index/table
- [ ] 1.3 Quick-start or role-based guides
- [ ] 1.4 Back/breadcrumb navigation between nested pages
- [ ] 1.5 Cross-references between related sections
- [ ] 1.6 Table of Contents in every file/page

## Aspect 2 — Visual Design
- [ ] 2.1 Consistent Markdown/CSS formatting throughout
- [ ] 2.2 Tables used for 3+ item comparisons
- [ ] 2.3 ✅/❌ annotations in code examples
- [ ] 2.4 Heading hierarchy H1→H2→H3 (no skipped levels)
- [ ] 2.5 Visual accents (icons, badges) used sparingly
- [ ] 2.6 Line/cell lengths readable on mobile

## Aspect 3 — Accessibility (WCAG 2.2 AA)
- [ ] 3.1 All img/image examples have alt text
- [ ] 3.2 ARIA attributes used correctly
- [ ] 3.3 Keyboard navigation patterns present
- [ ] 3.4 prefers-reduced-motion in CSS examples
- [ ] 3.5 Color contrast ≥ 4.5:1 in CSS examples
- [ ] 3.6 Screen reader patterns (aria-live, sr-only) shown

## Aspect 4 — Mobile & Responsive
- [ ] 4.1 Mobile-first CSS approach demonstrated
- [ ] 4.2 Touch target ≥44px rules stated
- [ ] 4.3 iOS safe area insets shown
- [ ] 4.4 Container Queries mentioned
- [ ] 4.5 PWA manifest example present
- [ ] 4.6 Specific mobile testing tools listed

## Aspect 5 — Performance UX
- [ ] 5.1 Core Web Vitals table with Good/Poor thresholds
- [ ] 5.2 Image optimization pipeline with code
- [ ] 5.3 Modern JS APIs (scheduler.yield, etc.)
- [ ] 5.4 CSS animations: transform/opacity only
- [ ] 5.5 Real User Monitoring (RUM) example
- [ ] 5.6 Measurement tools listed

## Aspect 6 — Forms & Inputs
- [ ] 6.1 Single-column layout justified with research
- [ ] 6.2 All inputmode types listed with examples
- [ ] 6.3 autocomplete attributes (WCAG 1.3.5)
- [ ] 6.4 Password show/hide toggle pattern
- [ ] 6.5 File upload (accessible drag & drop)
- [ ] 6.6 Session timeout handling (WCAG 2.2.1)

## Aspect 7 — Content & UX Writing
- [ ] 7.1 Jargon→plain language replacement table
- [ ] 7.2 Error message formula (What/Why/How/Tone)
- [ ] 7.3 Empty state formula (Icon+Context+Value+CTA)
- [ ] 7.4 Inclusive language table
- [ ] 7.5 Intl API for date/number formatting
- [ ] 7.6 Tone spectrum (casual→formal) shown

## Aspect 8 — Testing & Research
- [ ] 8.1 Research methods matrix
- [ ] 8.2 Usability testing session script template
- [ ] 8.3 Severity scale (0–4) defined
- [ ] 8.4 Bad vs good task examples
- [ ] 8.5 A/B test documentation template
- [ ] 8.6 Research report template

## Aspect 9 — Sources & Documentation Quality
- [ ] 9.1 All links point to authoritative sources
- [ ] 9.2 Sources table in every section
- [ ] 9.3 Books cited with author name
- [ ] 9.4 Link verification date present
- [ ] 9.5 CI link-checking in place
- [ ] 9.6 WCAG links reference correct version (2.2)

## Aspect 10 — Checklists & Audit Coverage
- [ ] 10.1 Pre-launch checklist (50+ items)
- [ ] 10.2 WCAG 2.2 audit template (all 50 criteria)
- [ ] 10.3 Performance audit template
- [ ] 10.4 Mobile audit (iOS + Android columns)
- [ ] 10.5 Design handoff checklist
- [ ] 10.6 Heuristic evaluation template

---

## Scoring Guide
- 90–100%: PASS ✅ — Production ready
- 75–89%:  GOOD ✅ — Publish with minor fixes
- 60–74%:  NEEDS WORK ⚠️ — Fix before launch
- < 60%:   FAIL ❌ — Major rework required
