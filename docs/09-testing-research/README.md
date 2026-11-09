# 09 — Usability Testing & User Research

> **Testing with 5 users finds 85% of usability problems. Research is not a phase — it is a continuous practice that runs throughout the product lifecycle.**

---

## Table of Contents
1. [Research Methods Overview](#1-research-methods-overview)
2. [Usability Testing](#2-usability-testing)
3. [Moderated vs. Unmoderated Testing](#3-moderated-vs-unmoderated-testing)
4. [User Interviews](#4-user-interviews)
5. [Surveys & Questionnaires](#5-surveys--questionnaires)
6. [Analytics & Quantitative Data](#6-analytics--quantitative-data)
7. [A/B Testing](#7-ab-testing)
8. [Card Sorting & Tree Testing](#8-card-sorting--tree-testing)
9. [Heuristic Evaluation](#9-heuristic-evaluation)
10. [Synthesis & Reporting](#10-synthesis--reporting)
11. [Checklist](#checklist)
12. [Sources & Further Reading](#sources--further-reading)

---

## 1. Research Methods Overview

**Source:** [NNGroup UX Research Methods](https://www.nngroup.com/articles/which-ux-research-methods/) | [IDEO Design Thinking](https://designthinking.ideo.com/)

### The Research Landscape

```
                    BEHAVIORAL (What people DO)
                              ↑
                    ┌─────────────────────┐
   QUALITATIVE      │  Usability testing  │  QUANTITATIVE
   (Why/How)   ←────│  Eye tracking       │────→ (What/How many)
                    │  Diary studies      │
                    └─────────────────────┘
                              │
            ┌─────────────────┼─────────────────┐
            ↓                 ↓                 ↓
     Interviews          A/B testing        Surveys
     (qualitative,       (quantitative,     (can be both,
     attitudinal)        behavioral)        attitudinal)
                              ↓
                    ATTITUDINAL (What people SAY)
```

### Research Method Selection Guide

| Question Type | Best Methods |
|--------------|-------------|
| "What problems exist?" | Usability testing, analytics, interviews |
| "Why does this problem occur?" | Interviews, diary studies, contextual inquiry |
| "Which design is better?" | A/B testing, preference testing |
| "How do users categorize content?" | Card sorting, tree testing |
| "What do users think of us?" | Surveys, NPS, CSAT |
| "Where do users struggle?" | Session recordings, eye tracking, funnel analysis |

### When to Use Research

| Project Phase | Recommended Research |
|--------------|---------------------|
| Discovery | User interviews, competitive analysis |
| Define | Affinity mapping, personas, journey mapping |
| Design | Paper prototyping, concept testing |
| Prototype | Usability testing (moderated) |
| Development | Unmoderated testing, accessibility audit |
| Launch | A/B testing, analytics monitoring |
| Post-launch | Longitudinal studies, NPS, support analysis |

---

## 2. Usability Testing

**Source:** [Steve Krug: Rocket Surgery Made Easy](https://www.sensible.com/rsme.html) | [NNGroup Usability Testing](https://www.nngroup.com/articles/usability-testing-101/)

### The Basics
- **Minimum participants:** 5 per user group (finds ~85% of issues)
- **Session length:** 60 minutes maximum (cognitive fatigue)
- **Task completion:** 3–5 tasks per session
- **Think-aloud protocol:** Ask participants to narrate their thoughts

### Recruiting Participants
```
Screening criteria example (e-commerce site):
✓ Age 25–55
✓ Has made an online purchase in the last 3 months
✓ Uses a smartphone at least once per day
✗ Works in UX, marketing, or web design (too biased)
✗ Has used our product before (can test separately)
```

**Recruiting tools:**
- [UserTesting.com](https://www.usertesting.com/) — On-demand participants
- [Respondent.io](https://www.respondent.io/) — B2B and professional participants
- [Prolific.com](https://www.prolific.com/) — Academic and consumer research

### Writing Test Tasks

| ❌ Bad Task | ✅ Good Task |
|-----------|------------|
| "Find the checkout page" | "You've decided to buy the blue running shoes in size 10. Complete the purchase." |
| "Use the search feature" | "Find out if there's a coffee shop near the Eiffel Tower that opens before 8am." |
| "Navigate to Account Settings" | "You've moved to a new address. Update your address in your account." |

**Task writing rules:**
1. Scenario-based (give them context)
2. Goal-oriented (don't mention the UI)
3. Realistic (users would actually do this)
4. No hints about WHERE to do the task
5. Avoid jargon from the UI

### Session Script Template
```markdown
## Intro (5 min)
"Thank you for joining. I'm going to ask you to complete 
some tasks on this website. There are no right or wrong answers — 
we're testing the website, not you.

Please think aloud as you work — narrate what you're seeing 
and what you're thinking.

Do you have any questions before we start?"

## Task 1 (10–15 min)
"[Read task scenario]. Please begin when you're ready."

Observer notes:
- Did they complete the task? Y/N
- Time on task: ___
- Errors/struggles: 
- Verbatim quotes:

## Debrief (5 min)
"What was your overall impression?"
"What was most confusing?"
"What worked well?"
"Is there anything you'd change?"
```

### Severity Rating Scale
| Rating | Description | Action |
|--------|-------------|--------|
| **4 — Critical** | Task failure; major business impact | Fix before launch |
| **3 — Serious** | Major difficulty; slows users significantly | Fix in next sprint |
| **2 — Moderate** | Annoying but users can recover | Fix in backlog |
| **1 — Minor** | Slight friction; easy to overlook | Nice to fix |
| **0 — Cosmetic** | Polish issue | Fix if time allows |

---

## 3. Moderated vs. Unmoderated Testing

**Source:** [NNGroup Moderated vs. Unmoderated](https://www.nngroup.com/articles/moderated-unmoderated-usability-testing/)

| Factor | Moderated | Unmoderated |
|--------|-----------|-------------|
| **Cost** | High | Low |
| **Speed** | Slow (1–2 weeks) | Fast (hours) |
| **Participants** | 5–8 | 20–50 |
| **Rich insights** | ✅ Deep "why" | ❌ Shallow |
| **Follow-up questions** | ✅ Yes | ❌ No |
| **Complex tasks** | ✅ Suitable | ❌ Limited |
| **Geographic reach** | Limited | ✅ Global |
| **Best for** | Early designs, complex flows | Validation, remote |

**Remote moderated tools:**
- [Lookback.io](https://www.lookback.io/)
- [UserZoom](https://www.userzoom.com/)
- Zoom + screen share

**Unmoderated tools:**
- [UserTesting.com](https://www.usertesting.com/)
- [Maze](https://maze.co/)
- [Useberry](https://www.useberry.com/)

---

## 4. User Interviews

**Source:** [NNGroup User Interviews](https://www.nngroup.com/articles/user-interviews/) | [Interviewing Users (Portigal)](https://rosenfeldmedia.com/books/interviewing-users/)

### Interview Types
| Type | Focus | Duration |
|------|-------|----------|
| **Generative** | Discover needs, behaviors, pain points | 45–60 min |
| **Evaluative** | Assess a specific design or concept | 30–45 min |
| **Contextual inquiry** | Observe in natural environment | 60–90 min |

### Question Framework

**Opening (Warm-up):**
- "Tell me about your role / typical day"
- "Walk me through the last time you [relevant task]"

**Core questions (behavior-focused):**
- "Tell me about the last time you [task]" ← Past behavior, not hypothetical
- "What was going through your mind when...?"
- "What would you do next?"
- "Can you show me how you'd normally do that?"

**Probes (follow-up):**
- "Tell me more about that"
- "What do you mean by [term]?"
- "What happened next?"
- "How did that make you feel?"

**❌ Questions to avoid:**
```
❌ "Would you use a feature like X?" — Hypothetical; people say yes to everything
❌ "Do you like this design?" — Primes positive response
❌ "Is this easy to use?" — Leading question
❌ "Don't you think it would be better if..." — Leading question
```

### Interview Analysis
1. **Record with consent** (video/audio)
2. **Transcribe** key sections
3. **Affinity mapping:** Cluster observations into themes
4. **Quote bank:** Save verbatim quotes as evidence
5. **Journey mapping:** Map the experience timeline

---

## 5. Surveys & Questionnaires

**Source:** [SurveyMonkey UX Research](https://www.surveymonkey.com/mp/user-experience-research/) | [Google Forms](https://forms.google.com)

### Key UX Metrics via Survey

**Net Promoter Score (NPS):**
```
"How likely are you to recommend [product] to a friend or colleague?"
0 (Not at all likely) ←————————→ 10 (Extremely likely)

Scoring:
0–6:  Detractors
7–8:  Passives
9–10: Promoters

NPS = % Promoters - % Detractors
Benchmark: > 50 = excellent; > 70 = exceptional
```

**System Usability Scale (SUS):**
10 questions, 5-point Likert scale — standardized, validated measure.
Score ≥ 68 = above average. [SUS Scale](https://www.usability.gov/how-to-and-tools/methods/system-usability-scale.html)

**Customer Satisfaction (CSAT):**
```
"How satisfied are you with [specific interaction]?"
⭐⭐⭐⭐⭐ (1–5 stars or 1–10 scale)
```

### Survey Design Rules
1. **Maximum 10 questions** for unsolicited surveys
2. **One concept per question** — no "and/or" questions
3. **Randomize answer options** to avoid order bias
4. **Use balanced scales:** Agree/Disagree (not Agree/Somewhat agree/Agree strongly)
5. **Open-ended last:** Cognitive fatigue; closed questions first
6. **Test your survey** — Have 3 colleagues complete before sending

---

## 6. Analytics & Quantitative Data

**Source:** [Google Analytics 4](https://analytics.google.com/) | [Hotjar](https://www.hotjar.com/) | [Microsoft Clarity](https://clarity.microsoft.com/)

### Key UX Metrics to Track

| Metric | Formula | Target |
|--------|---------|--------|
| Task Completion Rate | Completed ÷ Attempted × 100 | ≥ 78% |
| Error Rate | Errors ÷ Total attempts | ≤ 5% |
| Time on Task | Average time per task | Context-dependent |
| Conversion Rate | Conversions ÷ Visitors | Baseline + improvements |
| Bounce Rate | Single-page sessions ÷ Total | Varies by content type |
| Funnel Drop-off | Sessions lost at each step | Identify biggest drop |

### Session Recording Analysis
```
Tools: Hotjar, Microsoft Clarity, FullStory, LogRocket

Look for:
✓ Rage clicks (clicking same area repeatedly — confusion)
✓ Dead clicks (clicking non-interactive elements)
✓ U-turns (going forward then immediately back)
✓ Excessive scrolling (looking for something)
✓ Form field abandonment (which fields cause drop-off)
```

### Funnel Analysis
```
Example checkout funnel:
Step 1: Product page        → 100%
Step 2: Add to cart         → 42%   (-58%)
Step 3: Cart review         → 38%   (-4%)   ← Small drop, cart UX is fine
Step 4: Shipping info       → 28%   (-10%)  ← Problem: form too complex?
Step 5: Payment             → 24%   (-4%)
Step 6: Order confirmation  → 20%   (-4%)

Action: Investigate step 2 (product→cart) and step 4 (shipping form)
```

---

## 7. A/B Testing

**Source:** [Google Optimize Help](https://support.google.com/optimize) | [VWO A/B Testing](https://vwo.com/ab-testing/)

### When to A/B Test
✅ When you have enough traffic (minimum ~1,000 conversions/variant/week)
✅ When you have a clear hypothesis
✅ When you're measuring a specific metric
❌ Not for major redesigns (too many variables)
❌ Not when traffic is too low (underpowered test)

### Statistical Significance
- Minimum **95% confidence** before declaring a winner
- Run for **at least 2 full business cycles** (usually 2 weeks minimum)
- Use a [sample size calculator](https://www.optimizely.com/sample-size-calculator/)

### A/B Test Documentation Template
```markdown
## Test: [Name]

**Hypothesis:** 
Changing [element] from [A] to [B] will increase [metric] 
because [reason based on research/data].

**Control (A):** [Description + screenshot]
**Variant (B):** [Description + screenshot]

**Primary metric:** Checkout completion rate
**Secondary metrics:** Time to purchase, cart abandonment

**Sample size needed:** 2,400 per variant (95% confidence, 10% MDE)
**Expected runtime:** 14 days

**Result:**
- Control: 23.4% conversion
- Variant: 26.1% conversion (+11.5% relative)
- Confidence: 97.3% ✅
- Decision: Implement variant
```

---

## 8. Card Sorting & Tree Testing

Covered in detail in [Navigation & IA](../04-navigation-ia/README.md#1-information-architecture-principles).

**Quick reference:**
- **Open card sort:** Discover categories — use at beginning of IA work
- **Closed card sort:** Validate categories — use to confirm existing structure
- **Tree test:** Test navigation — use after card sort to validate the full tree

**Tools:** [Optimal Workshop](https://www.optimalworkshop.com/), [Maze](https://maze.co/)

---

## 9. Heuristic Evaluation

**Source:** [NNGroup Heuristic Evaluation](https://www.nngroup.com/articles/how-to-conduct-a-heuristic-evaluation/)

Evaluate an interface against Nielsen's 10 heuristics (see [UX Foundations](../01-foundations/README.md#1-nielsens-10-usability-heuristics)) with 3–5 evaluators.

### Process
1. **Brief evaluators** on the product, users, and task scenarios
2. **Independent evaluation** — each evaluator works alone first
3. **Document issues** — which heuristic violated, description, severity
4. **Consolidate** — combine all issues, remove duplicates
5. **Prioritize** — sort by severity rating

### Documentation Format
```markdown
| ID | Heuristic | Description | Severity | Screenshot |
|----|-----------|-------------|----------|-----------|
| H01 | H9: Error Recovery | Error on payment page says "Failed" with no explanation or next step | 4 — Critical | [link] |
| H02 | H6: Recognition | Search results have no way to filter or sort — user must remember criteria | 3 — Serious | [link] |
| H03 | H1: Visibility | No loading indicator when searching — user doesn't know if action registered | 3 — Serious | [link] |
```

---

## 10. Synthesis & Reporting

### Research Report Structure
```markdown
# Research Report: [Study Name]
**Date:** [Date] | **Researcher:** [Name] | **Method:** [Method]

## Executive Summary (1 page)
- 3–5 key findings as bullets
- Top priority recommendations

## Methodology
- Method used and why
- Participants (n=X, demographics)
- Tasks/questions used

## Key Findings
### Finding 1: [Clear headline]
- Evidence: [Quotes, data, screenshots]
- Impact: [Business/user impact]
- Recommendation: [Actionable next step]

## Affinity Map / Themes
[Screenshot of clustering exercise]

## Recommendations (prioritized)
| Priority | Recommendation | Effort | Impact |
|----------|---------------|--------|--------|
| 1 | Fix error messages on checkout | Low | High |

## Appendix
- Full session recordings/transcripts
- Survey data
- Participant demographics
```

---

## Checklist

- [ ] Research method matches the question type (behavioral vs. attitudinal)
- [ ] Usability tests use realistic, scenario-based tasks
- [ ] Tasks don't mention UI elements (not leading)
- [ ] Minimum 5 participants per user group
- [ ] Think-aloud protocol used in moderated sessions
- [ ] Sessions recorded (with participant consent)
- [ ] Severity rating applied to all issues found
- [ ] Interview questions behavior-focused (past events, not hypotheticals)
- [ ] Survey ≤ 10 questions; closed before open-ended
- [ ] A/B tests run to 95%+ statistical significance
- [ ] A/B tests run for minimum 2 weeks / 2 business cycles
- [ ] Analytics funnel analysis performed for key flows
- [ ] Session recordings reviewed for rage clicks and dead clicks
- [ ] Research findings shared in actionable report format
- [ ] Research findings linked to design decisions in documentation

---

## Sources & Further Reading

| Resource | URL |
|----------|-----|
| NNGroup Research Methods | https://www.nngroup.com/articles/which-ux-research-methods/ |
| NNGroup Usability Testing 101 | https://www.nngroup.com/articles/usability-testing-101/ |
| Steve Krug: Rocket Surgery Made Easy | https://www.sensible.com/rsme.html |
| System Usability Scale (SUS) | https://www.usability.gov/how-to-and-tools/methods/system-usability-scale.html |
| Hotjar | https://www.hotjar.com/ |
| Microsoft Clarity (Free) | https://clarity.microsoft.com/ |
| Maze (Prototype Testing) | https://maze.co/ |
| Optimal Workshop (Card Sorting) | https://www.optimalworkshop.com/ |
| Optimizely Sample Size Calculator | https://www.optimizely.com/sample-size-calculator/ |
| Interviewing Users (book) | https://rosenfeldmedia.com/books/interviewing-users/ |

---

*Last verified: November 2026*

---

[< Content & Writing](../08-content-writing/README.md) | [< Back to Knowledge Map](../../README.md) | [Next: Checklists >](../10-checklists/README.md)
