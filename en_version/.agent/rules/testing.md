# Testing Rule

## Activation
- **Mode:** Glob
- **Glob Pattern:** `*.test.*, *.spec.*, __tests__/**, tests/**`
- **Description:** Comprehensive testing strategies including unit, integration, E2E, and visual testing. Auto-activates for test files.

---

## Test Pyramid

```
      /\
     /E2E\  ← 10% - Slowest, most expensive
    /------\
   /INTEGR.\  ← 20% - Balance of speed & confidence
  /----------\
 /   UNIT     \  ← 70% - Fastest, cheapest
/--------------\
```

| Type | Scope | Speed | Coverage |
|------|-------|-------|----------|
| Unit | Function/Component | ⚡⚡⚡ | 70% |
| Integration | Module boundaries | ⚡⚡ | 20% |
| E2E | User flows | ⚡ | 10% |

---

## Unit Testing (Jest)

```typescript
describe('sum function', () => {
  test('adds 1 + 2 to equal 3', () => {
    expect(sum(1, 2)).toBe(3);
  });

  test('handles zero correctly', () => {
    expect(sum(0, 0)).toBe(0);
  });
});
```

### Mocking
```typescript
jest.mock('./apiService');

test('should use mocked data', async () => {
  (fetchData as jest.Mock).mockResolvedValue({ id: 1 });
  const data = await getServiceData();
  expect(data.id).toBe(1);
});
```

---

## Integration Testing (Supertest)

```typescript
import request from 'supertest';

describe('POST /api/users', () => {
  test('creates a new user', async () => {
    const response = await request(app)
      .post('/api/users')
      .send({ email: 'test@test.com', name: 'Test' })
      .expect(201);

    expect(response.body.data.email).toBe('test@test.com');
  });
});
```

---

## E2E Testing (Playwright)

```typescript
import { test, expect } from '@playwright/test';

test('user login flow', async ({ page }) => {
  await page.goto('/login');
  await page.fill('[name=email]', 'user@test.com');
  await page.fill('[name=password]', 'password123');
  await page.click('button[type=submit]');

  await expect(page).toHaveURL('/dashboard');
});
```

---

## TDD Workflow

```
   ┌─────────┐
   │  RED    │ ← Write failing test
   └────┬────┘
        │
        ▼
   ┌─────────┐
   │ GREEN   │ ← Write minimum code to pass
   └────┬────┘
        │
        ▼
   ┌─────────┐
   │REFACTOR │ ← Clean up, keep tests green
   └─────────┘
```

---

## Test Writing Rules

### AAA Pattern
```typescript
test('should calculate total', () => {
  // Arrange
  const cart = new Cart();
  cart.addItem({ price: 10 });

  // Act
  const total = cart.getTotal();

  // Assert
  expect(total).toBe(10);
});
```

### Rules
- One assertion per test (when possible)
- Tests must be deterministic
- Tests must be isolated
- No test interdependencies
- Clean up after tests (afterEach)

---

## Coverage Requirements

- Minimum: **80%** overall
- Critical paths: **95%**
- New code: **100%** (no untested new code)

```bash
npm run test:coverage
```

---

## Checklist

- [ ] Test pyramid followed (70/20/10)
- [ ] AAA pattern used
- [ ] No flaky tests
- [ ] Edge cases covered
- [ ] Mocks properly cleaned up
- [ ] Coverage >= 80%
- [ ] CI/CD runs tests

---

## Don't List

- Don't test implementation details
- Don't write tests after bugs (write before)
- Don't skip cleanup in afterEach
- Don't use real external services
- Don't write interdependent tests

---

**Version:** 2.0 (Antigravity Rule)
