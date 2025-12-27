# Debug Workflow

## Description
Systematic debugging workflow for identifying and resolving issues. Uses structured approach to isolate, understand, and fix bugs.

---

## Invocation
```
/debug [error description or symptom]
```

---

## Steps

### Step 1: Reproduce the Issue

```markdown
## Bug Reproduction Report

### Observed Behavior
- What happens: [Description]
- Error message: [Full text]
- When started: [Date/commit if known]

### Steps to Reproduce
1. [Step 1]
2. [Step 2]
3. [Step 3] -> Error occurs

### Environment
- OS: [Version]
- Node: [Version]
- Browser: [If applicable]

### Reproducibility
- [ ] Always
- [ ] Sometimes (rate: %)
- [ ] Rare
```

### Step 2: Understand the System

For complex issues, invoke `/ultrathink`:

```markdown
## System Context

### Data Flow
Input -> [Component A] -> [Component B] -> Output

### Expected Behavior
[What should happen]

### Actual Behavior
[What is happening]
```

### Step 3: Isolate the Problem

Use binary search method:

```markdown
## Isolation Process

1. Which 50% of the code contains the bug?
2. Divide that half
3. Repeat until pinpointed

### Minimal Reproduction
- Remove code until bug disappears
- Add back until it reappears
- Smallest case = isolation complete
```

### Step 4: Hypothesize & Test

```markdown
## Hypothesis List

| # | Hypothesis | Probability | Test Method |
|---|------------|-------------|-------------|
| 1 | [H1 Description] | 40% | [How to test] |
| 2 | [H2 Description] | 30% | [How to test] |
| 3 | [H3 Description] | 20% | [How to test] |

## Test Results

### H1: [Hypothesis]
- Test: [What was done]
- Result: [CONFIRMED / REJECTED]
- Evidence: [What proved it]
```

### Step 5: Apply Fix

```markdown
## Fix Implementation

### Before (Bug)
```code
[old code]
```

### After (Fix)
```code
[new code]
```

### Why This Fixes It
[Explanation of root cause and how fix addresses it]
```

### Step 6: Verify & Prevent

```markdown
## Verification

- [ ] Bug no longer reproduces
- [ ] Related functionality still works
- [ ] Regression test written

## Post-Mortem

### Root Cause
[What actually caused the bug]

### Why Not Caught Earlier
[Gap in testing/review]

### Prevention
[How to prevent similar bugs]
```

---

## Common Bug Patterns

| Pattern | Symptoms | Check |
|---------|----------|-------|
| Null Reference | TypeError | Value undefined? |
| Race Condition | Intermittent | Async ordering? |
| Memory Leak | Slow over time | Cleanup present? |
| Off-by-One | Edge values wrong | Loop bounds? |
| State Mutation | Unexpected changes | Immutability? |

---

## Output

Complete debugging report with:
- Reproduction steps
- Root cause analysis
- Applied fix
- Regression test
- Prevention recommendations

---

## Related Workflows
- `/ultrathink` - For complex root cause analysis
- `/test` - Write regression tests
