# Test Workflow

## Description
Test generation and execution workflow. Creates comprehensive tests following the test pyramid and ensures adequate coverage.

---

## Invocation
```
/test [component or feature to test]
```

---

## Steps

### Step 1: Identify Test Scope

```markdown
## Test Scope Analysis

### Target: [Component/Feature name]

### Test Types Needed
- [ ] Unit tests (functions, utils)
- [ ] Integration tests (API, services)
- [ ] E2E tests (user flows)

### Files to Test
- src/services/userService.ts
- src/utils/validation.ts
```

### Step 2: Write Unit Tests

Follow AAA pattern:

```typescript
describe('[Component/Function name]', () => {
  // Happy path
  test('should [expected behavior] when [condition]', () => {
    // Arrange
    const input = { /* setup */ };

    // Act
    const result = functionUnderTest(input);

    // Assert
    expect(result).toBe(expectedValue);
  });

  // Edge cases
  test('should handle empty input', () => {
    expect(functionUnderTest([])).toEqual([]);
  });

  test('should throw on invalid input', () => {
    expect(() => functionUnderTest(null)).toThrow();
  });
});
```

### Step 3: Write Integration Tests

```typescript
describe('POST /api/users', () => {
  test('creates a new user', async () => {
    const response = await request(app)
      .post('/api/users')
      .send({ email: 'test@test.com', name: 'Test' })
      .expect(201);

    expect(response.body.data.email).toBe('test@test.com');
  });

  test('returns 400 for invalid email', async () => {
    const response = await request(app)
      .post('/api/users')
      .send({ email: 'invalid', name: 'Test' })
      .expect(400);

    expect(response.body.error.code).toBe('VALIDATION_ERROR');
  });
});
```

### Step 4: Coverage Analysis

```bash
# Run with coverage
npm run test:coverage

# Check coverage report
```

```markdown
## Coverage Report

| File | Statements | Branches | Functions | Lines |
|------|------------|----------|-----------|-------|
| userService.ts | 95% | 90% | 100% | 95% |
| validation.ts | 100% | 100% | 100% | 100% |

### Coverage Targets
- Overall: >= 80%
- Critical paths: >= 95%
- New code: 100%
```

### Step 5: Test Quality Checklist

```markdown
## Test Quality Check

### Test Independence
- [ ] Tests can run in any order
- [ ] No shared mutable state
- [ ] Proper cleanup in afterEach

### Determinism
- [ ] No flaky tests
- [ ] No time-dependent tests
- [ ] Mocked external services

### Coverage
- [ ] Happy paths covered
- [ ] Error cases covered
- [ ] Edge cases covered
- [ ] Boundary conditions tested
```

---

## Test Pyramid

```
        /\
       /E2E\     <- 10% (Slow, expensive)
      /------\
     /INTEGR. \   <- 20% (Balance)
    /----------\
   /   UNIT     \  <- 70% (Fast, cheap)
  /--------------\
```

---

## Output

Complete test suite with:
- Unit tests for functions/utilities
- Integration tests for APIs
- Coverage report
- All tests passing

---

## Related Workflows
- `/implement` - Tests before implementation
- `/debug` - Write regression tests after fixes
