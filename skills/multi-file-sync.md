---
name: multi-file-sync
description: Çoklu dosya değişikliği ve bağlam koruma rehberi. Atomik değişiklikler, refactoring across files ve safe migration.
metadata:
  skillport:
    category: operations
    tags:
      - multi-file
      - refactoring
      - migration
      - context
---

# Multi-File Sync Skill

> Birden fazla dosyayı güvenli ve tutarlı şekilde değiştirme rehberi.
> Atomik adımlar, bağlam koruma ve rollback stratejileri.

---

## 📏 Temel Prensipler

### 1. Atomik Değişiklikler

```markdown
## Atomik Değişiklik Kuralı

Her commit TEK bir mantıksal değişiklik içermeli:

✅ DOĞRU:
- Commit 1: "rename: userId -> customerId in types"
- Commit 2: "rename: userId -> customerId in services"
- Commit 3: "rename: userId -> customerId in controllers"

❌ YANLIŞ:
- Commit 1: "refactor everything" (tüm değişiklikler tek commit'te)
```

### 2. Test-First Yaklaşım

```bash
# Her adımdan önce ve sonra testleri çalıştır
npm test

# Adım yap
# ... değişiklik ...

# Tekrar test et
npm test

# Geçtiyse commit
git commit -m "step X: description"
```

### 3. Bağımlılık Sıralaması

```markdown
## Değişiklik Sırası

Bağımlılık yönünde ilerle:

1. Types/Interfaces (en bağımsız)
2. Utilities/Helpers
3. Services/Repositories
4. Controllers/Handlers
5. Routes/Entry points
6. Tests
7. Documentation
```

---

## 🔄 Multi-File Değişiklik Süreci

### Faz 1: Analiz ve Planlama

```markdown
## Değişiklik Planı

### Etki Analizi
Değişiklik: [Ne değişecek]

### Etkilenen Dosyalar
1. `src/types/user.ts` - Type tanımı
2. `src/services/userService.ts` - Service layer
3. `src/controllers/userController.ts` - Controller
4. `src/routes/userRoutes.ts` - Routes
5. `tests/user.test.ts` - Tests

### Bağımlılık Grafiği
```
types/user.ts
     │
     ├── services/userService.ts
     │        │
     │        └── controllers/userController.ts
     │                     │
     │                     └── routes/userRoutes.ts
     │
     └── tests/user.test.ts
```

### Risk Değerlendirmesi
- Breaking change: [Evet/Hayır]
- Downtime gerekli: [Evet/Hayır]
- Rollback planı: [Strateji]
```

### Faz 2: Hazırlık

```bash
# 1. Temiz branch oluştur
git checkout -b feature/rename-user-to-customer

# 2. Çalışan durumu doğrula
npm test
npm run build
npm run lint

# 3. Backup/stash (güvenlik için)
git stash push -m "backup before big refactor"
```

### Faz 3: Adım Adım Uygulama

```typescript
// ADIM 1: Type tanımını değiştir
// src/types/user.ts
// ❌ Eski
interface User {
  userId: string;
  name: string;
}

// ✅ Yeni
interface User {
  customerId: string;  // userId -> customerId
  name: string;
}

// Commit: "rename: userId -> customerId in User interface"
```

```typescript
// ADIM 2: Service'i güncelle
// src/services/userService.ts
export async function getUser(customerId: string) { // userId -> customerId
  return db.user.findUnique({
    where: { customerId } // userId -> customerId
  });
}

// Commit: "rename: userId -> customerId in userService"
```

```typescript
// ADIM 3: Controller'ı güncelle
// Commit: "rename: userId -> customerId in userController"

// ADIM 4: Route'ları güncelle
// Commit: "rename: userId -> customerId in routes"

// ADIM 5: Testleri güncelle
// Commit: "rename: userId -> customerId in tests"
```

### Faz 4: Doğrulama

```bash
# Tüm kontrolleri çalıştır
npm run lint
npm run type-check
npm test
npm run build

# Eğer hepsi geçtiyse
git push origin feature/rename-user-to-customer
```

---

## 🛠️ Araçlar ve Teknikler

### IDE Refactoring (Rename Symbol)

```typescript
// VS Code / WebStorm
// F2 veya Sağ tık -> Rename Symbol

// Tüm kullanım yerlerini otomatik günceller
// AMA: Sadece TypeScript/JavaScript referansları
// String içindeki kullanımları bulamaz!
```

### Grep ile Kontrol

```bash
# Tüm kullanım yerlerini bul
grep -r "userId" --include="*.ts" --include="*.tsx" src/

# Case insensitive
grep -ri "userid" src/

# Exclude directories
grep -r "userId" --exclude-dir={node_modules,dist} .
```

### Find and Replace (Dikkatli!)

```bash
# Sed ile replace (DIKKATLI KULLAN!)
# Önce preview
grep -r "oldName" src/

# Sonra replace
find src -type f -name "*.ts" -exec sed -i 's/oldName/newName/g' {} +

# UYARI: Sed kör değiştirme yapar, yanlış eşleşmeler olabilir!
```

### TypeScript ile Otomatik Tespit

```bash
# Type error'ları göster
npx tsc --noEmit

# Watch modunda
npx tsc --noEmit --watch
```

---

## 🔍 Bağlam Koruma (Context Keeping)

### Çalışma Durumunu Belgele

```markdown
## Progress Tracker

### Tamamlanan Adımlar
- [x] Types güncellendi
- [x] Services güncellendi
- [ ] Controllers güncellendi
- [ ] Routes güncellendi
- [ ] Tests güncellendi

### Şu Anki Adım
Controllers'da `userId` -> `customerId` değişikliği

### Bekleyen Sorunlar
- [ ] Legacy API backward compatibility
- [ ] Database migration gerekebilir

### Notlar
- userController.ts'de 3 yerde userId var
- Biri query param, ikisi body'de
```

### Git Stash Kullanımı

```bash
# Yarım kalan işi kaydet
git stash push -m "WIP: userId rename, controllers kaldı"

# Stash listele
git stash list

# Geri al
git stash pop

# Belirli stash'i geri al
git stash apply stash@{0}
```

### Branch Stratejisi

```bash
# Feature branch
git checkout -b refactor/rename-userid

# Ara commit'ler
git commit -m "WIP: types done"
git commit -m "WIP: services done"

# Squash before merge (optional)
git rebase -i main
# Mark WIP commits as "squash"
```

---

## ⚠️ Tehlikeli Durumlar

### Breaking Change Detection

```typescript
// API değişikliği = Breaking change
// ÖNCE: /users/:userId
// SONRA: /users/:customerId

// Çözüm 1: Hem eski hem yeni destekle
router.get('/users/:userId', handleByUserId);
router.get('/users/:customerId', handleByCustomerId);

// Çözüm 2: Aliasing
router.get('/users/:id', (req) => {
  const id = req.params.id; // Generic isim
});
```

### Database Column Rename

```sql
-- TEHLIKELI: Direkt rename
ALTER TABLE users RENAME COLUMN user_id TO customer_id;
-- ❌ Eski kod kırılır!

-- GÜVENLİ: Expand and Contract pattern
-- Step 1: Yeni column ekle
ALTER TABLE users ADD COLUMN customer_id UUID;
UPDATE users SET customer_id = user_id;

-- Step 2: Kodu güncelle (her iki column'u destekle)

-- Step 3: Eski column'u kaldır (kod tamamen geçtikten sonra)
ALTER TABLE users DROP COLUMN user_id;
```

---

## 🔙 Rollback Stratejileri

### Git Revert

```bash
# Belirli commit'i geri al
git revert <commit-hash>

# Range revert
git revert HEAD~3..HEAD

# Merge'i revert
git revert -m 1 <merge-commit>
```

### Partial Rollback

```bash
# Sadece belirli dosyayı eski haline getir
git checkout HEAD~1 -- src/services/userService.ts

# Belirli commit'teki versiyona
git checkout abc123 -- src/services/userService.ts
```

---

## ✅ Kontrol Listesi

### Başlamadan Önce
- [ ] Etkilenen dosyalar listelendi
- [ ] Bağımlılık sırası belirlendi
- [ ] Testler çalışıyor
- [ ] Temiz git state

### Her Adımda
- [ ] Tek mantıksal değişiklik
- [ ] Testler geçiyor
- [ ] Type check geçiyor
- [ ] Ayrı commit yapıldı

### Tamamlandıktan Sonra
- [ ] Tüm testler geçiyor
- [ ] Build başarılı
- [ ] Lint temiz
- [ ] Code review alındı
- [ ] Documentation güncellendi

---

## 🔴 Yapma Listesi

❌ Tüm değişiklikleri tek commit'te yapma
❌ Test çalıştırmadan devam etme
❌ Bağımlılık sırasını atlama
❌ Elle string replace (grep + sed) güvenilmez
❌ Database column rename + code change aynı deployment'ta

---

## ✅ Mutlaka Yap Listesi

✅ Etki analizini yap ve belgele
✅ Bağımlılık sırasına göre ilerle
✅ Her adımda test çalıştır
✅ Her adımı ayrı commit et
✅ IDE refactoring araçlarını kullan
✅ Grep ile kontrol et
✅ TypeScript hataları sıfır olmalı
✅ Rollback planın olsun

---

**Son Güncelleme:** Aralık 2025
**Versiyon:** 1.0
