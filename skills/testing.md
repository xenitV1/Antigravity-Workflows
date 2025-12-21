---
name: testing
description: Kapsamlı test stratejileri ve 2025 test araçları. Unit, integration, e2e ve visual testing.
metadata:
  skillport:
    category: quality
    tags:
      - testing
      - jest
      - playwright
      - quality-assurance
---

# Testing Skill - Kalite Güvence ve Test Stratejileri

> Yazılım kalitesini sağlamak için sistematik test yaklaşımları.
> 2025 modern test araçları ve piramit test stratejisi.

---

# 📋 İçindekiler

1. [Test Piramidi](#1-test-piramidi)
2. [Unit Testing (Jest)](#2-unit-testing-jest)
3. [Integration Testing](#3-integration-testing)
4. [E2E Testing (Playwright)](#4-e2e-testing-playwright)
5. [Visual Regression Testing](#5-visual-regression-testing)
6. [TDD (Test Driven Development)](#6-tdd-test-driven-development)
7. [Test Yazım Kuralları](#7-test-yazım-kuralları)
8. [Kontrol Listesi](#8-kontrol-listesi)
9. [Yapma Listesi](#9-yapma-listesi)
10. [Mutlaka Yap Listesi](#10-mutlaka-yap-listesi)

---

# 1. Test Piramidi

```
      / \
     /E2E\  ← En az (Yavaş, Pahalı, Kırılgan)
    /-----\
   / INTEGR\ ← Orta (Hız ve Güven dengesi)
  /---------\
 /   UNIT    \ ← En çok (Hızlı, Ucuz, İzole)
/-------------\
```

| Tip | Kapsam | Hız | Maliyet |
|-----|--------|-----|---------|
| **Unit** | Fonksiyon/Component | ⚡⚡⚡ | 💸 |
| **Integration** | DB/API/Module arası | ⚡⚡ | 💸💸 |
| **E2E** | Tam kullanıcı akışı | ⚡ | 💸💸💸 |

---

# 2. Unit Testing (Jest)

## 2.1 Temel Test Yapısı

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
// Service mock'lama
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

## 4.1 Login Akışı

```typescript
import { test, expect } from '@playwright/test';

test('user can login successfully', async ({ page }) => {
  await page.goto('/login');
  await page.fill('input[name="email"]', 'user@example.com');
  await page.fill('input[name="password"]', 'password123');
  await page.click('button[type="submit"]');

  await expect(page).toHaveURL('/dashboard');
  await expect(page.locator('h1')).toContainText('Hoş Geldiniz');
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

1. **RED:** Testi yaz ve başarısız olduğunu gör.
2. **GREEN:** Testin geçmesi için gereken minimum kodu yaz.
3. **REFACTOR:** Kodu ve testi temizle, standartlara uygun hale getir.

---

# 7. Test Yazım Kuralları

- **AAA Pattern:** Arrange, Act, Assert.
- **Isolasyon:** Testler birbirinden bağımsız olmalı.
- **Hız:** Unit testler çok hızlı çalışmalı.
- **Readable:** Test ismi neyi test ettiğini açıkça söylemeli.
- **Deterministic:** Aynı girdiyle her zaman aynı sonuç.

---

# 8. Kontrol Listesi

- [ ] Unit testler en az %80 coverage sağlıyor mu?
- [ ] Kritik business logic integration testleri var mı?
- [ ] En önemli 3-4 kullanıcı akışı E2E ile test edildi mi?
- [ ] Testler CI/CD pipeline'da otomatik çalışıyor mu?
- [ ] Mock'lar doğru şekilde temizleniyor mu?

---

# 9. Yapma Listesi

❌ Production veritabanında test yapma.
❌ Çok büyük ve karmaşık unit testler yazma.
❌ Coverage için anlamsız testler ekleme.
❌ Başarısız olan testleri silip geçme.
❌ Test kodunda business logic duplicate etme.

---

# 10. Mutlaka Yap Listesi

✅ Önce test edilebilir kod yaz (Dependency Injection).
✅ Hatalı senaryoları (edge cases) mutlaka test et.
✅ Test Coverage raporlarını düzenli incele.
✅ Flaky testleri (bazen geçen bazen kalan) hemen düzelt.
✅ Her bug fix için o bug'ı yakalayan bir test ekle.

---

**Son Güncelleme:** Aralık 2025
**Versiyon:** 2.0
