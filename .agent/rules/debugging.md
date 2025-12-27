# Debugging Rule

## Activation
- **Mode:** Model Decision
- **Description:** Systematic debugging methodology with root cause analysis. Activate for: bug investigation, error diagnosis, performance issues, and production incidents.

---

## Debugging Cycle (MANDATORY ORDER)

```
REPRODUCE → UNDERSTAND → ISOLATE → HYPOTHESIZE → TEST → FIX → REFLECT
```

---

## Phase 1: REPRODUCE

```markdown
## Bug Reproduction Report

### Observed Behavior
- What happens: [Description]
- Error message: [Full text]
- When started: [Date/commit]

### Steps to Reproduce
1. [Step 1]
2. [Step 2]
3. [Step 3] → Error occurs

### Environment
- OS: [Version]
- Node: [Version]
- Browser: [If applicable]

### Reproducibility
- [ ] Always
- [ ] Sometimes (rate: %)
- [ ] Rare
```

---

## Phase 2: UNDERSTAND

- Map the system (data flow, component interaction)
- Identify expected vs actual behavior
- List relevant code paths

```markdown
## System Context

### Data Flow
Input → [Component A] → [Component B] → Output

### Expected Behavior
[What should happen]

### Actual Behavior
[What is happening]
```

---

## Phase 3: ISOLATE

### Binary Search Method
```
1. Find the scope (which 50% contains the bug?)
2. Divide that half
3. Repeat until pinpointed
```

### Minimal Reproduction
- Remove code until bug disappears
- Add back until it reappears
- Smallest case that reproduces = isolation

---

## Phase 4: HYPOTHESIZE

```markdown
## Hypothesis List

| # | Hypothesis | Probability | Test Method |
|---|------------|-------------|-------------|
| 1 | [H1 Description] | 40% | [How to test] |
| 2 | [H2 Description] | 30% | [How to test] |
| 3 | [H3 Description] | 20% | [How to test] |
```

### Common Bug Patterns

| Pattern | Symptoms | Check |
|---------|----------|-------|
| Null Reference | TypeError | Value undefined? |
| Race Condition | Intermittent | Async ordering? |
| Memory Leak | Slow over time | Cleanup present? |
| Off-by-One | Edge values wrong | Loop bounds? |
| State Mutation | Unexpected changes | Immutability? |

---

## Phase 5: TEST

- Test hypotheses in order of probability
- One hypothesis at a time
- Document results

```markdown
## Test Results

### H1: [Hypothesis]
- Test: [What was done]
- Result: [CONFIRMED / REJECTED]
- Evidence: [What proved it]
```

---

## Phase 6: FIX

### Fix Requirements
- [ ] Minimal change (don't over-engineer)
- [ ] Addresses root cause (not symptoms)
- [ ] Doesn't break other things
- [ ] Includes regression test

### Fix Template
```typescript
// BEFORE (bug)
[old code]

// AFTER (fix)
[new code]

// WHY: [Explanation of root cause]
```

---

## Phase 7: REFLECT

```markdown
## Post-Mortem

### Root Cause
[What actually caused the bug]

### Why Not Caught Earlier
[Gap in testing/review]

### Prevention
[How to prevent similar bugs]

### Lessons Learned
1. [Lesson 1]
2. [Lesson 2]
```

---

## 5 Whys Technique

```
Problem: User login fails
Why 1: Token is invalid → Why?
Why 2: Token expired → Why?
Why 3: Clock skew between servers → Why?
Why 4: NTP not configured → Why?
Why 5: Infrastructure setup incomplete → ROOT CAUSE
```

---

## Debugging Tools

| Tool | Purpose |
|------|---------|
| Chrome DevTools | Frontend debugging |
| VS Code Debugger | Breakpoints, step-through |
| Postman/Insomnia | API testing |
| console.log | Quick inspection |
| Structured logging | Production debugging |

---

## Checklist

- [ ] Bug reproduced consistently
- [ ] System flow understood
- [ ] Problem isolated
- [ ] Hypotheses listed with probabilities
- [ ] Root cause confirmed
- [ ] Fix is minimal
- [ ] Regression test written
- [ ] Post-mortem documented

---

**Version:** 2.0 (Antigravity Rule)
