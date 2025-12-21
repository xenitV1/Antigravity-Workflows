---
name: refactoring
description: Güvenli kod yeniden yapılandırma rehberi. Behavior preservation, incremental changes ve 2025 refactoring patterns.
metadata:
  skillport:
    category: quality
    tags:
      - refactoring
      - code-quality
      - clean-code
      - technical-debt
---

# Refactoring Skill - Güvenli Kod İyileştirme

> Mevcut kodu bozmadan iyileştirme metodolojisi.
> Behavior preservation, incremental changes ve test-first refactoring.

---

# 📋 İçindekiler

1. [Refactoring Altın Kuralı](#1-refactoring-altın-kuralı)
2. [Ne Zaman Refactor?](#2-ne-zaman-refactor)
3. [Refactoring Süreci](#3-refactoring-süreci)
4. [Common Refactoring Patterns](#4-common-refactoring-patterns)
5. [Code Smells](#5-code-smells)
6. [Safe Refactoring Checklist](#6-safe-refactoring-checklist)
7. [Incremental Refactoring Strategy](#7-incremental-refactoring-strategy)
8. [Kontrol Listesi](#8-kontrol-listesi)
9. [Yapma Listesi](#9-yapma-listesi)
10. [Mutlaka Yap Listesi](#10-mutlaka-yap-listesi)

---

# 1. Refactoring Altın Kuralı

> **"Refactoring davranışı DEĞİŞTİRMEZ, sadece yapıyı iyileştirir"**

```
Before Refactoring:
  Input: X → [Code A] → Output: Y

After Refactoring:
  Input: X → [Code B] → Output: Y  (AYNI Output!)
```

---

# 2. Ne Zaman Refactor?

## 2.1 Refactor Zamanı

| Sinyal | Örnek |
|--------|-------|
| **Code Smell** | Duplicate code, long method, large class |
| **Boy Scout Rule** | "Kodu bulduğundan daha temiz bırak" |
| **Before adding feature** | Yeni özellik eklemeden önce zemin hazırla |
| **After fixing bug** | Bug fix sonrası kodu iyileştir |
| **Code review feedback** | İyileştirme önerileri alındığında |

## 2.2 Refactor Etme Zamanı DEĞİL

| Durum | Neden? |
|-------|--------|
| ❌ Deadline çok yakın | Risk çok yüksek |
| ❌ Test coverage düşük | Güvenlik ağı yok |
| ❌ Sistemi anlamadan | Yanlış yere müdahale |
| ❌ Feature ile birlikte | Ayrı commit'lerde yap |

---

# 3. Refactoring Süreci

## 3.1 Adım 1: Güvenlik Ağı Oluştur

```typescript
// Mevcut davranışı belgele ve test et
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

## 3.2 Adım 2: Küçük Adımlarla İlerle

```typescript
// ❌ YANLIŞ: Büyük değişiklik
// Tüm dosyayı sil ve yeniden yaz

// ✅ DOĞRU: Küçük adımlar
// Commit 1: Extract helper function
// Commit 2: Rename variables
// Commit 3: Simplify conditionals
// Commit 4: Remove duplication
```

## 3.3 Adım 3: Her Adımda Test Çalıştır

```bash
# Her küçük değişiklikten sonra
npm test

# Testler geçtiyse commit
git add .
git commit -m "refactor: extract calculateItemTotal helper"

# Sonraki adıma geç
```

---

# 4. Common Refactoring Patterns

## 4.1 Extract Function

```typescript
// ❌ ÖNCE: Long function
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

// ✅ SONRA: Extracted functions
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
// ❌ ÖNCE: Switch statement
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

// ✅ SONRA: Strategy pattern
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
// ❌ ÖNCE
if (user.age >= 18) { /* ... */ }
const tax = amount * 0.18;
if (retryCount > 3) { /* ... */ }

// ✅ SONRA
const LEGAL_AGE = 18;
const TAX_RATE = 0.18;
const MAX_RETRY_COUNT = 3;

if (user.age >= LEGAL_AGE) { /* ... */ }
const tax = amount * TAX_RATE;
if (retryCount > MAX_RETRY_COUNT) { /* ... */ }
```

## 4.4 Simplify Conditionals

```typescript
// ❌ ÖNCE: Nested conditionals
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

// ✅ SONRA: Early return + table
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
// ❌ ÖNCE: Duplicated code
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

// ✅ SONRA: Extracted common logic
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

| Smell | Belirti | Çözüm |
|-------|---------|-------|
| **Long Method** | >20 satır | Extract Method |
| **Large Class** | >300 satır | Extract Class |
| **Long Parameter List** | >3 param | Introduce Parameter Object |
| **Duplicate Code** | Copy-paste | Extract Method/Class |
| **Feature Envy** | Başka class'ın verisiyle çok çalışma | Move Method |
| **Data Clumps** | Hep beraber gezen veriler | Extract Class |
| **Primitive Obsession** | String/number yerine object | Value Object |
| **Switch Statements** | Çok switch/if-else | Polymorphism |
| **Parallel Inheritance** | Her yeni class'ta ikizini yaratma | Inheritance refactor |
| **Dead Code** | Kullanılmayan kod | Remove |

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
- [ ] Test coverage yeterli mi? (minimum %80)
- [ ] Tüm testler geçiyor mu?
- [ ] CI/CD pipeline yeşil mi?

### Understanding
- [ ] Mevcut kodu anlıyor muyum?
- [ ] Edge case'leri biliyor muyum?
- [ ] Bağımlılıkları haritaladım mı?

### Planning
- [ ] Hangi refactoring pattern uygulayacağım?
- [ ] Adımları planladım mı?
- [ ] Rollback stratejim var mı?

### Communication
- [ ] Takımı bilgilendirdim mi?
- [ ] Code freeze var mı?
```

## 6.2 During Refactoring

```markdown
## During Refactoring

- [ ] Küçük adımlarla ilerliyorum
- [ ] Her adımda test çalıştırıyorum
- [ ] Her başarılı adımı commit ediyorum
- [ ] Feature eklemiyorum (sadece refactor)
- [ ] Bug fix yapmıyorum (sadece refactor)
```

## 6.3 After Refactoring

```markdown
## Post-Refactoring

- [ ] Tüm testler geçiyor
- [ ] Lint hata yok
- [ ] Type error yok
- [ ] Performance regresyon yok
- [ ] Code review istendi
- [ ] Documentation güncellendi
```

---

# 7. Incremental Refactoring Strategy

## 7.1 Strangler Fig Pattern

```typescript
// Eski kodu sarmala, yavaşça yenisiyle değiştir

// Step 1: Wrapper oluştur
class UserServiceWrapper {
  private legacyService: LegacyUserService;
  private newService: NewUserService;

  async getUser(id: string) {
    // Başta legacy kullan
    return this.legacyService.getUser(id);
  }
}

// Step 2: Feature flag ile yönlendir
async getUser(id: string) {
  if (featureFlags.useNewUserService) {
    return this.newService.getUser(id);
  }
  return this.legacyService.getUser(id);
}

// Step 3: Tamamen geçiş
async getUser(id: string) {
  return this.newService.getUser(id);
}

// Step 4: Legacy'yi kaldır
```

---

# 8. Kontrol Listesi

Her refactoring'de:

- [ ] Yeterli test coverage var
- [ ] Mevcut davranış belgelendi
- [ ] Küçük adımlarla ilerleniyor
- [ ] Her adım ayrı commit
- [ ] Testler her adımda geçiyor
- [ ] Feature eklenmedi
- [ ] Bug fix yapılmadı
- [ ] Performance kontrol edildi
- [ ] Code review yapıldı

---

# 9. Yapma Listesi

❌ Test olmadan refactor
❌ Büyük değişiklikleri tek seferde
❌ Refactor + feature aynı PR'da
❌ Refactor + bugfix aynı commit'te
❌ Davranışı değiştiren "refactor"
❌ Anlamadan refactor
❌ Deadline'da refactor

---

# 10. Mutlaka Yap Listesi

✅ Önce test yaz veya mevcut testleri doğrula
✅ Mevcut davranışı anla
✅ Küçük adımlarla ilerle
✅ Her adımda test çalıştır
✅ Her adımı ayrı commit et
✅ Rollback stratejin olsun
✅ Code review al
✅ Performance'ı ölç

---

**Son Güncelleme:** Aralık 2025
**Versiyon:** 2.0
