---
description: Central Orchestrator & Skills Registry. Loads automatically to route tasks to the appropriate Skills, Modes, or Guards.
---

# CORE.md - Skills Orchestrator

> Bu dosya tüm görevler için merkezi yönlendirme noktasıdır.
> Görev tipine göre uygun skill(ler) belirlenir ve yüklenir.

---

# 📋 İçindekiler

1. [Skills Referansı - Ne Zaman Hangi Skill?](#1-skills-referansı---ne-zaman-hangi-skill)
    - [1.1 🧠 UltraThink](#11-🧠-ultrathink---derin-düşünme-protokolü)
    - [1.2 🏗️ Architecture](#12-🏗️-architecture---sistem-tasarımı)
    - [1.3 🎨 Design System](#13-🎨-design-system---uiux-rehberi)
    - [1.4 💻 Backend](#14-💻-backend---server-side-geliştirme)
    - [1.5 📱 Mobile](#15-📱-mobile---cross-platform-uygulama)
    - [1.6 🧪 Testing](#16-🧪-testing---tdd-ve-test-stratejileri)
    - [1.7 🔍 Debugging](#17-🔍-debugging---hata-ayıklama)
    - [1.8 ♻️ Refactoring](#18-♻️-refactoring---kod-iyileştirme)
    - [1.9 🚀 Production Deployment](#19-🚀-production-deployment---devops)
    - [1.10 📁 Multi-File Sync](#110-📁-multi-file-sync---çoklu-dosya-değişikliği)
    - [1.11 📦 Dependency Management](#111-📦-dependency-management---paket-yönetimi)
    - [1.12 📝 Documentation](#112-📝-documentation---dokümantasyon)
    - [1.13 ⚡ Optimization](#113-⚡-optimization---sistem--akış-optimizasyonu)
2. [Skill Yükleme Protokolü](#2-skill-yükleme-protokolü)
3. [Skill Kombinasyonları](#3-skill-kombinasyonları)
4. [Skills Dizin Yapısı](#4-skills-dizin-yapısı)
5. [Kritik Kurallar](#5-kritik-kurallar)

---

# 1. Skills Referansı - Ne Zaman Hangi Skill?

> [!NOTE]
> **Dinamik Eşleştirme:** Kullanıcılar aşağıdaki örneklere birebir uymayan şekilde komut verebilir.
> Bu tablolar **referans** niteliğindedir. Agent olarak, kullanıcının talebini analiz et ve
> **semantik olarak en uygun skill(ler)i dinamik şekilde çıkarım yaparak** belirle.
> Örneğin "şu API'de sorun var" → debugging + backend skill'leri gerektirebilir.

---

## 1.1 🧠 UltraThink - Derin Düşünme Protokolü
**Dosya:** [skills/ultrathink.md](skills/ultrathink.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Mimari kararlar** | "Monolith'i mikroservislere bölelim mi?" | [**Bölüm 10:** Sentez ve Karar](skills/ultrathink.md#10-faz-7-sentez-ve-karar) |
| **Performans optimizasyonu** | "Bu sorgu neden yavaş?" | [**Bölüm 4:** Problem Anlama](skills/ultrathink.md#4-faz-1-problem-anlama) / [**Bölüm 5:** Hipotez](skills/ultrathink.md#5-faz-2-hipotez-üretimi) |
| **Karmaşık bug analizi** | "Race condition nereden kaynaklanıyor?" | [**Bölüm 4:** Problem Anlama](skills/ultrathink.md#4-faz-1-problem-anlama) |
| **Çok adımlı refaktör** | "Bu 10 dosyayı nasıl refactor edelim?" | [**Bölüm 3:** Meta-Planlama](skills/ultrathink.md#3-faz-0-meta-planlama) |
| **Sistem tasarımı** | "Ölçeklenebilir bir auth sistemi tasarla" | [**Bölüm 6:** Çözüm Uzayı Keşfi](skills/ultrathink.md#6-faz-3-çözüm-uzayı-keşfi) |
| **Trade-off değerlendirmesi** | "SQL vs NoSQL hangisi daha uygun?" | [**Bölüm 6.2:** Karşılaştırma Matrisi](skills/ultrathink.md#62-karşılaştırma-matrisi) |
| **Risk analizi** | "Bu değişikliğin potansiyel etkileri neler?" | [**Bölüm 7:** Kritik Değerlendirme (Pre-Mortem)](skills/ultrathink.md#7-faz-4-kritik-değerlendirme) |

---

## 1.2 🏗️ Architecture - Sistem Tasarımı
**Dosya:** [skills/architecture.md](skills/architecture.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Yeni sistem tasarımı** | "E-ticaret platformu mimarisi oluştur" | [**Bölüm 1:** Mimari Karar Süreci](skills/architecture.md#1-mimari-karar-süreci) |
| **Microservices kararı** | "Hangi servislere bölmeliyiz?" | [**Bölüm 3.1:** Monolith vs Microservices](skills/architecture.md#31-monolith-vs-microservices) |
| **Database seçimi** | "PostgreSQL mı MongoDB mi?" | [**Bölüm 5:** Database Seçimi](skills/architecture.md#5-database-seçimi) |
| **Scaling stratejisi** | "10x kullanıcıya nasıl ölçekleniriz?" | [**Bölüm 4:** Ölçeklenebilirlik Patternleri](skills/architecture.md#4-ölçeklenebilirlik-patternleri) |
| **API gateway tasarımı** | "Gateway pattern nasıl uygulayalım?" | [**Bölüm 3:** Mimari Patternler](skills/architecture.md#3-mimari-patternler) |
| **Event-driven architecture** | "Kafka ile async iletişim kur" | [**Bölüm 3.3:** Event-Driven Mimarisi](skills/architecture.md#33-event-driven-mimarisi) |

---

## 1.3 🎨 Design System - UI/UX Rehberi
**Dosya:** [skills/design-system.md](skills/design-system.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Component tasarımı** | "Button component oluştur" | [**Bölüm 5:** Component Boyutlandırma](skills/design-system.md#5-component-sizing) |
| **Responsive layout** | "Mobile-first grid sistemi kur" | [**Bölüm 2:** Grid Sistemi](skills/design-system.md#2-layout--grid-system) / [**Bölüm 6:** Breakpoints](skills/design-system.md#6-responsive-breakpoints) |
| **Color system** | "Dark mode desteği ekle" | [**Bölüm 4:** Renk Sistemi](skills/design-system.md#4-color-system) |
| **Typography** | "Font hierarchy belirle" | [**Bölüm 3:** Tipografi Skalası](skills/design-system.md#3-typography-scale-type-scale) |
| **Spacing system** | "8-point grid uygula" | [**Bölüm 1:** Spacing Sistemi](skills/design-system.md#1-spacing-system-8-point-grid) |
| **Animation** | "Micro-interaction ekle" | [**Bölüm 8:** Animasyon & Geçişler](skills/design-system.md#8-animation--transitions) |
| **Accessibility** | "WCAG uyumlu form yap" | [**Bölüm 12:** Erişilebilirlik Standartları](skills/design-system.md#12-accessibility-standards) |

---

## 1.4 💻 Backend - Server-Side Geliştirme
**Dosya:** [skills/backend.md](skills/backend.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **REST API oluşturma** | "User CRUD endpoint'leri yaz" | [**Bölüm 4:** API Tasarım Kuralları](skills/backend.md#4-api-design-rules) |
| **Authentication** | "JWT tabanlı auth sistemi kur" | [**Bölüm 6:** Güvenlik](skills/backend.md#6-security-best-practices) / [**Bölüm 1.1:** Tech Stack](skills/backend.md#11-tech-stack) |
| **Database integration** | "Prisma ile PostgreSQL bağla" | [**Bölüm 7:** Veritabanı Patternleri](skills/backend.md#7-database-patterns) |
| **Validation** | "Zod ile input validation yap" | [**Bölüm 5:** Input Validation (Zod)](skills/backend.md#5-input-validation-zod) |
| **Error handling** | "Global error handler oluştur" | [**Bölüm 9:** Error Handling](skills/backend.md#9-error-handling) |
| **Caching** | "Redis cache stratejisi uygula" | [**Bölüm 8:** Performans Optimizasyonu](skills/backend.md#8-performance-optimization) |
| **API security** | "Rate limiting ve CORS ayarla" | [**Bölüm 6:** Güvenlik Best Practices](skills/backend.md#6-security-best-practices) |

---

## 1.5 📱 Mobile - Cross-Platform Uygulama
**Dosya:** [skills/mobile.md](skills/mobile.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **React Native app** | "Expo ile yeni proje başlat" | [**Bölüm 2:** React Native Best Practices](skills/mobile.md#2-react-native-best-practices) |
| **Flutter app** | "Material 3 UI uygula" | [**Bölüm 3:** Flutter Best Practices](skills/mobile.md#3-flutter-best-practices) |
| **State management** | "Zustand/Riverpod kur" | [**Bölüm 2.4 / 3:** State Management](skills/mobile.md#2-react-native-best-practices) |
| **Navigation** | "Stack/Tab navigator ayarla" | [**Bölüm 2 / 3:** Navigation](skills/mobile.md#2-react-native-best-practices) |
| **Native features** | "Kamera/konum erişimi ekle" | [**Bölüm 5:** Platform-Specific Code](skills/mobile.md#5-platform-specific-code) |
| **Offline support** | "SQLite ile local storage" | [**Bölüm 4.1:** Güvenli Veri Saklama](skills/mobile.md#4-mobile-security) |
| **Push notifications** | "Firebase notification entegre et" | [**Bölüm 8:** Mutlaka Yap Listesi](skills/mobile.md#8-mutlaka-yap-listesi) |

---

## 1.6 🧪 Testing - TDD ve Test Stratejileri
**Dosya:** [skills/testing.md](skills/testing.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Unit test yazma** | "UserService için testler yaz" | [**Bölüm 2:** Unit Testing (Jest)](skills/testing.md#2-unit-testing-jest) |
| **Integration test** | "API endpoint testleri oluştur" | [**Bölüm 3:** Integration Testing](skills/testing.md#3-integration-testing) |
| **E2E testing** | "Playwright testleri yaz" | [**Bölüm 4:** E2E Testing](skills/testing.md#4-e2e-testing-playwright) |
| **Coverage** | "Test coverage raporu al" | [**Bölüm 1:** Test Piramidi (Strateji)](skills/testing.md#1-test-piramidi) |

---

## 1.7 🔍 Debugging - Hata Ayıklama
**Dosya:** [skills/debugging.md](skills/debugging.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Runtime error** | "TypeError: Cannot read property" | [**Bölüm 2:** REPRODUCE (Tekrarlama)](skills/debugging.md#2-phase-1-reproduce) |
| **Intermittent bug** | "Bazen çalışıyor bazen çalışmıyor" | [**Bölüm 4:** ISOLATE (İzole Etme)](skills/debugging.md#4-phase-3-isolate) |
| **Performance issue** | "Sayfa çok yavaş yükleniyor" | [**Bölüm 2:** REPRODUCE (Gözlemleme)](skills/debugging.md#2-phase-1-reproduce) |
| **Memory leak** | "Uygulama zamanla yavaşlıyor" | [**Bölüm 5:** HİPOTEZ Üretimi](skills/debugging.md#5-phase-4-hypothesize) |
| **Race condition** | "Veriler bazen yanlış geliyor" | [**Bölüm 5:** Common Bug Patterns](skills/debugging.md#5-phase-4-hypothesize) |
| **Production bug** | "Sadece production'da oluşan hata" | [**Bölüm 8:** REFLECT (Post-Mortem)](skills/debugging.md#8-phase-7-reflect) |
| **Regression** | "Eski feature bozuldu" | [**Bölüm 4.1:** Binary Search](skills/debugging.md#4-phase-3-isolate) |

---

## 1.8 ♻️ Refactoring - Kod İyileştirme
**Dosya:** [skills/refactoring.md](skills/refactoring.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Code smell temizleme** | "Bu fonksiyon çok uzun" | [**Bölüm 5:** Code Smells](skills/refactoring.md#5-code-smells) |
| **DRY uygulama** | "Duplicate kodu birleştir" | [**Bölüm 4:** Refactoring Patternleri](skills/refactoring.md#4-common-refactoring-patterns) |
| **Extract function** | "Büyük fonksiyonu parçala" | [**Bölüm 4.1:** Extract Function](skills/refactoring.md#41-extract-function) |
| **Rename refactoring** | "Daha anlamlı isimler ver" | [**Bölüm 3:** Refactoring Süreci (Küçük Adımlar)](skills/refactoring.md#3-refactoring-süreci) |
| **Design pattern** | "Strategy pattern uygula" | [**Bölüm 4:** Patternler](skills/refactoring.md#4-common-refactoring-patterns) |
| **Legacy code** | "Eski kodu modernize et" | [**Bölüm 7:** Incremental Refactoring](skills/refactoring.md#7-incremental-refactoring-strategy) |
| **Type safety** | "any'leri kaldır" | [**Bölüm 6:** Safe Checklist](skills/refactoring.md#6-safe-refactoring-checklist) |

---

## 1.9 🚀 Production Deployment - DevOps
**Dosya:** [skills/production-deployment.md](skills/production-deployment.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **CI/CD pipeline** | "GitHub Actions workflow kur" | [**Bölüm 3:** CI/CD Pipeline](skills/production-deployment.md#3-cicd-pipeline) |
| **Docker deployment** | "Container'ize et ve deploy et" | [**Bölüm 4.3:** Deployment Stratejileri](skills/production-deployment.md#4-deployment-strategies) |
| **Environment setup** | "Staging/production ayır" | [**Bölüm 3:** Pipeline (Environment)](skills/production-deployment.md#3-cicd-pipeline) |
| **Blue-green deploy** | "Zero-downtime deployment" | [**Bölüm 4:** Deployment Stratejileri](skills/production-deployment.md#4-deployment-strategies) |
| **Monitoring setup** | "Prometheus/Grafana kur" | [**Bölüm 5:** Monitoring & Observability](skills/production-deployment.md#5-monitoring--observability) |
| **Rollback** | "Önceki versiyona geri dön" | [**Bölüm 6:** Rollback Stratejisi](skills/production-deployment.md#6-rollback-strategy) |
| **Security scan** | "Pipeline'a Snyk ekle" | [**Bölüm 2:** Pre-Deployment](skills/production-deployment.md#2-pre-deployment-checklist) / [**Bölüm 3:** Security](skills/production-deployment.md#3-cicd-pipeline) |

---

## 1.10 📁 Multi-File Sync - Çoklu Dosya Değişikliği
**Dosya:** [skills/multi-file-sync.md](skills/multi-file-sync.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Global rename** | "userId'yi customerId yap tüm projede" | [**Bölüm 2:** Değişiklik Süreci (Planlama)](skills/multi-file-sync.md#2-multi-file-değişiklik-süreci) |
| **API versioning** | "v1'den v2'ye migrate et" | [**Bölüm 7:** Kontrol Listesi](skills/multi-file-sync.md#7-kontrol-listesi) |
| **Folder restructure** | "Feature-first yapıya geç" | [**Bölüm 4:** Context Preservation](skills/multi-file-sync.md#4-context-preservation) |
| **Import path update** | "Alias değişikliği yap" | [**Bölüm 3:** Araçlar ve Teknikler](skills/multi-file-sync.md#3-araçlar-ve-teknikler) |
| **Type definition change** | "Interface'i genişlet, tüm kullanımları güncelle" | [**Bölüm 5:** Tehlikeli Durumlar](skills/multi-file-sync.md#5-tehlikeli-durumlar) |
| **Config migration** | "ENV variable'ları rename et" | [**Bölüm 6:** Rollback Stratejileri](skills/multi-file-sync.md#6-rollback-stratejileri) |

---

## 1.11 📦 Dependency Management - Paket Yönetimi
**Dosya:** [skills/dependency-management.md](skills/dependency-management.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Security audit** | "npm audit çalıştır ve fix et" | [**Bölüm 3:** Security Auditing](skills/dependency-management.md#3-security-auditing) |
| **Major upgrade** | "React 18'den 19'a geç" | [**Bölüm 5:** Upgrade Stratejisi](skills/dependency-management.md#5-upgrade-stratejisi) |
| **Dependency cleanup** | "Kullanılmayan paketleri kaldır" | [**Bölüm 7:** Dependency Cleanup](skills/dependency-management.md#7-dependency-cleanup) |
| **Version conflict** | "Peer dependency hatası çöz" | [**Bölüm 4:** Version Management](skills/dependency-management.md#4-version-management) |
| **Lock file issue** | "package-lock.json sorunu" | [**Bölüm 6:** Lock File Yönetimi](skills/dependency-management.md#6-lock-file-yönetimi) |
| **Bundle size** | "Bundle'ı küçült" | [**Bölüm 8:** Dependency Monitoring](skills/dependency-management.md#8-dependency-monitoring) |
| **License check** | "Lisans uyumluluğunu kontrol et" | [**Bölüm 2:** Paket Ekleme Kararı](skills/dependency-management.md#2-paket-ekleme-kararı) |

---

## 1.12 📝 Documentation - Dokümantasyon
**Dosya:** [skills/documentation.md](skills/documentation.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **README yazma** | "Proje README'si oluştur" | [**Bölüm 2:** README Best Practices](skills/documentation.md#2-readme-best-practices) |
| **API docs** | "OpenAPI/Swagger dokümantasyonu" | [**Bölüm 4:** API Documentation](skills/documentation.md#4-api-documentation) |
| **Code comments** | "JSDoc ile fonksiyonları belgele" | [**Bölüm 3:** Code Documentation](skills/documentation.md#3-code-documentation) |
| **Architecture docs** | "Sistem diyagramları oluştur" | [**Bölüm 6:** Architecture Documentation](skills/documentation.md#6-architecture-documentation) |
| **Changelog** | "CHANGELOG.md güncelle" | [**Bölüm 5:** Changelog](skills/documentation.md#5-changelog) |
| **ADR yazma** | "Mimari karar belgele" | [**Bölüm 6.1:** ADR](skills/documentation.md#61-architecture-decision-records-adr) |
| **Onboarding guide** | "Yeni developer rehberi" | [**Bölüm 2:** README](skills/documentation.md#2-readme-best-practices) |

---

## 1.13 ⚡ Optimization - Sistem & Akış Optimizasyonu
**Dosya:** [skills/optimization.md](skills/optimization.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Bottleneck tespiti** | "Kullanıcı akışındaki yavaş adımları bul" | [**Bölüm 2:** Darboğaz Tespiti](skills/optimization.md#2-darboğaz-tespiti-bottleneck-identification) |
| **User flow analizi** | "Friction point'leri tespit et" | [**Bölüm 5:** Frontend & UX Optimizasyonu](skills/optimization.md#5-frontend--kullanıcı-deneyimi-optimizasyonu) |
| **Performans tuning** | "AI destekli sistem optimizasyonu" | [**Bölüm 3:** AI-Driven Optimizasyon](skills/optimization.md#3-ai-driven-optimizasyon) |
| **Observability** | "OpenTelemetry ile izlenebilirlik kur" | [**Bölüm 4:** Modern Gözlemlenebilirlik](skills/optimization.md#4-modern-gözlemlenebilirlik-observability) |
| **RUM & Metrics** | "Real User Monitoring entegre et" | [**Bölüm 5:** RUM & Metrics](skills/optimization.md#5-frontend--kullanıcı-deneyimi-optimizasyonu) |
| **Value Stream** | "Süreçlerdeki gereksiz adımları ayıkla" | [**Bölüm 7:** Sistematik İyileştirme Döngüsü](skills/optimization.md#7-sistematik-iyileştirme-döngüsü) |

---

# 2. Skill Yükleme Protokolü

## 2.1 Adım 1: Görev Analizi
```
Kullanıcı görevini oku
    │
    ▼
Yukarıdaki tablolardan uygun skill(ler)i belirle
    │
    ▼
Skill dosyasını yükle: skills/<skill-name>.md
```

## 2.2 Adım 2: Skill Bulunamazsa
```
⚠️ HATA: "[skill-name].md" skill dosyası bulunamadı.

Lütfen aşağıdakilerden birini yapın:
1. Skill dosyasının yolunu gösterin
2. Skill dosyasını oluşturun

Skills olmadan işleme BAŞLANAMAZ.
```

---

# 3. Skill Kombinasyonları

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
| **Performans İyileştirme** | optimization + ultrathink + debugging | 1→2→3 |

---

# 4. Skills Dizin Yapısı

```
c:\Users\Mehmet\Desktop\global_workflows\
├── GEMINI.md           ← Global kurallar
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
    ├── documentation.md        ✅ Dokümantasyon
    └── optimization.md         ✅ Sistem & Akış Optimizasyonu [NEW]
```

---

# 5. Kritik Kurallar

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
**Versiyon:** 3.1
