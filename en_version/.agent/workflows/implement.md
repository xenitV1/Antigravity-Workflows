# Implement Workflow

## Description
Feature and code implementation workflow. Guides through planning, coding, testing, and review phases for new features or changes.

---

## Invocation
```
/implement [feature description]
```

---

## Steps

### Step 1: Pre-Implementation Planning

For non-trivial features, first run `/plan`:

```markdown
## Implementation Scope

### Feature: [Name]
### Files to Modify:
- [ ] file1.ts
- [ ] file2.ts

### Files to Create:
- [ ] newFile.ts

### Dependencies:
- [List any new dependencies needed]
```

### Step 2: Test First (TDD Approach)

Write tests before implementation:

```typescript
describe('[Feature]', () => {
  test('should [expected behavior]', () => {
    // Arrange
    // Act
    // Assert
  });
});
```

### Step 3: Implementation

Follow the established patterns:

```markdown
## Implementation Checklist

### Code Quality
- [ ] TypeScript strict mode compliant
- [ ] No `any` types
- [ ] Proper error handling
- [ ] Input validation (Zod)

### Security
- [ ] No hardcoded secrets
- [ ] Input sanitization
- [ ] OWASP Top 10 considered

### Performance
- [ ] No N+1 queries
- [ ] Proper caching considered
- [ ] Lazy loading where appropriate
```

### Step 4: Quality Verification

Run all quality checks:

```bash
# Type check
npx tsc --noEmit

# Lint
npx eslint .

# Format
npx prettier --check .

# Tests
npm test
```

### Step 5: Self-Review

Before requesting review, check:

| Aspect | Question |
|--------|----------|
| Correctness | Does it solve the problem? |
| Completeness | Are all edge cases handled? |
| Clarity | Is the code readable? |
| Consistency | Does it follow project patterns? |

---

## Output

Completed implementation with:
- Working code
- Tests passing
- Quality gates passed
- Ready for review

---

## Related Workflows
- `/plan` - For complex feature planning
- `/test` - For comprehensive testing
- `/review` - For code review
