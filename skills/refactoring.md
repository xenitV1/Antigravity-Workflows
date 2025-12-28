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

# 📋 Contents

1. [The Golden Rule of Refactoring](#1-the-golden-rule-of-refactoring)
2. [When to Refactor?](#2-when-to-refactor)
3. [The Refactoring Process](#3-the-refactoring-process)
4. [Common Refactoring Patterns](#4-common-refactoring-patterns)
5. [Code Smells](#5-code-smells)
6. [Safe Refactoring Checklist](#6-safe-refactoring-checklist)
7. [Incremental Refactoring Strategy](#7-incremental-refactoring-strategy)
8. [Checklist](#8-checklist)
9. [Don't List](#9-dont-list)
10. [Must Do List](#10-must-do-list)

---

# 1. The Golden Rule of Refactoring

> **"Refactoring does NOT change behavior, it only improves structure"**

```
Before Refactoring:
  Input: X → [Code A] → Output: Y

After Refactoring:
  Input: X → [Code B] → Output: Y  (SAME Output!)
```

---

# 2. When to Refactor?

## 2.1 Time to Refactor

| Signal | Example |
|--------|-------|
| **Code Smell** | Duplicate code, long method, large class |
| **Boy Scout Rule** | "Leave the code cleaner than you found it" |
| **Before adding feature** | Prepare the ground before adding a new feature |
| **After fixing bug** | Improve the code after a bug fix |
| **Code review feedback** | When receiving improvement suggestions |

## 2.2 When NOT to Refactor

| Case | Why? |
|-------|--------|
| ❌ Deadline is very close | Risk is too high |
| ❌ Test coverage is low | No safety net |
| ❌ Without understanding the system | Intervening in the wrong place |
| ❌ Along with a feature | Keep them in separate commits |

---

# 3. The Refactoring Process

## 3.1 Step 1: Create a Safety Net

```typescript
// Document and test current behavior
describe('calculateTotal', () => {
  // Existing behavior tests (characterization tests)
  test('should calculate total for single item', () => {
    expect(calculateTotal([{ price: 100, qty: 1 }])).toBe(100);
  });

  test('should calculate total for multiple items', () => {
    expect(calculateTotal([
      { price: 100, qty: 2 },
      { price: 50, qty: 1 }
    ])).toBe(250);
  });

  test('should handle empty array', () => {
    expect(calculateTotal([])).toBe(0);
  });

  // Edge cases
  test('should handle zero quantity', () => {
    expect(calculateTotal([{ price: 100, qty: 0 }])).toBe(0);
  });
});
```

## 3.2 Step 2: Proceed in Small Steps

```typescript
// ❌ INCORRECT: Large change
// Delete the entire file and rewrite

// ✅ CORRECT: Small steps
// Commit 1: Extract helper function
// Commit 2: Rename variables
// Commit 3: Simplify conditionals
// Commit 4: Remove duplication
```

## 3.3 Step 3: Run Tests at Every Step

```bash
# After every small change
npm test

# If tests pass, commit
git add .
git commit -m "refactor: extract calculateItemTotal helper"

# Move to next step
```

---

# 4. Common Refactoring Patterns

## 4.1 Extract Function

```typescript
// ❌ BEFORE: Long function
function processOrder(order: Order) {
  // Validation (10 lines)
  if (!order.items) throw new Error('No items');
  if (order.items.length === 0) throw new Error('Empty order');
  if (!order.customerId) throw new Error('No customer');
  
  // Calculate total (15 lines)
  let total = 0;
  for (const item of order.items) {
    total += item.price * item.quantity;
  }
  const tax = total * 0.18;
  const grandTotal = total + tax;
  
  // Save to database (10 lines)
  // ...
}

// ✅ AFTER: Extracted functions
function processOrder(order: Order) {
  validateOrder(order);
  const grandTotal = calculateOrderTotal(order);
  return saveOrder(order, grandTotal);
}

function validateOrder(order: Order): void {
  if (!order.items) throw new Error('No items');
  if (order.items.length === 0) throw new Error('Empty order');
  if (!order.customerId) throw new Error('No customer');
}

function calculateOrderTotal(order: Order): number {
  const subtotal = order.items.reduce(
    (sum, item) => sum + item.price * item.quantity,
    0
  );
  const tax = subtotal * 0.18;
  return subtotal + tax;
}
```

## 4.2 Replace Conditional with Polymorphism

```typescript
// ❌ BEFORE: Switch statement
function calculateShipping(order: Order): number {
  switch (order.shippingType) {
    case 'standard':
      return order.weight * 1.0;
    case 'express':
      return order.weight * 2.5;
    case 'overnight':
      return order.weight * 5.0 + 10;
    default:
      throw new Error('Unknown shipping type');
  }
}

// ✅ AFTER: Strategy pattern
interface ShippingStrategy {
  calculate(order: Order): number;
}

class StandardShipping implements ShippingStrategy {
  calculate(order: Order): number {
    return order.weight * 1.0;
  }
}

class ExpressShipping implements ShippingStrategy {
  calculate(order: Order): number {
    return order.weight * 2.5;
  }
}

class OvernightShipping implements ShippingStrategy {
  calculate(order: Order): number {
    return order.weight * 5.0 + 10;
  }
}

const shippingStrategies: Record<string, ShippingStrategy> = {
  standard: new StandardShipping(),
  express: new ExpressShipping(),
  overnight: new OvernightShipping(),
};

function calculateShipping(order: Order): number {
  const strategy = shippingStrategies[order.shippingType];
  if (!strategy) throw new Error('Unknown shipping type');
  return strategy.calculate(order);
}
```

## 4.3 Replace Magic Numbers with Constants

```typescript
// ❌ BEFORE
if (user.age >= 18) { /* ... */ }
const tax = amount * 0.18;
if (retryCount > 3) { /* ... */ }

// ✅ AFTER
const LEGAL_AGE = 18;
const TAX_RATE = 0.18;
const MAX_RETRY_COUNT = 3;

if (user.age >= LEGAL_AGE) { /* ... */ }
const tax = amount * TAX_RATE;
if (retryCount > MAX_RETRY_COUNT) { /* ... */ }
```

## 4.4 Simplify Conditionals

```typescript
// ❌ BEFORE: Nested conditionals
function getDiscount(user: User, order: Order): number {
  if (user.isPremium) {
    if (order.total > 1000) {
      return 0.20;
    } else if (order.total > 500) {
      return 0.15;
    } else {
      return 0.10;
    }
  } else {
    if (order.total > 1000) {
      return 0.10;
    } else if (order.total > 500) {
      return 0.05;
    } else {
      return 0;
    }
  }
}

// ✅ AFTER: Early return + table
const DISCOUNT_TABLE = {
  premium: { high: 0.20, medium: 0.15, low: 0.10 },
  regular: { high: 0.10, medium: 0.05, low: 0 },
};

function getDiscount(user: User, order: Order): number {
  const tier = user.isPremium ? 'premium' : 'regular';
  const level = getOrderLevel(order.total);
  return DISCOUNT_TABLE[tier][level];
}

function getOrderLevel(total: number): 'high' | 'medium' | 'low' {
  if (total > 1000) return 'high';
  if (total > 500) return 'medium';
  return 'low';
}
```

## 4.5 Remove Duplication (DRY)

```typescript
// ❌ BEFORE: Duplicated code
async function createUser(data: CreateUserDto) {
  const user = await prisma.user.create({ data });
  await sendEmail(user.email, 'Welcome!', 'Welcome to our platform');
  await logActivity('user_created', user.id);
  return user;
}

async function createAdmin(data: CreateAdminDto) {
  const admin = await prisma.admin.create({ data });
  await sendEmail(admin.email, 'Welcome Admin!', 'Welcome to admin panel');
  await logActivity('admin_created', admin.id);
  return admin;
}

// ✅ AFTER: Extracted common logic
async function createAccount<T>(
  createFn: () => Promise<T & { id: string; email: string }>,
  welcomeMessage: string,
  activityType: string
): Promise<T & { id: string; email: string }> {
  const account = await createFn();
  await sendEmail(account.email, 'Welcome!', welcomeMessage);
  await logActivity(activityType, account.id);
  return account;
}

async function createUser(data: CreateUserDto) {
  return createAccount(
    () => prisma.user.create({ data }),
    'Welcome to our platform',
    'user_created'
  );
}
```

---

# 5. Code Smells

## 5.1 Identification

| Smell | Symptom | Solution |
|-------|---------|-------|
| **Long Method** | >20 lines | Extract Method |
| **Large Class** | >300 lines | Extract Class |
| **Long Parameter List** | >3 params | Introduce Parameter Object |
| **Duplicate Code** | Copy-paste | Extract Method/Class |
| **Feature Envy** | Working too much with another class's data | Move Method |
| **Data Clumps** | Data hanging out together | Extract Class |
| **Primitive Obsession** | Not using objects for string/number | Value Object |
| **Switch Statements** | Many switch/if-else | Polymorphism |
| **Parallel Inheritance** | Creating twin for every new class | Inheritance refactor |
| **Dead Code** | Unused code | Remove |

## 5.2 Detection Tools

```bash
# ESLint complexity rules
# .eslintrc.js
{
  "rules": {
    "complexity": ["error", { "max": 10 }],
    "max-lines-per-function": ["error", { "max": 50 }],
    "max-depth": ["error", { "max": 3 }],
    "max-params": ["error", { "max": 3 }]
  }
}

# SonarQube/SonarLint
sonar.qualitygate.wait=true
```

---

# 6. Safe Refactoring Checklist

## 6.1 Before Starting

```markdown
## Pre-Refactoring Checklist

### Safety Net
- [ ] Is test coverage sufficient? (minimum 80%)
- [ ] Do all tests pass?
- [ ] Is CI/CD pipeline green?

### Understanding
- [ ] Do I understand the current code?
- [ ] Do I know the edge cases?
- [ ] Have I mapped the dependencies?

### Planning
- [ ] Which refactoring pattern will I apply?
- [ ] Have I planned the steps?
- [ ] Do I have a rollback strategy?

### Communication
- [ ] Have I informed the team?
- [ ] Is there a code freeze?
```

## 6.2 During Refactoring

```markdown
## During Refactoring

- [ ] Proceeding in small steps
- [ ] Running tests at every step
- [ ] Committing every successful step
- [ ] Not adding features (only refactor)
- [ ] Not fixing bugs (only refactor)
```

## 6.3 After Refactoring

```markdown
## Post-Refactoring

- [ ] All tests pass
- [ ] No lint errors
- [ ] No type errors
- [ ] No performance regression
- [ ] Code review requested
- [ ] Documentation updated
```

---

# 7. Incremental Refactoring Strategy

## 7.1 Strangler Fig Pattern

```typescript
// Apply new code wrapper, slowly replace the old one

// Step 1: Create wrapper
class UserServiceWrapper {
  private legacyService: LegacyUserService;
  private newService: NewUserService;

  async getUser(id: string) {
    // Use legacy at first
    return this.legacyService.getUser(id);
  }
}

// Step 2: Route with Feature flag
async getUser(id: string) {
  if (featureFlags.useNewUserService) {
    return this.newService.getUser(id);
  }
  return this.legacyService.getUser(id);
}

// Step 3: Full transition
async getUser(id: string) {
  return this.newService.getUser(id);
}

// Step 4: Remove legacy
```

---

# 8. Checklist

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

# 9. Don't List

❌ Do not refactor without tests
❌ Do not make large changes at once
❌ Do not put refactor + feature in the same PR
❌ Do not put refactor + bugfix in the same commit
❌ Do not "refactor" in a way that changes behavior
❌ Do not refactor without understanding
❌ Do not refactor right at the deadline

---

# 10. Must Do List

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
**Version:** 2.0
