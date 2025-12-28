---
name: ultrathink
description: Maximum thinking capacity protocol. Used for complex architecture, deep analysis, multi-step planning, and critical decision-making.
metadata:
  skillport:
    category: thinking
    tags:
      - deep-analysis
      - critical-thinking
      - problem-solving
      - decision-making
---

# UltraThink - Deep Analysis Protocol

> This skill activates **maximum thinking capacity**.
> Provides systematic, multi-layered analysis for complex problems.

---

# 📋 Contents

1. [When to Use?](#1-when-to-use)
2. [Thinking Depth Levels](#2-thinking-depth-levels)
3. [Phase 0: Meta-Planning](#3-phase-0-meta-planning)
4. [Phase 1: Problem Understanding](#4-phase-1-problem-understanding)
5. [Phase 2: Hypothesis Generation](#5-phase-2-hypothesis-generation)
6. [Phase 3: Solution Space Exploration](#6-phase-3-solution-space-exploration)
7. [Phase 4: Critical Evaluation](#7-phase-4-critical-evaluation)
8. [Phase 5: Edge Case Matrix](#8-phase-5-edge-case-matrix)
9. [Phase 6: Self-Correction Loop](#9-phase-6-self-correction-loop)
10. [Phase 7: Synthesis and Decision](#10-phase-7-synthesis-and-decision)
11. [Chain-of-Thought Prompt](#11-chain-of-thought-prompt)
12. [Checklist](#12-checklist)
13. [Don't Checklist](#13-dont-checklist)
14. [Must-Do Checklist](#14-must-do-checklist)
15. [Thinking Tools Reference](#15-thinking-tools-reference)

---

# 1. When to Use?

| Scenario | Example |
|---------|-------|
| Architectural decisions | "Should we split the Monolith into microservices?" |
| Performance optimization | "Why is this query slow?" |
| Complex bug analysis | "Where is the race condition coming from?" |
| Multi-step refactoring | "How should we refactor these 10 files?" |
| System design | "Design a scalable auth system" |
| Trade-off evaluation | "SQL vs NoSQL: which is more suitable?" |
| Risk analysis | "What are the potential impacts of this change?" |

---

# 2. Thinking Depth Levels

Analyze the problem and determine the appropriate depth level:

| Level | Step Count | When? |
|--------|-------------|-----------|
| **Light** | 3-5 steps | Simple decision, single-dimensional problem |
| **Medium** | 8-15 steps | Multiple dependencies, medium complexity |
| **Deep** | 20-40 steps | System-wide impact, high risk |
| **Ultra** | 50+ steps | Critical architectural decision, hard to revert |

---

# 3. Phase 0: Meta-Planning

BEFORE starting any analysis, answer these questions:

```markdown
## Meta-Planning

### Problem Assessment
- **Complexity (1-10):** [Score]
- **Risk Level:** [Low/Medium/High/Critical]
- **Impact Area:** [Local/Module/System-wide]
- **Reversibility:** [Easy/Hard/Impossible]

### Socratic Reality Check (5-Step Reality Check)
Ask these 5 questions to yourself as a __reflex__ before every operation:

1. **User Intent:**
   - "What EXACTLY does the user want from me?"
   - "Is what they said and what they actually need the same?"

2. **Context:**
   - "Am I working on the correct file/location right now?"
   - "Does this operation fit the overall architecture of the project?"

3. **Action:**
   - "What am I doing right now?" (Simple and clear definition)

4. **Rationale & Alternatives:**
   - "Why am I doing it this way?"
   - "Is there a simpler or safer way?"

5. **Ripple Effect:**
   - "What could this change break?"
   - "Will it create a domino effect?"


### Success Criteria
- When is this analysis considered "sufficient"?
- Which questions must be answered?
- Minimum confidence level: [%X]
```

> [!IMPORTANT]
> **NEVER** take action without answering the **Ripple Effect** question. Calculate the domino effect.

---

# 4. Phase 1: Problem Understanding

## 4.1 Define the Problem in Your Own Words

```markdown
## Problem Definition

### Original Request
[What the user said]

### My Understanding
[Describe the problem in my own words]

### Validation Question
"Do I understand correctly: [summary]?"
```

## 4.2 Information Map

```markdown
## Information Map

### ✅ Knowns (Certain)
1. [Info 1] - Source: [how do we know?]
2. [Info 2] - Source: [how do we know?]

### ❓ Unknowns (To be investigated)
1. [Question 1] - How can we find out?
2. [Question 2] - How can we find out?

### ⚠️ Assumptions (To be validated)
1. [Assumption 1] - What happens if it's wrong?
2. [Assumption 2] - What happens if it's wrong?
```

## 4.3 Constraints and Requirements

```markdown
## Constraints

### Technical Constraints
- [Constraint 1]
- [Constraint 2]

### Business Constraints
- Time: [Duration]
- Budget: [If any]
- Resources: [Available team/tools]

### Quality Requirements
- Performance: [Metric]
- Security: [Level]
- Scalability: [Target]
```

---

# 5. Phase 2: Hypothesis Generation

## 5.1 Initial Hypotheses

```markdown
## Hypothesis List

### H1: [Hypothesis Name]
- **Description:** [What do we think it is?]
- **Confidence:** [%] 
- **Assumptions:** [What assumptions does it rely on?]
- **Test Method:** [How can we validate?]

### H2: [Hypothesis Name]
[Same format...]

### H3: [Hypothesis Name]
[Same format...]
```

## 5.2 Hypothesis Confidence Calibration

| Confidence Level | Meaning | What to do? |
|----------------|--------|-------------|
| **90-100%** | Very strong evidence | Proceed immediately |
| **70-89%** | Good evidence, small uncertainty | Proceed but monitor |
| **50-69%** | Mixed evidence | Further analysis |
| **30-49%** | Weak evidence | Search for alternatives |
| **0-29%** | Very uncertain | Rethink |

---

# 6. Phase 3: Solution Space Exploration

## 6.1 Generate at Least 3 Alternatives

```markdown
## Alternative Solutions

### Approach 1: [Name]
**Description:** [Summary]

| Criterion | Evaluation |
|--------|---------------|
| Performance | ⭐⭐⭐⭐⭐ |
| Complexity | ⭐⭐⭐ |
| Maintainability | ⭐⭐⭐⭐ |
| Implementation Time | [Time] |
| Risk | [Low/Medium/High] |

**Advantages:**
- [+] ...
- [+] ...

**Disadvantages:**
- [-] ...
- [-] ...

---

### Approach 2: [Name]
[Same format...]

---

### Approach 3: [Name]
[Same format...]
```

## 6.2 Comparison Matrix

```markdown
| Criterion | Weight | Approach 1 | Approach 2 | Approach 3 |
|-----------|--------|------------|------------|------------|
| Performance | 30% | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| Complexity | 20% | ⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐ |
| Cost | 25% | $$ | $ | $$$ |
| Risk | 25% | Low | Medium | Low |
| **TOTAL** | 100% | [Score] | [Score] | [Score] |
```

---

# 7. Phase 4: Critical Evaluation

## 7.1 Devil's Advocate

Ask these questions for every solution:

```markdown
## Critical Questions

### Weak Points
- "What is the weakest point of this solution?"
- "Where could it fail?"
- "Which assumption, if wrong, will collapse it?"

### Outside Perspective
- "How would a senior developer criticize this?"
- "What would I think of this code 6 months from now?"
- "What would a rival team say about this?"

### Scale Test
- "What happens under 10x load?"
- "When there are 100x users?"
- "When data grows 1000x?"

### Security
- "Did I check OWASP Top 10?"
- "Which attack vectors are open?"
- "Is there a risk of data leakage?"
```

## 7.2 Pre-Mortem Analysis

```markdown
## Pre-Mortem: "This Project Failed"

Assume that 6 months from now, this project FAILED. Why?

### Possible Failure Causes
1. [Cause 1] - Probability: [%]
2. [Cause 2] - Probability: [%]
3. [Cause 3] - Probability: [%]

### Measures for Each Cause
| Failure | Measure | Whose Responsibility? |
|--------------|-------|-------------------|
| [Cause 1] | [Measure] | [Who] |
| [Cause 2] | [Measure] | [Who] |
```

---

# 8. Phase 5: Edge Case Matrix

## 8.1 Input Edge Cases

| Scenario | Normal | Edge Case | Strategy |
|---------|--------|-----------|----------|
| Data type | String | null/undefined | Default value + log |
| Length | 1-100 char | 0 or 10000+ | Validation + truncate |
| Format | UTF-8 | Emoji/Special chars | Sanitization |
| Size | <1MB | >100MB | Streaming + chunk |

## 8.2 State Edge Cases

| Scenario | Normal | Edge Case | Strategy |
|---------|--------|-----------|----------|
| Concurrency | Sequential | Parallel writes | Mutex/Lock |
| Timing | <100ms | Timeout | Retry + fallback |
| Connection | Online | Offline | Queue + sync |
| Memory | Normal | High usage | GC + cleanup |

## 8.3 Business Edge Cases

| Scenario | Normal | Edge Case | Strategy |
|---------|--------|-----------|----------|
| User | Active | Deleted mid-op | Graceful abort |
| Permission | Authorized | Role changed | Re-check + deny |
| Data | Complete | Partial/corrupt | Validation + reject |

---

# 9. Phase 6: Self-Correction Loop

## 9.1 Metacognitive Checkpoints

Ask these questions after each phase:

```markdown
## Metacognitive Check

### Progress Check
- [ ] Is progress being made, or am I in a loop?
- [ ] Is this analysis depth sufficient for the problem?
- [ ] Could I be missing something important?

### Confidence Calibration
- My current confidence level: [%]
- Is this confidence level realistic?
- Is more evidence needed?

### Revision Need
- [ ] Do I need to revise my previous thoughts?
- [ ] Which assumption of mine has changed?
- [ ] How does new information affect my hypotheses?
```

## 9.2 Bias Detection and Correction

| Bias | Danger | Check Question | Correction |
|------|---------|----------------|----------|
| **Anchoring** | Getting stuck on the first idea | "Is my first idea really the best?" | Generate 3+ alternatives |
| **Confirmation** | Searching for supporting evidence | "Did I search for contrary evidence?" | Actively try to disprove |
| **Availability** | First example that comes to mind | "What is the base rate?" | Search for statistics/data |
| **Sunk Cost** | Unable to give up on investment | "What would I do if I started from scratch?" | Fresh evaluation |
| **Overconfidence** | Excessive confidence | "How could I be wrong?" | Add 10% margin of error |

---

# 10. Phase 7: Synthesis and Decision

## 10.1 Final Decision Template

```markdown
# 🧠 UltraThink Analysis Report

## Summary
[Summarize main findings in 2-3 sentences]

## Selected Solution
**Approach:** [Name]
**Confidence Level:** [%]
**Rationale:** [Why this was selected - 2-3 sentences]

## Rejected Alternatives
1. **[Alternative 1]** - Reason for rejection: [Short explanation]
2. **[Alternative 2]** - Reason for rejection: [Short explanation]

## Risk Matrix
| Risk | Probability | Impact | Measure |
|------|------------|--------|---------|
| [Risk 1] | [%] | [Low/Medium/High] | [Strategy] |
| [Risk 2] | [%] | [Low/Medium/High] | [Strategy] |

## Action Plan
1. [ ] **Step 1:** [Description] - [Duration]
2. [ ] **Step 2:** [Description] - [Duration]
3. [ ] **Step 3:** [Description] - [Duration]

## Success Criteria
- [ ] [Criterion 1]
- [ ] [Criterion 2]
- [ ] [Criterion 3]

## Review Date
This decision should be re-evaluated on [date].
```

---

# 11. Chain-of-Thought Prompt

```
"While solving this problem, I will follow these steps:

1. META-PLANNING: First evaluate the problem, determine complexity
2. UNDERSTANDING: Express the problem in my own words, separate knowns/unknowns
3. HYPOTHESIS: Generate at least 3 hypotheses, determine confidence level for each
4. ALTERNATIVE: Generate at least 3 solution paths, compare
5. CRITICAL: Question every solution, be the devil's advocate
6. EDGE CASE: List unexpected situations
7. SELF-CHECK: Question my own thinking, check for bias
8. DECISION: Give the final decision with rationale

In every step:
- State my confidence level (%0-100)
- Mark uncertainties
- Explain assumptions
- Evaluate alternative views

Do not answer until thinking is complete. Show steps."
```

---

# 12. Checklist

For every UltraThink analysis:

- [ ] Meta-planning performed (complexity, depth determined)
- [ ] Problem expressed from 3 different angles
- [ ] At least 3 hypotheses generated
- [ ] At least 3 solution alternatives evaluated
- [ ] Devil's advocate questions asked
- [ ] Pre-mortem analysis performed
- [ ] Edge cases listed
- [ ] Bias check performed
- [ ] Confidence level calibrated
- [ ] Final decision justified

---

# 13. Don't Checklist

❌ Don't immediately apply the first solution that comes to mind
❌ Don't look from a single perspective
❌ Don't accept assumptions without questioning
❌ Don't decide without generating alternatives
❌ Don't code without thinking about edge cases
❌ Don't show your confidence level as 100%
❌ Don't skip bias check
❌ Don't give decision without justification

---

# 14. Must-Do Checklist

✅ Evaluate every problem from at least 3 different angles
✅ Generate minimum 3 alternative solutions
✅ State confidence level for every decision
✅ Write assumptions clearly
✅ Ask "How can I be wrong?"
✅ List edge cases and determine their strategies
✅ Justify your decision
✅ Give an action plan
✅ Define success criteria

---

# 15. Thinking Tools Reference

| Tool | When? | How? |
|------|-----------|--------|
| **First Principles** | Complex problem | Go down to core facts, build from there |
| **Inversion** | Risk analysis | "What SHOULDN'T I do?" question |
| **Analogy** | New problem | Search for similar solved problems |
| **Systems Thinking** | Complex system | Map interactions between parts |
| **Probabilistic** | Uncertainty | Estimate and update probabilities |
| **Red Team** | Decision validation | Attack your own solution |

---

**Last Update:** December 2025
**Version:** 3.0
