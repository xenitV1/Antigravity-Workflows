# Refactoring Rule - Safe Code Improvement

## Activation
- **Mode:** Model Decision
- **Description:** Safe code restructuring methodology. Activate for: code improvement, technical debt reduction, pattern migration, and structural changes that preserve behavior.

---

## Golden Rule

> **"Refactoring does NOT change behavior, only improves structure"**

```
Before: Input X -> [Code A] -> Output Y
After:  Input X -> [Code B] -> Output Y (SAME Output!)
```

---

## When to Refactor

| Signal | Example |
|--------|---------|
| Code Smell | Duplicate code, long method, large class |
| Boy Scout Rule | "Leave code cleaner than you found it" |
| Before adding feature | Prepare ground for new functionality |
| After fixing bug | Improve code after bug fix |
| Code review feedback | When improvement suggestions received |

## When NOT to Refactor

| Situation | Reason |
|-----------|--------|
| Deadline very close | Risk too high |
| Low test coverage | No safety net |
| Without understanding | Wrong intervention |
| With feature | Separate commits |

---

## Refactoring Process

### Step 1: Create Safety Net
```typescript
describe('calculateTotal', () => {
  test('existing behavior', () => {
    expect(calculateTotal([{ price: 100, qty: 1 }])).toBe(100);
  });
});
```

### Step 2: Small Steps
```
Commit 1: Extract helper function
Commit 2: Rename variables
Commit 3: Simplify conditionals
Commit 4: Remove duplication
```

### Step 3: Test After Each Step
```bash
npm test
git commit -m "refactor: extract calculateItemTotal helper"
```

---

## Common Patterns

### Extract Function
```typescript
// BEFORE: Long function
function processOrder(order) {
  // Validation (10 lines)
  // Calculate total (15 lines)
  // Save to database (10 lines)
}

// AFTER: Extracted functions
function processOrder(order) {
  validateOrder(order);
  const total = calculateOrderTotal(order);
  return saveOrder(order, total);
}
```

### Replace Magic Numbers
```typescript
// BEFORE
if (user.age >= 18) { }

// AFTER
const LEGAL_AGE = 18;
if (user.age >= LEGAL_AGE) { }
```

### Simplify Conditionals
```typescript
// BEFORE: Nested if-else
// AFTER: Early return + lookup table
const DISCOUNT_TABLE = {
  premium: { high: 0.20, medium: 0.15, low: 0.10 },
  regular: { high: 0.10, medium: 0.05, low: 0 },
};
```

---

## Code Smells

| Smell | Symptom | Solution |
|-------|---------|----------|
| Long Method | >20 lines | Extract Method |
| Large Class | >300 lines | Extract Class |
| Long Parameter List | >3 params | Parameter Object |
| Duplicate Code | Copy-paste | Extract Method |
| Feature Envy | Uses other class data | Move Method |
| Magic Numbers | Hardcoded values | Constants |
| Dead Code | Unused code | Remove |

---

## Safe Refactoring Checklist

### Before Starting
- [ ] Test coverage sufficient? (min 80%)
- [ ] All tests passing?
- [ ] CI/CD pipeline green?
- [ ] Code understood?
- [ ] Dependencies mapped?

### During Refactoring
- [ ] Small steps
- [ ] Test after each step
- [ ] Separate commit per step
- [ ] No features added
- [ ] No bug fixes

### After Refactoring
- [ ] All tests pass
- [ ] No lint errors
- [ ] No type errors
- [ ] No performance regression
- [ ] Code review requested

---

## Strangler Fig Pattern

For incremental legacy code replacement:

```typescript
// Step 1: Wrapper
class ServiceWrapper {
  async getUser(id) {
    return this.legacyService.getUser(id);
  }
}

// Step 2: Feature flag
async getUser(id) {
  if (featureFlags.useNewService) {
    return this.newService.getUser(id);
  }
  return this.legacyService.getUser(id);
}

// Step 3: Full migration
// Step 4: Remove legacy
```

---

## Checklist

- [ ] Adequate test coverage exists
- [ ] Current behavior documented
- [ ] Proceeding in small steps
- [ ] Each step has separate commit
- [ ] Tests pass at each step
- [ ] No features added
- [ ] No bug fixes mixed in
- [ ] Performance verified
- [ ] Code review completed

---

## Don't List

- Refactor without tests
- Large changes at once
- Refactor + feature in same PR
- Refactor + bugfix in same commit
- "Refactor" that changes behavior
- Refactor without understanding
- Refactor at deadline

---

**Version:** 2.0 (Antigravity Rule)
