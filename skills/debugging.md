---
name: debugging
description: Sistematik hata ayıklama rehberi. Root cause analysis, debugging metodolojileri ve 2025 araçları.
metadata:
  skillport:
    category: quality
    tags:
      - debugging
      - troubleshooting
      - root-cause-analysis
      - error-handling
---

# Debugging Skill - Sistematik Hata Ayıklama

> Sistematik ve bilimsel yaklaşımla hata ayıklama metodolojisi.
> Problem çözme, root cause analysis ve debugging araçları.

---

# 📋 İçindekiler

1. [Debugging Döngüsü](#1-debugging-döngüsü)
2. [Faz 1: REPRODUCE (Tekrarlama)](#2-faz-1-reproduce-tekrarlama)
3. [Faz 2: UNDERSTAND (Anlama)](#3-faz-2-understand-anlama)
4. [Faz 3: ISOLATE (İzolasyon)](#4-faz-3-isolate-izolasyon)
5. [Faz 4: HYPOTHESIZE (Hipotez)](#5-faz-4-hypothesize-hipotez)
6. [Faz 5: TEST (Test Etme)](#6-faz-5-test-test-etme)
7. [Faz 6: FIX (Düzeltme)](#7-faz-6-fix-düzeltme)
8. [Faz 7: REFLECT (Yansıtma)](#8-faz-7-reflect-yansıtma)
9. [Debugging Araçları](#9-debugging-araçları)
10. [Kontrol Listesi](#10-kontrol-listesi)
11. [Yapma Listesi](#11-yapma-listesi)
12. [Mutlaka Yap Listesi](#12-mutlaka-yap-listesi)

---

# 1. Debugging Döngüsü

```
┌─────────────┐
│  REPRODUCE  │ ← Hatayı tutarlı şekilde tekrarla
└──────┬──────┘
       │
       ▼
┌─────────────┐
│ UNDERSTAND  │ ← Sistemi ve beklenen davranışı anla
└──────┬──────┘
       │
       ▼
┌─────────────┐
│   ISOLATE   │ ← Problemi dar bir alana sıkıştır
└──────┬──────┘
       │
       ▼
┌─────────────┐
│ HYPOTHESIZE │ ← Olası nedenleri listele
└──────┬──────┘
       │
       ▼
┌─────────────┐
│    TEST     │ ← Hipotezleri test et
└──────┬──────┘
       │
       ▼
┌─────────────┐
│     FIX     │ ← Düzelt ve doğrula
└──────┬──────┘
       │
       ▼
┌─────────────┐
│   REFLECT   │ ← Öğrenilenleri belgele
└─────────────┘
```

---

# 2. Faz 1: REPRODUCE (Tekrarlama)

## 2.1 Hatayı Tutarlı Tekrarla

```markdown
## Hata Tekrarlama Raporu

### Gözlemlenen Davranış
- Ne oluyor? [Detaylı açıklama]
- Hata mesajı: [Tam hata metni]
- Ne zaman başladı? [Tarih/commit]

### Tekrarlama Adımları
1. [Adım 1]
2. [Adım 2]
3. [Adım 3]
→ Hata oluşuyor

### Ortam Bilgisi
- OS: [Windows/Mac/Linux versiyonu]
- Node: [Versiyon]
- Browser: [Chrome/Firefox + versiyon]
- Dependencies: [İlgili paket versiyonları]

### Tekrarlanabilirlik
- [ ] Her seferinde oluyor (100%)
- [ ] Sık sık oluyor (~%80)
- [ ] Bazen oluyor (~%50)
- [ ] Nadiren oluyor (~%10)
- [ ] Henüz tekrarlayamadım
```

## 2.2 Tekrarlama İpuçları

```typescript
// Seed kullanarak deterministik test
Math.random = () => 0.5; // Random'ı sabit yap

// Tarih sabitleyerek test
jest.useFakeTimers();
jest.setSystemTime(new Date('2025-01-01'));

// Network koşullarını simüle et
await page.route('**/*', route => route.abort()); // Offline
```

---

# 3. Faz 2: UNDERSTAND (Anlama)

## 3.1 Sistemi Anla

```markdown
## Sistem Haritası

### İlgili Bileşenler
1. [Bileşen A] → [Görevi]
2. [Bileşen B] → [Görevi]
3. [Bileşen C] → [Görevi]

### Veri Akışı
```
User Input → API → Service → Database
     ↓
  Response ← Transform ← Query Result
```

### Beklenen Davranış vs Gerçek Davranış
| Adım | Beklenen | Gerçek |
|------|----------|--------|
| Input | X | X ✅ |
| Process | Y | Z ❌ |
| Output | A | B ❌ |
```

## 3.2 5 Whys Tekniği

```markdown
## 5 Whys Analysis

**Problem:** Kullanıcı login olamıyor

1. **Neden?** → API 401 dönüyor
2. **Neden?** → Token geçersiz
3. **Neden?** → Token expire olmuş
4. **Neden?** → Token yenileme çalışmıyor
5. **Neden?** → Refresh token endpoint'i değişmiş ama client güncellenmemiş

**Root Cause:** API versiyonu güncellendi ama client'ta breaking change handle edilmedi
```

---

# 4. Faz 3: ISOLATE (İzolasyon)

## 4.1 Binary Search ile Hata Bulma

```markdown
## İzolasyon Stratejisi

### Divide and Conquer
1. Sistemin yarısını devre dışı bırak
2. Hata hala var mı?
   - Evet → O yarıda ara
   - Hayır → Diğer yarıda ara
3. Tekrarla: kalan yarıyı ikiye böl
```

```bash
# Git bisect ile hatalı commit bulma
git bisect start
git bisect bad HEAD           # Şu an hatalı
git bisect good v1.0.0        # Bu versiyon düzgündü
# Git otomatik olarak commit'ler arasında binary search yapar
git bisect run npm test       # Otomatik test çalıştır
```

## 4.2 Minimal Reproduction

```typescript
// Büyük uygulamadan minimal örnek çıkar
// ❌ Tüm uygulama ile debug etme

// ✅ Minimal repro oluştur
const minimalExample = () => {
  // Sadece hatayı tetikleyen minimum kod
  const data = { id: null };
  return data.id.toString(); // TypeError burada!
};
```

---

# 5. Faz 4: HYPOTHESIZE (Hipotez)

## 5.1 Olası Nedenleri Listele

```markdown
## Hipotez Listesi

| # | Hipotez | Olasılık | Test Yöntemi |
|---|---------|----------|--------------|
| 1 | Null pointer | %40 | Console.log ile değer kontrol |
| 2 | Race condition | %30 | Timeout ekleyerek test |
| 3 | Cache stale | %20 | Cache temizleyerek test |
| 4 | API değişikliği | %10 | API response kontrol |

### En Olası Hipotez İlk Test Edilmeli
→ Başla: Hipotez #1
```

## 5.2 Common Bug Patterns

| Pattern | Belirtiler | Kontrol Et |
|---------|------------|------------|
| **Null Reference** | TypeError: Cannot read | Değer undefined/null mı? |
| **Off-by-One** | Array out of bounds | İndex hesaplaması |
| **Race Condition** | Intermittent failure | Async sıralama |
| **Memory Leak** | Slow over time | Cleanup yapılıyor mu? |
| **Infinite Loop** | Freeze/hang | Loop koşulu |
| **Wrong Scope** | Unexpected value | Closure/scope |
| **Type Coercion** | `'5' + 5 = '55'` | Strict equality |

---

# 6. Faz 5: TEST (Test Etme)

## 6.1 Debugging Araçları

```typescript
// 1. Console methods
console.log('Value:', value);
console.table(arrayData);
console.group('Section');
console.trace('Stack trace');
console.time('operation');
// ... operation
console.timeEnd('operation');

// 2. Debugger statement
function processData(data) {
  debugger; // Breakpoint
  return transform(data);
}

// 3. Conditional breakpoint (DevTools'da)
// Right-click on line number → Add conditional breakpoint
// Condition: user.role === 'admin'
```

## 6.2 Node.js Debugging

```bash
# Node Inspector
node --inspect src/index.js
# Chrome'da chrome://inspect

# Node Inspector with break
node --inspect-brk src/index.js

# VS Code launch.json
{
  "type": "node",
  "request": "launch",
  "name": "Debug",
  "program": "${workspaceFolder}/src/index.js",
  "skipFiles": ["<node_internals>/**"]
}
```

## 6.3 Network Debugging

```typescript
// Fetch/XHR intercepting
const originalFetch = window.fetch;
window.fetch = async (...args) => {
  console.log('Fetch:', args);
  const response = await originalFetch(...args);
  console.log('Response:', response.status);
  return response;
};

// Axios interceptor
axios.interceptors.request.use(config => {
  console.log('Request:', config);
  return config;
});

axios.interceptors.response.use(
  response => {
    console.log('Response:', response);
    return response;
  },
  error => {
    console.error('Error:', error);
    return Promise.reject(error);
  }
);
```

---

# 7. Faz 6: FIX (Düzeltme)

## 7.1 Fix Stratejisi

```markdown
## Fix Planı

### Root Cause
[Net olarak root cause'u belirt]

### Proposed Fix
[Düzeltme yaklaşımını açıkla]

### Code Changes
```diff
- const value = data.item.value;
+ const value = data?.item?.value ?? 'default';
```

### Verification
- [ ] Bug artık oluşmuyor
- [ ] Yeni bug yaratılmadı (regression)
- [ ] Test yazıldı
- [ ] Edge case'ler kontrol edildi
```

## 7.2 Fix Sonrası Test

```typescript
// Regression test yaz
test('should handle null item in data', () => {
  const data = { item: null };
  expect(() => processData(data)).not.toThrow();
  expect(processData(data)).toBe('default');
});

test('should handle missing item property', () => {
  const data = {};
  expect(() => processData(data)).not.toThrow();
});
```

---

# 8. Faz 7: REFLECT (Yansıtma)

## 8.1 Post-Mortem Dokumentasyonu

```markdown
## Bug Post-Mortem

### Özet
[Hatanın kısa özeti]

### Timeline
- [Tarih] Hata raporlandı
- [Tarih] Root cause bulundu
- [Tarih] Fix deploy edildi

### Root Cause
[Detaylı açıklama]

### Impact
- Etkilenen kullanıcı sayısı: [X]
- Downtime: [Y dakika]
- Revenue impact: [Varsa]

### Lessons Learned
1. [Öğrenilen 1]
2. [Öğrenilen 2]

### Prevention
Bu tür hataları önlemek için:
1. [ ] [Aksiyon 1]
2. [ ] [Aksiyon 2]
```

---

# 9. Debugging Araçları

## 9.1 Static Analysis

```bash
# ESLint ile potansiyel hataları bul
npx eslint . --ext .ts,.tsx

# TypeScript type checking
npx tsc --noEmit

# SonarQube/SonarLint
# VS Code extension veya CI integration
```

## 9.2 Runtime Analysis

```typescript
// Performance profiling
console.profile('myFunction');
myFunction();
console.profileEnd('myFunction');

// Memory snapshot
// Chrome DevTools → Memory → Take heap snapshot

// React DevTools Profiler
// Components tab → Profiler → Record
```

## 9.3 Logging Best Practices

```typescript
// Structured logging
import pino from 'pino';

const logger = pino({
  level: process.env.LOG_LEVEL || 'info',
});

logger.info({ userId, action: 'login' }, 'User logged in');
logger.error({ err, userId }, 'Login failed');

// Log levels
logger.trace('Very detailed');
logger.debug('Debugging info');
logger.info('General info');
logger.warn('Warning');
logger.error('Error');
logger.fatal('Fatal error');
```

---

# 10. Kontrol Listesi

Her debugging session'da:

- [ ] Hata tutarlı şekilde tekrarlandı
- [ ] Sistem ve beklenen davranış anlaşıldı
- [ ] Problem izole edildi
- [ ] Hipotezler listelendi ve önceliklendirildi
- [ ] En olası hipotez ilk test edildi
- [ ] Root cause bulundu
- [ ] Fix uygulandı ve doğrulandı
- [ ] Regression test yazıldı
- [ ] Post-mortem dokümante edildi

---

# 11. Yapma Listesi

❌ Tahminle düzeltmeye çalışma (print debugging loop)
❌ Birden fazla şeyi aynı anda değiştirme
❌ Root cause'u anlamadan fix yapma
❌ Test yazmadan PR açma
❌ Debugging kodunu commit etme (console.log)
❌ Hataları sessizce yutma (empty catch)
❌ Timeout ile "fix" yaptığını sanma

---

# 12. Mutlaka Yap Listesi

✅ Önce tekrarla, sonra debug et
✅ Binary search ile izole et
✅ Hipotezleri yaz ve test et
✅ Bir seferde bir değişiklik yap
✅ Her fix için test yaz
✅ Öğrenilenleri belgele
✅ Stack trace'i dikkatlice oku
✅ Version control kullan (git stash, bisect)

---

**Son Güncelleme:** Aralık 2025
**Versiyon:** 2.0
