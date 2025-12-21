---
description: Central Orchestrator & Skills Registry. Loads automatically to route tasks to the appropriate Skills, Modes, or Guards.
---

# CORE.md - Skills Orchestrator

> Bu dosya tüm görevler için merkezi yönlendirme noktasıdır.
> Görev tipine göre uygun skill(ler) belirlenir ve yüklenir.

---

## 🎯 Skills Referansı - Ne Zaman Hangi Skill?

> [!NOTE]
> **Dinamik Eşleştirme:** Kullanıcılar aşağıdaki örneklere birebir uymayan şekilde komut verebilir.
> Bu tablolar **referans** niteliğindedir. Agent olarak, kullanıcının talebini analiz et ve
> **semantik olarak en uygun skill(ler)i dinamik şekilde çıkarım yaparak** belirle.
> Örneğin "şu API'de sorun var" → debugging + backend skill'leri gerektirebilir.

---

### 🧠 UltraThink - Derin Düşünme Protokolü

**Dosya:** `skills/ultrathink.md`

| Senaryo | Örnek |
|---------|-------|
| **Mimari kararlar** | "Monolith'i mikroservislere bölelim mi?" |
| **Performans optimizasyonu** | "Bu sorgu neden yavaş?" |
| **Karmaşık bug analizi** | "Race condition nereden kaynaklanıyor?" |
| **Çok adımlı refaktör** | "Bu 10 dosyayı nasıl refactor edelim?" |
| **Sistem tasarımı** | "Ölçeklenebilir bir auth sistemi tasarla" |
| **Trade-off değerlendirmesi** | "SQL vs NoSQL hangisi daha uygun?" |
| **Risk analizi** | "Bu değişikliğin potansiyel etkileri neler?" |

---

### 🏗️ Architecture - Sistem Tasarımı

**Dosya:** `skills/architecture.md`

| Senaryo | Örnek |
|---------|-------|
| **Yeni sistem tasarımı** | "E-ticaret platformu mimarisi oluştur" |
| **Microservices kararı** | "Hangi servislere bölmeliyiz?" |
| **Database seçimi** | "PostgreSQL mı MongoDB mi?" |
| **Scaling stratejisi** | "10x kullanıcıya nasıl ölçekleniriz?" |
| **API gateway tasarımı** | "Gateway pattern nasıl uygulayalım?" |
| **Event-driven architecture** | "Kafka ile async iletişim kur" |

---

### 🎨 Design System - UI/UX Rehberi

**Dosya:** `skills/design-system.md`

| Senaryo | Örnek |
|---------|-------|
| **Component tasarımı** | "Button component oluştur" |
| **Responsive layout** | "Mobile-first grid sistemi kur" |
| **Color system** | "Dark mode desteği ekle" |
| **Typography** | "Font hierarchy belirle" |
| **Spacing system** | "8-point grid uygula" |
| **Animation** | "Micro-interaction ekle" |
| **Accessibility** | "WCAG uyumlu form yap" |

---

### 💻 Backend - Server-Side Geliştirme

**Dosya:** `skills/backend.md`

| Senaryo | Örnek |
|---------|-------|
| **REST API oluşturma** | "User CRUD endpoint'leri yaz" |
| **Authentication** | "JWT tabanlı auth sistemi kur" |
| **Database integration** | "Prisma ile PostgreSQL bağla" |
| **Validation** | "Zod ile input validation yap" |
| **Error handling** | "Global error handler oluştur" |
| **Caching** | "Redis cache stratejisi uygula" |
| **API security** | "Rate limiting ve CORS ayarla" |

---

### 📱 Mobile - Cross-Platform Uygulama

**Dosya:** `skills/mobile.md`

| Senaryo | Örnek |
|---------|-------|
| **React Native app** | "Expo ile yeni proje başlat" |
| **Flutter app** | "Material 3 UI uygula" |
| **State management** | "Zustand/Riverpod kur" |
| **Navigation** | "Stack/Tab navigator ayarla" |
| **Native features** | "Kamera/konum erişimi ekle" |
| **Offline support** | "SQLite ile local storage" |
| **Push notifications** | "Firebase notification entegre et" |

---

### 🧪 Testing - TDD ve Test Stratejileri

**Dosya:** `skills/testing.md`

| Senaryo | Örnek |
|---------|-------|
| **Unit test yazma** | "UserService için testler yaz" |
| **Integration test** | "API endpoint testleri oluştur" |
| **E2E testing** | "Playwright ile login flow test et" |
| **Test coverage** | "Coverage'ı %80'e çıkar" |
| **Mocking** | "External API'yi mock'la" |
| **TDD uygulama** | "Red-Green-Refactor döngüsü" |
| **React testing** | "Component testleri yaz" |

---

### 🔍 Debugging - Hata Ayıklama

**Dosya:** `skills/debugging.md`

| Senaryo | Örnek |
|---------|-------|
| **Runtime error** | "TypeError: Cannot read property" |
| **Intermittent bug** | "Bazen çalışıyor bazen çalışmıyor" |
| **Performance issue** | "Sayfa çok yavaş yükleniyor" |
| **Memory leak** | "Uygulama zamanla yavaşlıyor" |
| **Race condition** | "Veriler bazen yanlış geliyor" |
| **Production bug** | "Sadece production'da oluşan hata" |
| **Regression** | "Eski feature bozuldu" |

---

### ♻️ Refactoring - Kod İyileştirme

**Dosya:** `skills/refactoring.md`

| Senaryo | Örnek |
|---------|-------|
| **Code smell temizleme** | "Bu fonksiyon çok uzun" |
| **DRY uygulama** | "Duplicate kodu birleştir" |
| **Extract function** | "Büyük fonksiyonu parçala" |
| **Rename refactoring** | "Daha anlamlı isimler ver" |
| **Design pattern** | "Strategy pattern uygula" |
| **Legacy code** | "Eski kodu modernize et" |
| **Type safety** | "any'leri kaldır" |

---

### 🚀 Production Deployment - DevOps

**Dosya:** `skills/production-deployment.md`

| Senaryo | Örnek |
|---------|-------|
| **CI/CD pipeline** | "GitHub Actions workflow kur" |
| **Docker deployment** | "Container'ize et ve deploy et" |
| **Environment setup** | "Staging/production ayır" |
| **Blue-green deploy** | "Zero-downtime deployment" |
| **Monitoring setup** | "Prometheus/Grafana kur" |
| **Rollback** | "Önceki versiyona geri dön" |
| **Security scan** | "Pipeline'a Snyk ekle" |

---

### 📁 Multi-File Sync - Çoklu Dosya Değişikliği

**Dosya:** `skills/multi-file-sync.md`

| Senaryo | Örnek |
|---------|-------|
| **Global rename** | "userId'yi customerId yap tüm projede" |
| **API versioning** | "v1'den v2'ye migrate et" |
| **Folder restructure** | "Feature-first yapıya geç" |
| **Import path update** | "Alias değişikliği yap" |
| **Type definition change** | "Interface'i genişlet, tüm kullanımları güncelle" |
| **Config migration** | "ENV variable'ları rename et" |

---

### 📦 Dependency Management - Paket Yönetimi

**Dosya:** `skills/dependency-management.md`

| Senaryo | Örnek |
|---------|-------|
| **Security audit** | "npm audit çalıştır ve fix et" |
| **Major upgrade** | "React 18'den 19'a geç" |
| **Dependency cleanup** | "Kullanılmayan paketleri kaldır" |
| **Version conflict** | "Peer dependency hatası çöz" |
| **Lock file issue** | "package-lock.json sorunu" |
| **Bundle size** | "Bundle'ı küçült" |
| **License check** | "Lisans uyumluluğunu kontrol et" |

---

### 📝 Documentation - Dokümantasyon

**Dosya:** `skills/documentation.md`

| Senaryo | Örnek |
|---------|-------|
| **README yazma** | "Proje README'si oluştur" |
| **API docs** | "OpenAPI/Swagger dokümantasyonu" |
| **Code comments** | "JSDoc ile fonksiyonları belgele" |
| **Architecture docs** | "Sistem diyagramları oluştur" |
| **Changelog** | "CHANGELOG.md güncelle" |
| **ADR yazma** | "Mimari karar belgele" |
| **Onboarding guide** | "Yeni developer rehberi" |

---

## 🔄 Skill Yükleme Protokolü

### Adım 1: Görev Analizi
```
Kullanıcı görevini oku
    │
    ▼
Yukarıdaki tablolardan uygun skill(ler)i belirle
    │
    ▼
Skill dosyasını yükle: skills/<skill-name>.md
```

### Adım 2: Skill Bulunamazsa
```
⚠️ HATA: "[skill-name].md" skill dosyası bulunamadı.

Lütfen aşağıdakilerden birini yapın:
1. Skill dosyasının yolunu gösterin
2. Skill dosyasını oluşturun

Skills olmadan işleme BAŞLANAMAZ.
```

---

## 🔗 Skill Kombinasyonları

Karmaşık görevler birden fazla skill gerektirebilir:

| Senaryo | Skill Kombinasyonu | Yükleme Sırası |
|---------|-------------------|----------------|
| **Karmaşık Backend API** | ultrathink + architecture + backend | 1→2→3 |
| **Yeni UI Component** | design-system + testing | 1→2 |
| **Production Release** | production-deployment + testing | 1→2 |
| **Büyük Refactoring** | ultrathink + refactoring + multi-file-sync + testing | 1→2→3→4 |
| **Mobile App Feature** | mobile + testing | 1→2 |
| **Bug Fix** | debugging + testing | 1→2 |
| **Mimari Karar** | ultrathink + architecture | 1→2 |
| **Paket Upgrade** | dependency-management + testing | 1→2 |

---

## 📂 Skills Dizin Yapısı

```
c:\Users\Mehmet\Desktop\global_workflows\
├── GEMINI.md           ← Global kurallar (C:\Users\Mehmet\.gemini\ içine kopyalanmalı)
├── CORE.md             ← Bu dosya (Merkezi orchestrator)
└── skills/
    ├── ultrathink.md           ✅ Derin düşünme
    ├── architecture.md         ✅ Sistem tasarımı
    ├── design-system.md        ✅ UI/UX rehberi
    ├── backend.md              ✅ Server-side geliştirme
    ├── mobile.md               ✅ Cross-platform mobile
    ├── testing.md              ✅ TDD ve test stratejileri
    ├── debugging.md            ✅ Hata ayıklama
    ├── refactoring.md          ✅ Kod iyileştirme
    ├── production-deployment.md ✅ DevOps/CI-CD
    ├── multi-file-sync.md      ✅ Çoklu dosya değişikliği
    ├── dependency-management.md ✅ Paket yönetimi
    └── documentation.md        ✅ Dokümantasyon
```

---

## ⚠️ Kritik Kurallar

> [!CAUTION]
> **Skill yüklemeden işleme BAŞLAMA!**
> Her görev için uygun skill(ler) MUTLAKA yüklenmelidir.

> [!WARNING]
> **Skill bulunamazsa DURMA!**
> Kullanıcıdan dosya yolunu iste veya skill oluşturulmasını öner.

> [!IMPORTANT]
> **GEMINI.md kuralları her zaman geçerlidir!**
> ESLint kontrolü, 2x code review mutlaka yapılmalıdır.

---

**Son Güncelleme:** Aralık 2025
**Versiyon:** 2.0
