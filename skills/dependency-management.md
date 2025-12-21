---
name: dependency-management
description: Paket ve bağımlılık yönetimi rehberi. Security audit, version management ve upgrade stratejileri.
metadata:
  skillport:
    category: operations
    tags:
      - npm
      - dependencies
      - security
      - versioning
---

# Dependency Management Skill

> Güvenli ve sürdürülebilir bağımlılık yönetimi rehberi.
> Security auditing, version control ve upgrade stratejileri.

---

# 📋 İçindekiler

1. [Temel Prensipler](#1-temel-prensipler)
2. [Paket Ekleme Kararı](#2-paket-ekleme-kararı)
3. [Security Auditing](#3-security-auditing)
4. [Version Management](#4-version-management)
5. [Upgrade Stratejisi](#5-upgrade-stratejisi)
6. [Lock File Yönetimi](#6-lock-file-yönetimi)
7. [Dependency Cleanup](#7-dependency-cleanup)
8. [Dependency Monitoring](#8-dependency-monitoring)
9. [Kontrol Listesi](#9-kontrol-listesi)
10. [Yapma Listesi](#10-yapma-listesi)
11. [Mutlaka Yap Listesi](#11-mutlaka-yap-listesi)

---

# 1. Temel Prensipler

| Prensip | Açıklama |
|---------|----------|
| **Minimize Dependencies** | Gereksiz paket ekleme |
| **Lock Versions** | package-lock.json commit'le |
| **Audit Regularly** | Haftalık security check |
| **Update Strategically** | Major updates dikkatli |
| **Document Decisions** | Neden bu paket? |

---

# 2. Paket Ekleme Kararı

## 2.1 Paket Eklemeden Önce

```markdown
## Paket Değerlendirme Checklist

### Gerçekten Gerekli mi?
- [ ] Native çözüm var mı? (built-in modules)
- [ ] Basit bir util ile yapılabilir mi?
- [ ] Proje boyutuna değer mi?

### Paket Kalitesi
- [ ] Weekly downloads: >10K
- [ ] GitHub stars: >1K
- [ ] Son commit: <6 ay
- [ ] Open issues reasonable
- [ ] Maintainer aktif

### Güvenlik
- [ ] npm audit temiz
- [ ] Snyk/Dependabot taraması
- [ ] Bilinen vulnerabilities yok
- [ ] Dependency chain küçük

### Lisans
- [ ] MIT / Apache 2.0 / ISC (uyumlu)
- [ ] GPL değil (commercial projeler için)
```

## 2.2 Paket Karşılaştırma

```markdown
## Paket Karşılaştırma: Date Library

| Kriter | date-fns | dayjs | moment |
|--------|----------|-------|--------|
| Size (gzip) | 13KB | 2KB | 72KB |
| Tree-shakeable | ✅ | ❌ | ❌ |
| Immutable | ✅ | ✅ | ❌ |
| TypeScript | ✅ | ✅ | ✅ |
| Maintenance | ✅ | ✅ | ⚠️ Deprecated |

**Karar:** dayjs (en küçük, aktif bakım)
```

---

# 3. Security Auditing

## 3.1 npm audit

```bash
# Güvenlik taraması
npm audit

# Otomatik fix (dikkatli!)
npm audit fix

# Breaking changes dahil fix
npm audit fix --force  # ⚠️ TEHLİKELİ

# JSON formatında (CI için)
npm audit --json

# Production dependencies only
npm audit --omit=dev
```

## 3.2 Audit Raporunu Anlama

```
┌───────────────┬──────────────────────────────────────────────────────┐
│ Critical      │ eval injection in lodash < 4.17.21                    │
| Package       │ lodash                                                |
| Severity      │ critical                                              |
| Vulnerable    │ <4.17.21                                              |
| Patched in    │ >=4.17.21                                             |
| Dependency of │ my-project > some-package > lodash                    |
└───────────────┴──────────────────────────────────────────────────────┘
```

## 3.3 Snyk Integration

```bash
# Snyk CLI kurulumu
npm install -g snyk

# Auth
snyk auth

# Test
snyk test

# Monitor (continuous)
snyk monitor

# Fix önerileri
snyk wizard
```

## 3.4 CI Pipeline'da Audit

```yaml
# .github/workflows/security.yml
name: Security Audit

on:
  push:
    branches: [main]
  schedule:
    - cron: '0 0 * * 1'  # Her Pazartesi

jobs:
  audit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: npm audit
        run: npm audit --audit-level=high
        
      - name: Snyk scan
        uses: snyk/actions/node@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
```

---

# 4. Version Management

## 4.1 Semantic Versioning

```
MAJOR.MINOR.PATCH
  │      │     │
  │      │     └── Backward compatible bug fixes
  │      └──────── Backward compatible new features
  └─────────────── Breaking changes
```

## 4.2 Version Range Syntax

```json
{
  "dependencies": {
    "exact": "1.2.3",           // Tam bu versiyon
    "patch": "~1.2.3",          // 1.2.x (>=1.2.3 <1.3.0)
    "minor": "^1.2.3",          // 1.x.x (>=1.2.3 <2.0.0) [DEFAULT]
    "any": "*",                 // Herhangi (TEHLİKELİ!)
    "range": ">=1.2.3 <2.0.0",  // Explicit range
    "latest": "latest"          // Son stable (TEHLİKELİ!)
  }
}
```

## 4.3 Önerilen Yaklaşım

```json
{
  "dependencies": {
    // Production: Daha conservative
    "express": "^4.18.2",      // Minor updates OK
    "prisma": "~5.6.0",        // Sadece patch
    
    // Security-critical: Lock
    "jsonwebtoken": "9.0.2"    // Exact version
  },
  "devDependencies": {
    // Dev: Daha liberal
    "typescript": "^5.0.0",
    "eslint": "^8.0.0"
  }
}
```

---

# 5. Upgrade Stratejisi

## 5.1 Düzenli Minor Updates

```bash
# Outdated paketleri göster
npm outdated

# Interactive update
npx npm-check -u

# Sadece patch/minor (güvenli)
npm update

# Tüm paketleri son minor'a
npx npm-check-updates -u --target minor
npm install
```

## 5.2 Major Updates (Dikkatli!)

```markdown
## Major Update Checklist: package@X.0.0

### Hazırlık
- [ ] CHANGELOG okuyun
- [ ] Migration guide var mı?
- [ ] Breaking changes listesi

### Uygulama
- [ ] Branch oluştur
- [ ] Package update
- [ ] Type errors fix
- [ ] Runtime errors fix
- [ ] Tests güncelle
- [ ] All tests pass

### Doğrulama
- [ ] Smoke test
- [ ] Critical paths test
- [ ] Performance check
- [ ] Code review
```

## 5.3 Major Update Örneği

```bash
# 1. Branch oluştur
git checkout -b upgrade/react-19

# 2. Package update
npm install react@19 react-dom@19

# 3. TypeScript uyarılarını kontrol et
npx tsc --noEmit

# 4. Testleri çalıştır
npm test

# 5. Breaking changes'i düzelt
# ... kod değişiklikleri ...

# 6. Tekrar test
npm test

# 7. Build
npm run build

# 8. Commit & PR
git commit -m "chore: upgrade react to v19"
```

---

# 6. Lock File Yönetimi

## 6.1 package-lock.json

```bash
# Zorunlu olarak lock file'dan install
npm ci  # CI/CD'de kullan (npm install yerine)

# Lock file regenerate
rm package-lock.json
npm install

# Lock file integrity check
npm audit signatures
```

## 6.2 .npmrc Ayarları

```ini
# .npmrc
save-exact=true              # Exact versions by default
package-lock=true            # Always generate lock file
audit=true                   # Auto audit on install
fund=false                   # Hide funding messages
engine-strict=true           # Enforce engine requirements
```

---

# 7. Dependency Cleanup

## 7.1 Kullanılmayan Paketleri Bul

```bash
# depcheck kurulumu
npm install -g depcheck

# Kullanılmayan paketleri bul
depcheck

# Sonur:
Unused dependencies
* lodash
* moment

Unused devDependencies
* @types/express
```

## 7.2 Paket Boyutu Analizi

```bash
# Bundle size analysis
npx source-map-explorer dist/main.js

# Import cost (VS Code extension)
# Her import'un boyutunu gösterir

# bundlephobia.com
# Paket boyutlarını online kontrol
```

## 7.3 Cleanup Script

```bash
# Gereksiz paketleri kaldır
npm uninstall lodash moment

# node_modules temizle ve yeniden install
rm -rf node_modules
npm ci

# Cache temizle
npm cache clean --force
```

---

# 8. Dependency Monitoring

## 8.1 Dependabot Config

```yaml
# .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: npm
    directory: "/"
    schedule:
      interval: weekly
      day: monday
      time: "09:00"
    open-pull-requests-limit: 10
    versioning-strategy: increase
    labels:
      - dependencies
    ignore:
      - dependency-name: "*"
        update-types: ["version-update:semver-major"]
    groups:
      dev-dependencies:
        dependency-type: development
```

## 8.2 Renovate Config

```json
// renovate.json
{
  "extends": ["config:base"],
  "packageRules": [
    {
      "matchUpdateTypes": ["minor", "patch"],
      "automerge": true
    },
    {
      "matchUpdateTypes": ["major"],
      "labels": ["breaking-change"]
    }
  ],
  "schedule": ["every weekend"]
}
```

---

# 9. Kontrol Listesi

### Paket Eklerken
- [ ] Gerçekten gerekli mi?
- [ ] Alternatifler değerlendirildi mi?
- [ ] Paket kalitesi yeterli mi?
- [ ] Security audit temiz mi?
- [ ] Lisans uyumlu mi?
- [ ] Bundle size kabul edilebilir mi?

### Düzenli Bakım (Haftalık)
- [ ] npm audit çalıştır
- [ ] Dependabot PR'larını review et
- [ ] Outdated paketleri kontrol et

### Major Upgrade
- [ ] CHANGELOG oku
- [ ] Breaking changes listele
- [ ] Branch'te test et
- [ ] Full test suite çalıştır
- [ ] Performance kontrol et

---

# 10. Yapma Listesi

❌ npm install --save ile "*" veya "latest" kullanma
❌ package-lock.json'ı .gitignore'a ekleme
❌ npm audit fix --force körü körüne çalıştırma
❌ Major update'leri test etmeden deploy etme
❌ Deprecated paketleri uzun süre tutma
❌ node_modules'ı commit'leme

---

# 11. Mutlaka Yap Listesi

✅ package-lock.json'ı commit et
✅ CI'da `npm ci` kullan (npm install değil)
✅ Haftalık npm audit çalıştır
✅ Dependabot/Renovate kullan
✅ Major updates için ayrı branch
✅ Kullanılmayan paketleri temizle
✅ Bundle size'ı izle

---

**Son Güncelleme:** Aralık 2025
**Versiyon:** 2.0
