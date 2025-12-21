---
name: testing
description: Test-Driven Development rehberi. Unit, integration ve e2e testing için 2025 best practices, test stratejileri ve otomasyon.
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

# Testing Skill - TDD & Test Stratejileri

> Test-Driven Development ve kapsamlı test stratejileri rehberi.
> Güvenilir, maintainable ve hızlı testler yazma metodolojisi.

---

## 🎯 Test Piramidi

```
        /\
       /  \        E2E Tests (Az, yavaş, pahalı)
      /----\       
     /      \      Integration Tests (Orta)
    /--------\     
   /          \    Unit Tests (Çok, hızlı, ucuz)
  /______________\
```

| Seviye | Oran | Hız | Kapsam |
|--------|------|-----|--------|
| **Unit** | ~70% | <10ms | Tek fonksiyon/component |
| **Integration** | ~20% | <1s | Modüller arası |
| **E2E** | ~10% | Saniyeler | Tüm sistem |

---

## 📏 TDD Döngüsü: Red-Green-Refactor

### Adım 1: RED (Fail)
```typescript
// Önce başarısız test yaz
test('should calculate total with tax', () => {
  const result = calculateTotal(100, 0.18);
  expect(result).toBe(118);
});

// ❌ Test FAILS - fonksiyon henüz yok
```

### Adım 2: GREEN (Pass)
```typescript
// Minimum kod yaz - testi geçir
function calculateTotal(amount: number, taxRate: number): number {
  return amount + (amount * taxRate);
}

// ✅ Test PASSES
```

### Adım 3: REFACTOR
```typescript
// Kodu iyileştir - testler hala geçmeli
function calculateTotal(amount: number, taxRate: number): number {
  const tax = amount * taxRate;
  return Number((amount + tax).toFixed(2));
}

// ✅ Test still PASSES
```

---

## 🧪 Unit Testing

### Test Yapısı: AAA Pattern

```typescript
describe('UserService', () => {
  describe('createUser', () => {
    test('should create user with valid data', async () => {
      // ARRANGE - Hazırlık
      const userData = { email: 'test@example.com', name: 'Test User' };
      const mockRepo = { create: jest.fn().mockResolvedValue({ id: '1', ...userData }) };
      const service = new UserService(mockRepo);

      // ACT - İşlem
      const result = await service.createUser(userData);

      // ASSERT - Doğrulama
      expect(result.id).toBe('1');
      expect(result.email).toBe('test@example.com');
      expect(mockRepo.create).toHaveBeenCalledWith(userData);
    });
  });
});
```

### İsimlendirme Kuralları

```typescript
// ✅ DOĞRU - Açıklayıcı test isimleri
test('should return empty array when no users found', () => {});
test('should throw ValidationError when email is invalid', () => {});
test('should calculate discount correctly for premium users', () => {});

// ❌ YANLIŞ - Belirsiz isimler
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
  update: jest.fn(),
  delete: jest.fn(),
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
  expect(mockUserRepository.findById).toHaveBeenCalledTimes(1);
  expect(result).toEqual(mockUser);
});

// Spy kullanımı
test('should log error on failure', async () => {
  const consoleSpy = jest.spyOn(console, 'error').mockImplementation();
  mockUserRepository.findById.mockRejectedValue(new Error('DB Error'));

  await expect(userService.getUser('1')).rejects.toThrow();
  expect(consoleSpy).toHaveBeenCalled();

  consoleSpy.mockRestore();
});
```

### Edge Cases

```typescript
describe('divide function', () => {
  // Happy path
  test('should divide two numbers correctly', () => {
    expect(divide(10, 2)).toBe(5);
  });

  // Edge cases
  test('should throw when dividing by zero', () => {
    expect(() => divide(10, 0)).toThrow('Division by zero');
  });

  test('should handle negative numbers', () => {
    expect(divide(-10, 2)).toBe(-5);
  });

  test('should handle decimal numbers', () => {
    expect(divide(7, 2)).toBe(3.5);
  });

  test('should handle very large numbers', () => {
    expect(divide(Number.MAX_SAFE_INTEGER, 2)).toBeCloseTo(4503599627370496);
  });

  // Boundary cases
  test('should handle zero dividend', () => {
    expect(divide(0, 5)).toBe(0);
  });
});
```

---

## 🔄 Integration Testing

### API Endpoint Testing

```typescript
import request from 'supertest';
import { app } from '../app';
import { prisma } from '../lib/prisma';

describe('POST /api/users', () => {
  beforeEach(async () => {
    await prisma.user.deleteMany();
  });

  afterAll(async () => {
    await prisma.$disconnect();
  });

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
    expect(response.body.data.password).toBeUndefined(); // Password should not be returned
  });

  test('should return 400 for invalid email', async () => {
    const response = await request(app)
      .post('/api/users')
      .send({
        email: 'invalid-email',
        password: 'SecurePass123!',
        name: 'Test User',
      })
      .expect(400);

    expect(response.body.success).toBe(false);
    expect(response.body.error.code).toBe('VALIDATION_ERROR');
  });

  test('should return 409 for duplicate email', async () => {
    // First create a user
    await request(app)
      .post('/api/users')
      .send({
        email: 'test@example.com',
        password: 'SecurePass123!',
        name: 'Test User',
      });

    // Try to create with same email
    const response = await request(app)
      .post('/api/users')
      .send({
        email: 'test@example.com',
        password: 'AnotherPass123!',
        name: 'Another User',
      })
      .expect(409);

    expect(response.body.error.code).toBe('DUPLICATE_EMAIL');
  });
});
```

### Database Integration

```typescript
describe('UserRepository', () => {
  let repository: UserRepository;

  beforeAll(async () => {
    repository = new UserRepository(prisma);
  });

  beforeEach(async () => {
    await prisma.user.deleteMany();
  });

  test('should create and retrieve user', async () => {
    const created = await repository.create({
      email: 'test@example.com',
      name: 'Test',
    });

    const found = await repository.findById(created.id);

    expect(found).not.toBeNull();
    expect(found?.email).toBe('test@example.com');
  });

  test('should handle transactions correctly', async () => {
    await expect(
      prisma.$transaction(async (tx) => {
        await tx.user.create({ data: { email: 'a@test.com', name: 'A' } });
        throw new Error('Force rollback');
      })
    ).rejects.toThrow();

    const count = await prisma.user.count();
    expect(count).toBe(0); // Transaction rolled back
  });
});
```

---

## 🌐 E2E Testing

### Playwright Setup

```typescript
// playwright.config.ts
import { defineConfig } from '@playwright/test';

export default defineConfig({
  testDir: './e2e',
  fullyParallel: true,
  retries: process.env.CI ? 2 : 0,
  workers: process.env.CI ? 1 : undefined,
  reporter: 'html',
  use: {
    baseURL: 'http://localhost:3000',
    trace: 'on-first-retry',
    screenshot: 'only-on-failure',
  },
});
```

### E2E Test Örneği

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

  test('should show error for invalid credentials', async ({ page }) => {
    await page.goto('/login');

    await page.fill('[data-testid="email-input"]', 'wrong@example.com');
    await page.fill('[data-testid="password-input"]', 'wrongpassword');
    await page.click('[data-testid="login-button"]');

    await expect(page.locator('[data-testid="error-message"]')).toBeVisible();
    await expect(page).toHaveURL('/login');
  });
});
```

---

## 🧩 React Component Testing

### Testing Library

```typescript
import { render, screen, fireEvent, waitFor } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { LoginForm } from './LoginForm';

describe('LoginForm', () => {
  const mockOnSubmit = jest.fn();

  beforeEach(() => {
    mockOnSubmit.mockClear();
  });

  test('should render login form', () => {
    render(<LoginForm onSubmit={mockOnSubmit} />);

    expect(screen.getByLabelText(/email/i)).toBeInTheDocument();
    expect(screen.getByLabelText(/password/i)).toBeInTheDocument();
    expect(screen.getByRole('button', { name: /login/i })).toBeInTheDocument();
  });

  test('should submit form with valid data', async () => {
    const user = userEvent.setup();
    render(<LoginForm onSubmit={mockOnSubmit} />);

    await user.type(screen.getByLabelText(/email/i), 'test@example.com');
    await user.type(screen.getByLabelText(/password/i), 'password123');
    await user.click(screen.getByRole('button', { name: /login/i }));

    await waitFor(() => {
      expect(mockOnSubmit).toHaveBeenCalledWith({
        email: 'test@example.com',
        password: 'password123',
      });
    });
  });

  test('should show validation error for invalid email', async () => {
    const user = userEvent.setup();
    render(<LoginForm onSubmit={mockOnSubmit} />);

    await user.type(screen.getByLabelText(/email/i), 'invalid-email');
    await user.click(screen.getByRole('button', { name: /login/i }));

    await waitFor(() => {
      expect(screen.getByText(/valid email/i)).toBeInTheDocument();
    });
    expect(mockOnSubmit).not.toHaveBeenCalled();
  });
});
```

---

## 📊 Test Coverage

### Jest Coverage Config

```javascript
// jest.config.js
module.exports = {
  collectCoverage: true,
  coverageDirectory: 'coverage',
  coverageReporters: ['text', 'lcov', 'html'],
  coverageThreshold: {
    global: {
      branches: 80,
      functions: 80,
      lines: 80,
      statements: 80,
    },
  },
  collectCoverageFrom: [
    'src/**/*.{ts,tsx}',
    '!src/**/*.d.ts',
    '!src/**/*.test.{ts,tsx}',
    '!src/**/index.ts',
  ],
};
```

### Meaningful Coverage

```typescript
// ❌ Sadece coverage için test yazma
test('should exist', () => {
  expect(myFunction).toBeDefined();
});

// ✅ Davranışı test et
test('should calculate correctly', () => {
  expect(myFunction(10, 20)).toBe(30);
  expect(myFunction(-5, 5)).toBe(0);
  expect(myFunction(0, 0)).toBe(0);
});
```

---

## ⚡ CI/CD Integration

```yaml
# .github/workflows/test.yml
name: Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Run linter
        run: npm run lint
      
      - name: Run type check
        run: npm run type-check
      
      - name: Run unit tests
        run: npm run test:unit -- --coverage
      
      - name: Run integration tests
        run: npm run test:integration
      
      - name: Upload coverage
        uses: codecov/codecov-action@v3
```

---

## ✅ Kontrol Listesi

Her test yazarken:

- [ ] Test AAA pattern'i takip ediyor
- [ ] Test ismi açıklayıcı
- [ ] Tek bir şeyi test ediyor (Single Responsibility)
- [ ] Edge case'ler kapsanmış
- [ ] Mocking doğru yapılmış
- [ ] Cleanup (afterEach/afterAll) var
- [ ] Test bağımsız çalışıyor (izole)
- [ ] Flaky test yok (deterministik)
- [ ] Coverage threshold karşılanıyor

---

## 🔴 Yapma Listesi

❌ Implementation detaylarını test etme
❌ Aynı şeyi birden fazla yerde test etme
❌ Test içinde logic yazma
❌ Hard-coded timeout'lar
❌ Test order'a bağımlılık
❌ Dış servislere gerçek istek atma (mock kullan)
❌ Sadece happy path test etme
❌ console.log ile debug'da bırakma

---

## ✅ Mutlaka Yap Listesi

✅ Önce test yaz (TDD)
✅ Edge case'leri düşün
✅ Describe/it blokları ile organize et
✅ Factory pattern ile test data oluştur
✅ CI pipeline'da testleri çalıştır
✅ Coverage raporla
✅ Flaky testleri hemen düzelt
✅ Test helper'lar kullan (renderWithProviders vb.)

---

**Son Güncelleme:** Aralık 2025
**Versiyon:** 1.0
