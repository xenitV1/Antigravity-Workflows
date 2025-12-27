---
description: Central Orchestrator & Skills Registry. Loads automatically to route tasks to the appropriate Skills, Modes, or Guards.
---

# CORE.md - Skills Orchestrator

> Bu dosya tüm görevler için merkezi yönlendirme noktasıdır.
> Görev tipine göre uygun skill(ler) belirlenir ve yüklenir.

---

## 🔧 DİNAMİK PATH ALGILAMA (Otomatik)

> [!NOTE]
> **AI Agent için:** Bu dosyayı okuduğunda, path'leri **otomatik olarak algıla**.
> Dizin yapısını kullanıcının home dizinine göre belirle.

### Kurulum Yapısı

```
~/.gemini/
├── GEMINI.md                    # Global kurallar
└── antigravity/
    ├── CORE.md                  # Bu dosya (Merkezi orkestratör)
    └── global_workflows/
        └── skills/              # Skill dosyaları

~/.agent/                        # Antigravity IDE Rules & Workflows
├── rules/                       # 15 workspace rule (Model Decision/Glob/Always On)
└── workflows/                   # 8 slash command (/ultrathink, /plan, etc.)
```

**Placeholder Tanımları:**
| Placeholder | Anlamı |
|-------------|--------|
| `{ANTIGRAVITY_DIR}` | `~/.gemini/antigravity/` dizini |
| `{SKILLS_DIR}` | `~/.gemini/antigravity/global_workflows/skills/` dizini |
| `{AGENT_DIR}` | `~/.agent/` dizini |
| `{RULES_DIR}` | `~/.agent/rules/` dizini |
| `{WORKFLOWS_DIR}` | `~/.agent/workflows/` dizini |

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
| **Sokratik Gerçeklik Kontrolü** | "Kullanıcı ne istiyor? Ben ne yapıyorum?" | [**Bölüm 3:** Sokratik Reality Check](skills/ultrathink.md#sokratik-gerçeklik-kontrolü-5-step-reality-check) |
| **Meta-Planlama** | "Karmaşık görevi nasıl adımlara bölelim?" | [**Bölüm 3:** Faz 0 - Meta-Planlama](skills/ultrathink.md#3-faz-0-meta-planlama) |
| **Problem Analizi** | "Sorunun kök nedeni ne?" | [**Bölüm 4:** Faz 1 - Problem Anlama](skills/ultrathink.md#4-faz-1-problem-anlama) |
| **Hipotez Kalibrasyonu** | "Çözümden ne kadar eminiz? (Güven %)" | [**Bölüm 5.2:** Güven Kalibrasyonu](skills/ultrathink.md#52-hipotez-güven-kalibrasyonu) |
| **Çözüm Üretimi** | "Alternatif çözümler neler?" | [**Bölüm 6:** Faz 3 - Çözüm Uzayı](skills/ultrathink.md#6-faz-3-çözüm-uzayı-keşfi) |
| **Trade-off Analizi** | "Karşılaştırma matrisi hazırla" | [**Bölüm 6.2:** Karşılaştırma Matrisi](skills/ultrathink.md#62-karşılaştırma-matrisi) |
| **Kritik Değerlendirme** | "Pre-mortem yapalım (Risk analizi)" | [**Bölüm 7:** Faz 4 - Kritik Değerlendirme](skills/ultrathink.md#7-faz-4-kritik-değerlendirme) |
| **Devil's Advocate** | "Çözümü çürütmeye çalış" | [**Bölüm 7.1:** Şeytanın Avukatı](skills/ultrathink.md#71-devils-advocate-şeytanın-avukatı) |
| **Edge Case Analizi** | "Sınır durumlar neler? (Input/State)" | [**Bölüm 8:** Edge Case Analizi](skills/ultrathink.md#8-faz-5-edge-case-analizi) |
| **Bias Kontrolü** | "Önyargılı mı düşünüyoruz?" | [**Bölüm 9.2:** Bias Tespiti](skills/ultrathink.md#92-bias-tespiti-ve-düzeltme) |
| **Sentez ve Karar** | "Nihai kararı ver ve belgele" | [**Bölüm 10:** Faz 7 - Sentez ve Karar](skills/ultrathink.md#10-faz-7-sentez-ve-karar) |

---

## 1.2 🏗️ Architecture - Sistem Tasarımı
**Dosya:** [skills/architecture.md](skills/architecture.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Süreç Yönetimi** | "Mimari karar süreci nasıl işler?" | [**Bölüm 1:** Mimari Karar Süreci](skills/architecture.md#1-mimari-karar-süreci) |
| **Gereksinim Analizi** | "Non-functional gereksinimler neler?" | [**Bölüm 2:** Requirements (Func vs Non-Func)](skills/architecture.md#2-functional-vs-non-functional-requirements) |
| **Mimari Seçimi** | "Monolith mi Microservices mi?" | [**Bölüm 3.1:** Monolith vs Microservices](skills/architecture.md#31-monolith-vs-microservices) |
| **Katmanlı Mimari** | "Layered architecture uygula" | [**Bölüm 3.2:** Layered Architecture](skills/architecture.md#32-layered-architecture) |
| **Event-Driven** | "Async/Event-driven yapı kur" | [**Bölüm 3.3:** Event-Driven Mimarisi](skills/architecture.md#33-event-driven-mimarisi) |
| **CQRS** | "Command ve Query'yi ayır" | [**Bölüm 3.4:** CQRS](skills/architecture.md#34-cqrs-command-query-responsibility-segregation) |
| **Ölçeklendirme** | "Sistemi scale et (Yatay/Dikey)" | [**Bölüm 4.1:** Horizontal vs Vertical Scaling](skills/architecture.md#41-horizontal-vs-vertical-scaling) |
| **Yük Dengeleme** | "Load balancer stratejisi" | [**Bölüm 4.2:** Load Balancing](skills/architecture.md#42-load-balancing) |
| **Caching** | "Cache mekanizması kuralım" | [**Bölüm 4.3:** Caching Strategy](skills/architecture.md#43-caching-strategy) |
| **Veritabanı Seçimi** | "SQL vs NoSQL kararı ver" | [**Bölüm 5:** Database Selection](skills/architecture.md#5-database-selection) |
| **Validation** | "POC ile doğrula" | [**Bölüm 1 (Adım 6):** Validate](skills/architecture.md#1-mimari-karar-süreci) |

---

## 1.3 🎨 Design System - UI/UX Rehberi
**Dosya:** [skills/design-system.md](skills/design-system.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Tasarım Süreci** | "Adım adım tasarım yap (CoT)" | [**Bölüm 15:** Chain-of-Thought Prompt](skills/design-system.md#15-chain-of-thought-prompt-adım-adım-düşünme) |
| **Dinamik Karar** | "Proje tipine göre (E-ticaret/SaaS) esne" | [**Bölüm 16:** Bağlamsal Esneklik](skills/design-system.md#16-dinamik-karar-alma---bağlamsal-esneklik) |
| **Component Tasarımı** | "Button/Card oluştur" | [**Bölüm 5:** Component Sizing](skills/design-system.md#5-component-sizing) |
| **Spacing & Layout** | "8-point grid ve container yapısı" | [**Bölüm 1:** Spacing](skills/design-system.md#1-spacing-system-8-point-grid) / [**Bölüm 2:** Layout](skills/design-system.md#2-layout--grid-system) |
| **Visual Hierarchy** | "Shadow ve Z-index ayarla" | [**Bölüm 7:** Visual Hierarchy](skills/design-system.md#7-visual-hierarchy) |
| **Micro-interactions** | "Hover ve Loading durumları" | [**Bölüm 10:** Micro-interactions](skills/design-system.md#10-micro-interactions) |
| **Modern CSS** | "Container Query kullan" | [**Bölüm 11:** Modern CSS (2025)](skills/design-system.md#11-modern-css-features-2025) |
| **Typography** | "Fluid typography uygula" | [**Bölüm 3:** Tipografi / Fluid Scale](skills/design-system.md#3-typography-scale-type-scale) |
| **Color & Theme** | "Dark mode ve kontrast" | [**Bölüm 4:** Color System](skills/design-system.md#4-color-system) |
| **Responsive** | "Mobil uyumlu yap" | [**Bölüm 6:** Breakpoints](skills/design-system.md#6-responsive-breakpoints) |
| **Animation** | "Geçiş efektleri ekle" | [**Bölüm 8:** Animasyon](skills/design-system.md#8-animation--transitions) |
| **Accessibility** | "Erişilebilir (a11y) yap" | [**Bölüm 12:** Erişilebilirlik](skills/design-system.md#12-accessibility-standards) |

---

## 1.4 💻 Backend - Server-Side Geliştirme
**Dosya:** [skills/backend.md](skills/backend.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **API Tasarımı** | "REST standartlarına uygun route yap" | [**Bölüm 4:** API Design Best Practices](skills/backend.md#4-api-design-best-practices) |
| **Response Formatı** | "Standart API response dön" | [**Bölüm 4.2:** Response Format Standardı](skills/backend.md#42-response-format-standardı) |
| **Validation** | "Zod ile input doğrulama" | [**Bölüm 5:** Input Validation (Zod)](skills/backend.md#5-input-validation-zod) |
| **Security** | "Rate limit ve Helmet ekle" | [**Bölüm 6:** Security Best Practices](skills/backend.md#6-security-best-practices) |
| **Authentication** | "JWT ve Role-based auth" | [**Bölüm 6:** Auth Middleware](skills/backend.md#6-security-best-practices) |
| **Database Patterns** | "Repository pattern uygula" | [**Bölüm 7.1:** Repository Pattern](skills/backend.md#71-repository-pattern) |
| **Transactions** | "Atomic transaction yönetimi" | [**Bölüm 7.2:** Transaction Handling](skills/backend.md#72-transaction-handling) |
| **Performance** | "Redis caching entegrasyonu" | [**Bölüm 8.2:** Caching (Redis)](skills/backend.md#82-caching-redis) |
| **Error Handling** | "Global error handler ve AppError" | [**Bölüm 9:** Error Handling](skills/backend.md#9-error-handling) |
| **Folder Structure** | "Domain-driven dosya yapısı" | [**Bölüm 3:** Project Structure](skills/backend.md#3-project-structure) |
| **Tech Stack** | "Hono.js / Modern Stack" | [**Bölüm 1:** Tech Stack & Tools](skills/backend.md#1-tech-stack--tools) |

---

## 1.5 📱 Mobile - Cross-Platform Uygulama
**Dosya:** [skills/mobile.md](skills/mobile.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Setup & Proje** | "React Native veya Flutter projesi kur" | [**Bölüm 2.1 / 3.1:** Proje Yapısı](skills/mobile.md#2-react-native-best-practices) |
| **Component Standardı** | "Modern ve performanslı component yaz" | [**Bölüm 2.2 / 3.2:** Best Practices](skills/mobile.md#22-functional-components--hooks) |
| **Performans** | "FlashList veya RepaintBoundary kullan" | [**Bölüm 2.3 / 3.3:** Performance Optimization](skills/mobile.md#23-performance-optimization) |
| **State Management** | "Zustand veya Riverpod entegrasyonu" | [**Bölüm 2.4 / 3.4:** State Management](skills/mobile.md#24-state-management-zustand) |
| **Navigation** | "Stack/Tab navigation kurgula" | [**Bölüm 2.6 / 3.5:** Navigation](skills/mobile.md#26-navigation-react-navigation) |
| **Security** | "Token'ları Secure Store'da sakla" | [**Bölüm 4.1:** Secure Storage](skills/mobile.md#41-secure-storage) |
| **API Güvenliği** | "Certificate pinning uygula" | [**Bölüm 4.2:** API Security](skills/mobile.md#42-api-security) |
| **Platform Özellikleri** | "Kamera/Konum izni ve logic" | [**Bölüm 5:** Platform-Specific Code](skills/mobile.md#5-platform-specific-code) |
| **Offline First** | "İnternet yokken çalışma stratejisi" | [**Bölüm 4:** Mobile Security & Storage](skills/mobile.md#4-mobile-security) |

---

## 1.6 🧪 Testing - TDD ve Test Stratejileri
**Dosya:** [skills/testing.md](skills/testing.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Strateji Kurulumu** | "Test piramidi nasıl olmalı?" | [**Bölüm 1:** Test Piramidi](skills/testing.md#1-test-piramidi) |
| **Unit Test** | "Jest ile fonksiyon/component test et" | [**Bölüm 2:** Unit Testing (Jest)](skills/testing.md#2-unit-testing-jest) |
| **Mocking** | "API call'u mock'la" | [**Bölüm 2.2:** Mocking](skills/testing.md#22-mocking) |
| **Integration Test** | "API endpoint testi yaz (Supertest)" | [**Bölüm 3:** Integration Testing](skills/testing.md#3-integration-testing) |
| **E2E Test** | "Playwright ile login akışını test et" | [**Bölüm 4:** E2E Testing (Playwright)](skills/testing.md#4-e2e-testing-playwright) |
| **Visual Test** | "Arayüz kaymalarını yakala" | [**Bölüm 5:** Visual Regression Testing](skills/testing.md#5-visual-regression-testing) |
| **TDD Workflow** | "Red-Green-Refactor uygula" | [**Bölüm 6:** TDD (Test Driven Development)](skills/testing.md#6-tdd-test-driven-development) |
| **Best Practices** | "AAA pattern ve izolasyon kuralları" | [**Bölüm 7:** Test Yazım Kuralları](skills/testing.md#7-test-yazım-kuralları) |
| **Kalite Kontrolü** | "Coverage analizi yap" | [**Bölüm 8:** Kontrol Listesi](skills/testing.md#8-kontrol-listesi) |

---

## 1.7 � Debugging - Hata Ayıklama Protokolü
**Dosya:** [skills/debugging.md](skills/debugging.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Tekrarlama (Reproduce)** | "Hatayı adım adım tekrarla" | [**Bölüm 2:** Phase 1 - Reproduce](skills/debugging.md#2-faz-1-reproduce-tekrarla) |
| **Kök Neden (RCA)** | "Problem neden oluştu?" | [**Bölüm 3/5:** Root Cause Analysis](skills/debugging.md#3-faz-2-understand-anla) |
| **İzolasyon** | "Binary search ile alanı daralt" | [**Bölüm 4:** Phase 3 - Isolate](skills/debugging.md#4-faz-3-isolate-izolasyon) |
| **Hipotez Testi** | "En olası nedeni test et" | [**Bölüm 5:** Phase 4 - Hypothesize](skills/debugging.md#5-faz-4-hypothesize-hipotez) |
| **Network Debugging** | "API isteklerini incele" | [**Bölüm 6.3:** Network Debugging](skills/debugging.md#63-network-debugging) |
| **Logging** | "Yapılandırılmış log ekle" | [**Bölüm 9.2:** Structured Logging](skills/debugging.md#92-structured-logging) |
| **Common Patterns** | "Null reference veya Race condition" | [**Bölüm 5.2:** Common Bug Patterns](skills/debugging.md#52-common-bug-patterns) |
| **Post-Mortem** | "Olay sonrası rapor yaz" | [**Bölüm 8:** Phase 7 - Reflect](skills/debugging.md#8-faz-7-reflect-yansıtma) |
| **Tools** | "VS Code debugger kullan" | [**Bölüm 6:** Phase 5 - Fix & Tools](skills/debugging.md#6-faz-5-fix--tools) |
| **Race condition** | "Veriler bazen yanlış geliyor" | [**Bölüm 5:** Common Bug Patterns](skills/debugging.md#5-phase-4-hypothesize) |
| **Production bug** | "Sadece production'da oluşan hata" | [**Bölüm 8:** REFLECT (Post-Mortem)](skills/debugging.md#8-phase-7-reflect) |
| **Regression** | "Eski feature bozuldu" | [**Bölüm 4.1:** Binary Search](skills/debugging.md#4-phase-3-isolate) |

---

## 1.8 ♻️ Refactoring - Kod İyileştirme
**Dosya:** [skills/refactoring.md](skills/refactoring.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Zamanlama** | "Şu an refactor yapmalı mıyım?" | [**Bölüm 2:** Ne Zaman Refactor?](skills/refactoring.md#2-ne-zaman-refactor) |
| **Code Smells** | "Long method veya duplication var" | [**Bölüm 5:** Code Smells](skills/refactoring.md#5-code-smells) |
| **Süreç** | "Küçük adımlarla ilerle" | [**Bölüm 3:** Refactoring Süreci](skills/refactoring.md#3-refactoring-süreci-küçük-adımlar) |
| **Extract Patterns** | "Fonksiyonu parçala (Extract Method)" | [**Bölüm 4.1:** Extract Function](skills/refactoring.md#41-extract-function) |
| **Rename & Simplify** | "Değişken ismini düzelt" | [**Bölüm 4.2:** Rename Variable](skills/refactoring.md#4-common-refactoring-patterns) |
| **DRY** | "Tekrar eden kodu temizle" | [**Bölüm 4.5:** Remove Duplication](skills/refactoring.md#45-remove-duplication-dry) |
| **Magic Numbers** | "Sabitleri constant yap" | [**Bölüm 4.3:** Replace Magic Numbers](skills/refactoring.md#43-replace-magic-numbers-with-constants) |
| **Legacy Code** | "Eski kodu güvenle değiştir (Sprout)" | [**Bölüm 7:** Incremental Refactoring](skills/refactoring.md#7-incremental-refactoring-strategy) |
| **Safe Checklist** | "Type safety ve test kontrolü" | [**Bölüm 6 / 8:** Kontrol Listesi](skills/refactoring.md#8-kontrol-listesi) |

---

## 1.9 🚀 Production Deployment - DevOps
**Dosya:** [skills/production-deployment.md](skills/production-deployment.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Hazırlık** | "Deploy öncesi checklist kontrolü" | [**Bölüm 2:** Pre-Deployment Checklist](skills/production-deployment.md#2-pre-deployment-checklist) |
| **Pipeline Kurulumu** | "GitHub Actions ile CI/CD kur" | [**Bölüm 3:** CI/CD Pipeline](skills/production-deployment.md#3-cicd-pipeline) |
| **Secrets** | "API key ve env variable yönetimi" | [**Bölüm 3.2:** Pipeline Security](skills/production-deployment.md#32-pipeline-security) |
| **Strateji Seçimi** | "Blue-Green veya Canary uygula" | [**Bölüm 4:** Deployment Strategies](skills/production-deployment.md#4-deployment-stratejileri-deployment-strategies) |
| **Feature Flags** | "A/B testi veya kademeli açılış" | [**Bölüm 4.3:** Feature Flags](skills/production-deployment.md#43-feature-flags) |
| **Monitoring** | "Prometheus/Grafana metrikleri" | [**Bölüm 5:** Monitoring & Observability](skills/production-deployment.md#5-monitoring--observability) |
| **Alerting** | "Hata oranı artınca uyarı gönder" | [**Bölüm 5.3:** Alert Rules](skills/production-deployment.md#53-alert-rules) |
| **Rollback** | "Acil durumda eski sürüme dön" | [**Bölüm 6:** Rollback Strategy](skills/production-deployment.md#6-rollback-strategy) |
| **Güvenlik** | "Security scan ve incident response" | [**Bölüm 7:** Security & Compliance](skills/production-deployment.md#7-security--compliance) |

---

## 1.10 📁 Multi-File Sync - Çoklu Dosya Değişikliği
**Dosya:** [skills/multi-file-sync.md](skills/multi-file-sync.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Planlama** | "Bu değişiklik 20 dosyayı etkileyecek" | [**Bölüm 2:** Değişiklik Süreci (Planlama)](skills/multi-file-sync.md#2-multi-file-değişiklik-süreci) |
| **Global Rename** | "userId'yi customerId yap" | [**Bölüm 3.1:** IDE Refactoring](skills/multi-file-sync.md#31-ide-refactoring-rename-symbol) |
| **Grep Kontrolü** | "Text içinde kalan referansları bul" | [**Bölüm 3.2:** Grep ile Kontrol](skills/multi-file-sync.md#32-grep-ile-kontrol) |
| **Context** | "Refactor sırasında bağlamı kaybetme" | [**Bölüm 4:** Bağlam Koruma (Stash)](skills/multi-file-sync.md#42-git-stash-kullanımı) |
| **Tehlikeli Durumlar** | "Interface değişti, her yeri güncelle" | [**Bölüm 5:** Tehlikeli Durumlar](skills/multi-file-sync.md#5-tehlikeli-durumlar) |
| **Rollback** | "İşler karıştı, geri al" | [**Bölüm 6:** Rollback Stratejileri](skills/multi-file-sync.md#6-rollback-stratejileri) |
| **Kontrol Listesi** | "Her şeyi düzgün yaptım mı?" | [**Bölüm 7:** Kontrol Listesi](skills/multi-file-sync.md#7-kontrol-listesi) |

---

## 1.11 📦 Dependency Management - Paket Yönetimi
**Dosya:** [skills/dependency-management.md](skills/dependency-management.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Paket Seçimi** | "Bu kütüphaneyi kullanmalı mıyım?" | [**Bölüm 2:** Paket Ekleme Kararı](skills/dependency-management.md#2-paket-ekleme-kararı) |
| **Audit** | "Güvenlik açıklarını tarat" | [**Bölüm 3:** Security Auditing](skills/dependency-management.md#3-security-auditing) |
| **Versiyonlama** | "Tilde (~) mi Caret (^) mi?" | [**Bölüm 4:** Version Management](skills/dependency-management.md#4-version-management) |
| **Upgrade** | "Paketleri güvenle güncelle" | [**Bölüm 5:** Upgrade Stratejisi](skills/dependency-management.md#5-upgrade-stratejisi) |
| **Lock File** | "package-lock.json conflict var" | [**Bölüm 6:** Lock File Yönetimi](skills/dependency-management.md#6-lock-file-yönetimi) |
| **Temizlik** | "Kullanılmayan paketleri sil" | [**Bölüm 7:** Dependency Cleanup](skills/dependency-management.md#7-dependency-cleanup) |
| **Monitoring** | "Dependabot ayarla" | [**Bölüm 8:** Dependency Monitoring](skills/dependency-management.md#8-dependency-monitoring) |

---

## 1.12 📝 Documentation - Dokümantasyon
**Dosya:** [skills/documentation.md](skills/documentation.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **README** | "Proje giriş dokümanı hazırla" | [**Bölüm 2:** README Best Practices](skills/documentation.md#2-readme-best-practices) |
| **Code Comments** | "JSDoc/TSDoc formatında yorum yaz" | [**Bölüm 3:** Code Documentation](skills/documentation.md#3-code-documentation) |
| **API Docs** | "Swagger/OpenAPI speği oluştur" | [**Bölüm 4:** API Documentation](skills/documentation.md#4-api-documentation) |
| **Changelog** | "Versiyon geçmişini tut" | [**Bölüm 5:** Changelog & Versioning](skills/documentation.md#5-changelog--versioning) |
| **ADR** | "Mimari kararı kaydet" | [**Bölüm 6.1:** Architecture Decision Records](skills/documentation.md#61-architecture-decision-records-adr) |
| **Diagrams** | "Sistem diyagramı çiz (Mermaid)" | [**Bölüm 6.2:** Architecture Diagrams](skills/documentation.md#62-architecture-diagrams-c4-model) |
| **Technical Writing** | "Nasıl daha net yazarım?" | [**Bölüm 7:** Technical Writing Style](skills/documentation.md#7-technical-writing-best-practices) |

---

## 1.13 ⚡ Optimization - Sistem & Akış Optimizasyonu
**Dosya:** [skills/optimization.md](skills/optimization.md)

| Senaryo | Örnek | İlgili Bölüm |
|---------|-------|--------------|
| **Darboğaz Tespiti** | "Sistem neden yavaş?" | [**Bölüm 2:** Bottleneck Identification](skills/optimization.md#2-darboğaz-tespiti-bottleneck-identification) |
| **AI Analizi** | "Yapay zeka ile kod analizi yap" | [**Bölüm 3:** AI-Driven Optimizasyon](skills/optimization.md#3-ai-driven-optimizasyon) |
| **Observability** | "LCP/INP skorlarını ölç" | [**Bölüm 5:** Frontend & UX Optimizasyonu](skills/optimization.md#5-frontend--kullanıcı-deneyimi-optimizasyonu) |
| **Backend Tuning** | "N+1 query sorununu çöz" | [**Bölüm 6:** Backend & Database Tuning](skills/optimization.md#6-backend--veritabanı-optimizasyonu) |
| **İyileştirme Döngüsü** | "Ölç -> Analiz Et -> İyileştir" | [**Bölüm 7:** Sistematik İyileştirme Döngüsü](skills/optimization.md#7-sistematik-iyileştirme-döngüsü) |
| **Prensipler** | "Premature optimization'dan kaçın" | [**Bölüm 1:** Optimizasyon Prensipleri](skills/optimization.md#1-optimizasyon-prensipleri-2025) |
| **Observability Tools** | "OpenTelemetry kurulumu" | [**Bölüm 4:** Modern Gözlemlenebilirlik](skills/optimization.md#4-modern-gözlemlenebilirlik-observability) |

---

# 2. Skill Yükleme Protokolü

## 2.1 Adım 1: Hassas Görev Analizi
```
Kullanıcı görevini analiz et (Örn: "Button component tasarla")
    │
    ▼
CORE.md tablolarından SKILL ve İLGİLİ BÖLÜMÜ bul
(Örn: Skill=design-system.md, Bölüm=#5-component-sizing)
    │
    ▼
Skill dosyasını KOMPLE OKUMA ❌
Sadece ilgili bölümü ve kuralları oku ✅
```

## 2.2 Adım 2: Selective Reading (Seçici Okuma) Protokolü

**Dosyanın tamamını okumak yerine:**

1. **Hedef Belirle:** İlgili başlığı (örn: `# 5. Component Sizing`) belirle.
2. **Konumu Bul:** Dosyada bu başlığın satır numarasını bul (örn: `view_file_outline` veya `grep_search` ile).
3. **Kısmi Oku:** Sadece o bölümü ve alt maddelerini içeren aralığı oku (örn: `view_file` ile startLine-endLine vererek).

> [!TIP]
> Bu yöntem context limitini korur ve odaklanmayı artırır.

## 2.3 Adım 3: Skill Bulunamazsa
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

{WORKFLOWS_ROOT}/
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
**Versiyon:** 1.3
