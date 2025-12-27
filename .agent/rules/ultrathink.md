# UltraThink - Deep Analysis Protocol

## Activation
- **Mode:** Model Decision
- **Description:** Maximum thinking capacity protocol. Activate for: architectural decisions, performance optimization, complex bug analysis, multi-step planning, system design, trade-off evaluation, risk analysis, and critical decision-making.

---

## Core Protocol

### Phase 0: Meta-Planning (ALWAYS START HERE)

```markdown
## Meta-Planning

### Problem Assessment
- **Complexity (1-10):** [Score]
- **Risk Level:** [Low/Medium/High/Critical]
- **Impact Area:** [Local/Module/System-wide]
- **Reversibility:** [Easy/Hard/Impossible]
```

### Socratic Reality Check (5-Step - MANDATORY REFLEX)

Ask these 5 questions BEFORE EVERY operation:

1. **User Intent:** "What EXACTLY does the user want?"
2. **Context:** "Am I working on the correct file/location?"
3. **Action:** "What am I doing right now?" (Simple definition)
4. **Rationale:** "Why this way? Is there a simpler approach?"
5. **Ripple Effect:** "What could this change break?"

> **NEVER** take action without answering Ripple Effect. Calculate the domino effect.

---

## 7-Phase Analysis Cycle

### Phase 1: Problem Understanding
- Express problem in your own words
- Create Information Map: Knowns, Unknowns, Assumptions
- List constraints (technical, business, quality)

### Phase 2: Hypothesis Generation
- Generate minimum 3 hypotheses
- Assign confidence level (0-100%) to each
- List assumptions and test methods

### Phase 3: Solution Space Exploration
- Generate minimum 3 alternative approaches
- Create comparison matrix (Performance, Complexity, Cost, Risk)
- Weight criteria and score alternatives

### Phase 4: Critical Evaluation
**Devil's Advocate Questions:**
- "What is the weakest point?"
- "Where could it fail?"
- "How would a senior developer criticize this?"

**Pre-Mortem:** Assume project FAILED in 6 months. Why?

### Phase 5: Edge Case Matrix
| Category | Normal | Edge Case | Strategy |
|----------|--------|-----------|----------|
| Input | Expected | null/empty/overflow | Validate + fallback |
| State | Sequential | Concurrent | Lock/Mutex |
| Business | Active user | Deleted mid-op | Graceful abort |

### Phase 6: Self-Correction Loop
- Progress check: Am I in a loop?
- Confidence calibration: Is my confidence realistic?
- Bias detection: Anchoring, Confirmation, Sunk Cost?

### Phase 7: Synthesis and Decision
```markdown
# UltraThink Analysis Report

## Summary
[2-3 sentences]

## Selected Solution
**Approach:** [Name]
**Confidence:** [%]
**Rationale:** [Why]

## Risk Matrix
| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|

## Action Plan
1. [ ] Step 1
2. [ ] Step 2
3. [ ] Step 3
```

---

## Thinking Depth Levels

| Level | Steps | When? |
|-------|-------|-------|
| Light | 3-5 | Simple decision |
| Medium | 8-15 | Multiple dependencies |
| Deep | 20-40 | System-wide impact |
| Ultra | 50+ | Critical, irreversible |

---

## Bias Detection

| Bias | Check Question | Correction |
|------|----------------|------------|
| Anchoring | "Is my first idea really best?" | Generate 3+ alternatives |
| Confirmation | "Did I seek contrary evidence?" | Try to disprove |
| Sunk Cost | "What if I started fresh?" | Fresh evaluation |
| Overconfidence | "How could I be wrong?" | Add 10% margin |

---

## Thinking Tools

| Tool | When | How |
|------|------|-----|
| First Principles | Complex problem | Break to core facts |
| Inversion | Risk analysis | "What NOT to do?" |
| Analogy | New problem | Find similar solved cases |
| Red Team | Validation | Attack own solution |

---

## Checklist

- [ ] Meta-planning performed
- [ ] Socratic Reality Check completed
- [ ] Problem viewed from 3+ angles
- [ ] 3+ hypotheses generated
- [ ] 3+ alternatives evaluated
- [ ] Devil's advocate asked
- [ ] Pre-mortem done
- [ ] Edge cases listed
- [ ] Bias checked
- [ ] Decision justified

---

## Don't Checklist

- Never apply first solution immediately
- Never look from single perspective
- Never accept assumptions without questioning
- Never decide without alternatives
- Never code without edge case thinking
- Never show 100% confidence
- Never skip bias check
- Never give unjustified decisions

---

**Version:** 3.0 (Antigravity Rule Format)
