---
name: testing
description: Test-Driven Development guide. 2025 best practices, test strategies, and automation for unit, integration, and e2e testing.
metadata:
  skillport:
    category: quality
    tags:
      - tdd
      - unit-testing
      - integration-testing
      - e2e
      - jest
      - vitest
---

# Testing Skill - TDD & Test Strategies

> Guide for Test-Driven Development and comprehensive test strategies.
> Methodology for writing reliable, maintainable, and fast tests.

---

## 🎯 Test Pyramid

```
        /\
       /  \        E2E Tests (Few, slow, expensive)
      /----\       
     /      \      Integration Tests (Medium)
    /--------\     
   /          \    Unit Tests (Many, fast, cheap)
  /______________\
```

| Level | Ratio | Speed | Scope |
|--------|------|-----|--------|
| **Unit** | ~70% | <10ms | Single function/component |
| **Integration** | ~20% | <1s | Between modules |
| **E2E** | ~10% | Seconds | Entire system |

---

## 📏 TDD Cycle: Red-Green-Refactor

### Step 1: RED (Fail)
```typescript
// Write a failing test first
test('should calculate total with tax', () => {
  const result = calculateTotal(100, 0.18);
  expect(result).toBe(118);
});

// ❌ Test FAILS - function does not exist yet
```

### Step 2: GREEN (Pass)
```typescript
// Write minimum code to pass the test
function calculateTotal(amount: number, taxRate: number): number {
  return amount + (amount * taxRate);
}

// ✅ Test PASSES
```

### Step 3: REFACTOR
```typescript
// Improve code - tests should still pass
function calculateTotal(amount: number, taxRate: number): number {
  const tax = amount * taxRate;
  return Number((amount + tax).toFixed(2));
}

// ✅ Test still PASSES
```

---

## 🧪 Unit Testing

### Test Structure: AAA Pattern

```typescript
describe('UserService', () => {
  describe('createUser', () => {
    test('should create user with valid data', async () => {
      // ARRANGE
      const userData = { email: 'test@example.com', name: 'Test User' };
      const mockRepo = { create: jest.fn().mockResolvedValue({ id: '1', ...userData }) };
      const service = new UserService(mockRepo);

      // ACT
      const result = await service.createUser(userData);

      // ASSERT
      expect(result.id).toBe('1');
      expect(result.email).toBe('test@example.com');
      expect(mockRepo.create).toHaveBeenCalledWith(userData);
    });
  });
});
```

### Naming Conventions

```typescript
// ✅ CORRECT - Descriptive test names
test('should return empty array when no users found', () => {});
test('should throw ValidationError when email is invalid', () => {});
test('should calculate discount correctly for premium users', () => {});

// ❌ INCORRECT - Vague names
test('test1', () => {});
test('createUser works', () => {});
test('error case', () => {});
```

### Mocking Best Practices

```typescript
// Mock setup
const mockUserRepository = {
  findById: jest.fn(),
  create: jest.fn(),
};

beforeEach(() => {
  jest.clearAllMocks();
});

test('should get user by id', async () => {
  // Arrange
  const mockUser = { id: '1', name: 'John' };
  mockUserRepository.findById.mockResolvedValue(mockUser);

  // Act
  const result = await userService.getUser('1');

  // Assert
  expect(mockUserRepository.findById).toHaveBeenCalledWith('1');
  expect(result).toEqual(mockUser);
});
```

---

## 🔄 Integration Testing

### API Endpoint Testing

```typescript
import request from 'supertest';
import { app } from '../app';

describe('POST /api/users', () => {
  test('should create user with valid data', async () => {
    const response = await request(app)
      .post('/api/users')
      .send({
        email: 'test@example.com',
        password: 'SecurePass123!',
        name: 'Test User',
      })
      .expect(201);

    expect(response.body.success).toBe(true);
    expect(response.body.data.email).toBe('test@example.com');
  });
});
```

---

## 🌐 E2E Testing

### Playwright Example

```typescript
import { test, expect } from '@playwright/test';

test.describe('User Authentication', () => {
  test('should login with valid credentials', async ({ page }) => {
    await page.goto('/login');

    await page.fill('[data-testid="email-input"]', 'user@example.com');
    await page.fill('[data-testid="password-input"]', 'SecurePass123!');
    await page.click('[data-testid="login-button"]');

    await expect(page).toHaveURL('/dashboard');
    await expect(page.locator('[data-testid="welcome-message"]')).toContainText('Welcome');
  });
});
```

---

## 🧩 React Component Testing

```typescript
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';

describe('LoginForm', () => {
  test('should render login form', () => {
    render(<LoginForm onSubmit={jest.fn()} />);

    expect(screen.getByLabelText(/email/i)).toBeInTheDocument();
    expect(screen.getByRole('button', { name: /login/i })).toBeInTheDocument();
  });
});
```

---

## ✅ Checklist

While writing tests:

- [ ] Test follows AAA pattern
- [ ] Test name is descriptive
- [ ] Tests a single thing (Single Responsibility)
- [ ] Edge cases covered
- [ ] Mocking performed correctly
- [ ] Cleanup present (afterEach/afterAll)
- [ ] Test runs independently (isolated)
- [ ] No flaky tests (deterministic)
- [ ] Coverage threshold met

---

## 🔴 Don't List

❌ Do not test implementation details
❌ Do not test the same thing in multiple places
❌ Do not write logic inside tests
❌ Do not use hard-coded timeouts
❌ Do not depend on test order
❌ Do not make real requests to external services (use mocks)
❌ Do not only test the happy path
❌ Do not leave debug console.logs

---

## ✅ Must Do List

✅ Write tests first (TDD)
✅ Consider edge cases
✅ Organize with describe/it blocks
✅ Use factory pattern to create test data
✅ Run tests in CI pipeline
✅ Report coverage
✅ Fix flaky tests immediately
✅ Use test helpers (renderWithProviders etc.)

---

**Last Update:** December 2025
**Version:** 1.0
