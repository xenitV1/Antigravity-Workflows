---
description: Safe refactoring workflow that preserves behavior while improving code structure. Ensures proper test coverage and incremental changes.
---

# Refactor Workflow

## Description
Use this workflow when improving code structure without changing behavior. It ensures proper test coverage, incremental changes, and verification at each step.

---

## Invocation
```
/refactor [target code or pattern]
```

---

## Steps

### Step 1: Pre-Refactor Safety Check

```markdown
## Safety Checklist

### Test Coverage
- Current coverage: [X%]
- Required: >= 80%
- [ ] Coverage sufficient

### Understanding
- [ ] Code behavior understood
- [ ] Edge cases identified
- [ ] Dependencies mapped

### Git State
- [ ] Clean working tree
- [ ] Feature branch created
```

### Step 2: Characterization Tests

If coverage is low, write tests first:

```typescript
// Document existing behavior before changing
describe('calculateTotal - Characterization Tests', () => {
  test('existing behavior for single item', () => {
    expect(calculateTotal([{ price: 100, qty: 1 }])).toBe(100);
  });

  test('existing behavior for empty array', () => {
    expect(calculateTotal([])).toBe(0);
  });
});
```

### Step 3: Identify Refactoring Pattern

```markdown
## Refactoring Plan

### Code Smell Detected
[e.g., Long Method, Duplicate Code, Magic Numbers]

### Pattern to Apply
[e.g., Extract Function, Replace Magic Numbers, Strategy Pattern]

### Scope
- Files affected: [list]
- Functions to change: [list]
```

### Step 4: Incremental Changes

Make small, atomic commits:

```markdown
## Change Sequence

### Commit 1: Extract helper function
- [ ] Extract logic
- [ ] Run tests
- [ ] Commit

### Commit 2: Rename variables
- [ ] Rename for clarity
- [ ] Run tests
- [ ] Commit

### Commit 3: Simplify conditionals
- [ ] Apply pattern
- [ ] Run tests
- [ ] Commit
```

After EACH commit:
```bash
npm test
npx tsc --noEmit
```

### Step 5: Verification

```markdown
## Post-Refactor Verification

### Tests
- [ ] All existing tests pass
- [ ] No new failures

### Quality
- [ ] TypeScript: No errors
- [ ] ESLint: No new warnings
- [ ] Prettier: Formatted

### Behavior
- [ ] Behavior unchanged
- [ ] Performance not degraded
```

---

## Common Refactoring Patterns

| Pattern | Before | After |
|---------|--------|-------|
| Extract Function | Long method | Multiple focused functions |
| Replace Magic Number | `if (age >= 18)` | `if (age >= LEGAL_AGE)` |
| Simplify Conditional | Nested if-else | Early return + lookup table |
| Remove Duplication | Copy-pasted code | Shared utility function |

---

## Rollback Strategy

```bash
# If tests fail, revert last commit
git revert HEAD

# Or reset to before refactoring
git reset --hard origin/main
```

---

## Output

Refactored code with:
- Improved structure
- Same behavior (verified by tests)
- Incremental commits
- Documentation of changes

---

## Related Workflows
- `/test` - Ensure coverage before refactoring
- `/review` - Code review after refactoring
