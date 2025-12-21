---
name: refactoring
description: Safe code refactoring guide. Behavior preservation, incremental changes, and 2025 refactoring patterns.
metadata:
  skillport:
    category: quality
    tags:
      - refactoring
      - code-quality
      - clean-code
      - technical-debt
---

# Refactoring Skill - Safe Code Improvement

> Methodology for improving existing code without breaking it.
> Behavior preservation, incremental changes, and test-first refactoring.

---

## 🎯 The Golden Rule of Refactoring

> **"Refactoring does NOT change behavior, it only improves structure"**

```
Before Refactoring:
  Input: X → [Code A] → Output: Y

After Refactoring:
  Input: X → [Code B] → Output: Y  (SAME Output!)
```

---

## 📏 When to Refactor?

### Time to Refactor

| Signal | Example |
|--------|-------|
| **Code Smell** | Duplicate code, long method, large class |
| **Boy Scout Rule** | "Leave the code cleaner than you found it" |
| **Before adding feature** | Prepare the ground before adding a new feature |
| **After fixing bug** | Improve the code after a bug fix |
| **Code review feedback** | When receiving improvement suggestions |

### When NOT to Refactor

| Case | Why? |
|-------|--------|
| ❌ Deadline is very close | Risk is too high |
| ❌ Test coverage is low | No safety net |
| ❌ Without understanding the system | Intervening in the wrong place |
| ❌ Along with a feature | Keep them in separate commits |

---

## 🔄 The Refactoring Process

### Step 1: Create a Safety Net

```typescript
// Document and test current behavior
describe('calculateTotal', () => {
  test('should calculate total for multiple items', () => {
    expect(calculateTotal([
      { price: 100, qty: 2 },
      { price: 50, qty: 1 }
    ])).toBe(250);
  });
});
```

### Step 2: Proceed in Small Steps

```typescript
// ❌ INCORRECT: Large change
// Delete the entire file and rewrite

// ✅ CORRECT: Small steps
// Commit 1: Extract helper function
// Commit 2: Rename variables
// Commit 3: Simplify conditionals
```

---

## 🛠️ Common Refactoring Patterns

### 1. Extract Function

```typescript
// ✅ AFTER: Extracted functions
function processOrder(order: Order) {
  validateOrder(order);
  const grandTotal = calculateOrderTotal(order);
  return saveOrder(order, grandTotal);
}
```

### 2. Replace Magic Numbers with Constants

```typescript
// ✅ AFTER
const LEGAL_AGE = 18;
const TAX_RATE = 0.18;

if (user.age >= LEGAL_AGE) { /* ... */ }
const tax = amount * TAX_RATE;
```

---

## 🛡️ Safe Refactoring Checklist

### Before Starting

- [ ] Is test coverage sufficient? (min 80%)
- [ ] Do all tests pass?
- [ ] Do I understand the current code?
- [ ] Have I planned the steps?

### During Refactoring

- [ ] Proceeding in small steps
- [ ] Running tests at every step
- [ ] Committing every successful step
- [ ] Not adding features (only refactor)

---

## ✅ Checklist

In every refactoring:

- [ ] Sufficient test coverage present
- [ ] Current behavior documented
- [ ] Proceeding in small steps
- [ ] Every step is a separate commit
- [ ] Tests pass at every step
- [ ] No features added
- [ ] No bug fixes made
- [ ] Performance checked
- [ ] Code review performed

---

## 🔴 Don't List

❌ Do not refactor without tests
❌ Do not make large changes at once
❌ Do not put refactor + feature in the same PR
❌ Do not put refactor + bugfix in the same commit
❌ Do not "refactor" in a way that changes behavior
❌ Do not refactor without understanding
❌ Do not refactor right at the deadline

---

## ✅ Must Do List

✅ Write tests first or verify existing tests
✅ Understand current behavior
✅ Proceed in small steps
✅ Run tests at every step
✅ Commit every step separately
✅ Have a rollback strategy
✅ Get code review
✅ Measure performance

---

**Last Update:** December 2025
**Version:** 1.0
