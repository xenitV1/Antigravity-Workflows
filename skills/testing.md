---
name: testing
description: Comprehensive testing strategies and 2025 tools. Unit, integration, e2e, and visual testing.
metadata:
  skillport:
    category: quality
    tags:
      - testing
      - jest
      - playwright
      - quality-assurance
---

# Testing Skill - QA & Test Strategies

> Systematic approaches to ensure software quality.
> 2025 modern testing tools and testing pyramid strategy.

---

# 📋 Contents

1. [Test Pyramid](#1-test-pyramid)
2. [Unit Testing (Jest)](#2-unit-testing-jest)
3. [Integration Testing](#3-integration-testing)
4. [E2E Testing (Playwright)](#4-e2e-testing-playwright)
5. [Visual Regression Testing](#5-visual-regression-testing)
6. [TDD (Test Driven Development)](#6-tdd-test-driven-development)
7. [Test Writing Rules](#7-test-writing-rules)
8. [Checklist](#8-checklist)
9. [Don't List](#9-dont-list)
10. [Must Do List](#10-must-do-list)

---

# 1. Test Pyramid

```
      / \
     /E2E\  ← Fewest (Slow, Expensive, Brittle)
    /-----\
   / INTEGR\ ← Medium (Balance of Speed & Confidence)
  /---------\
 /   UNIT    \ ← Most (Fast, Cheap, Isolated)
/-------------\
```

| Type | Scope | Speed | Cost |
|-----|--------|-----|---------|
| **Unit** | Function/Component | ⚡⚡⚡ | 💸 |
| **Integration** | Between DB/API/Modules | ⚡⚡ | 💸💸 |
| **E2E** | Full user flow | ⚡ | 💸💸💸 |

---

# 2. Unit Testing (Jest)

## 2.1 Basic Test Structure

```typescript
import { sum } from './math';

describe('sum function', () => {
  test('adds 1 + 2 to equal 3', () => {
    expect(sum(1, 2)).toBe(3);
  });

  test('handles zero correctly', () => {
    expect(sum(0, 0)).toBe(0);
  });
});
```

## 2.2 Mocking

```typescript
// Mocking service
jest.mock('./apiService');
import { fetchData } from './apiService';

test('should use mocked data', async () => {
  (fetchData as jest.Mock).mockResolvedValue({ id: 1, name: 'Test' });
  const data = await getServiceData();
  expect(data.name).toBe('Test');
});
```

---

# 3. Integration Testing

## 3.1 API Integration

```typescript
import request from 'supertest';
import app from './app';

describe('POST /api/users', () => {
  test('should create a new user and return it', async () => {
    const response = await request(app)
      .post('/api/users')
      .send({ email: 'test@example.com', name: 'Test' });

    expect(response.status).toBe(201);
    expect(response.body.email).toBe('test@example.com');
  });
});
```

---

# 4. E2E Testing (Playwright)

## 4.1 Login Flow

```typescript
import { test, expect } from '@playwright/test';

test('user can login successfully', async ({ page }) => {
  await page.goto('/login');
  await page.fill('input[name="email"]', 'user@example.com');
  await page.fill('input[name="password"]', 'password123');
  await page.click('button[type="submit"]');

  await expect(page).toHaveURL('/dashboard');
  await expect(page.locator('h1')).toContainText('Welcome');
});
```

---

# 5. Visual Regression Testing

```typescript
// Playwright visual test
test('dashboard visual comparison', async ({ page }) => {
  await page.goto('/dashboard');
  await expect(page).toHaveScreenshot('dashboard.png');
});
```

---

# 6. TDD (Test Driven Development)

1. **RED:** Write the test and see it fail.
2. **GREEN:** Write the minimum code to pass the test.
3. **REFACTOR:** Clean up code and test, follow standards.

---

# 7. Test Writing Rules

- **AAA Pattern:** Arrange, Act, Assert.
- **Isolation:** Tests must be independent of each other.
- **Speed:** Unit tests must run very fast.
- **Readable:** Test name should clearly state what is being tested.
- **Deterministic:** Same input always yields same result.

---

# 8. Checklist

- [ ] Unit tests cover at least 80%?
- [ ] Are there integration tests for critical business logic?
- [ ] Top 3-4 user flows tested with E2E?
- [ ] Tests running automatically in CI/CD pipeline?
- [ ] Mocks cleared correctly?

---

# 9. Don't List

❌ Do not test against production database.
❌ Do not write huge and complex unit tests.
❌ Do not add meaningless tests just for coverage.
❌ Do not delete failing tests and move on.
❌ Do not duplicate business logic in test code.

---

# 10. Must Do List

✅ Write testable code first (Dependency Injection).
✅ Must test failure scenarios (edge cases).
✅ Regularly review Test Coverage reports.
✅ Fix flaky tests immediately.
✅ Add a test for every bug fix to catch regressions.

---

**Last Update:** December 2025
**Version:** 2.0
