---
description: MOD SEÇİM MATRİSİ
---

# AI MOD YÖNLENDİRME

> **KULLANIM:** "ai-modes.md'ye göre ilerle" → AI bu dosyaya bakıp uygun modu seçer

---

## MOD SEÇİM KURALLARI

### GÖREVİN TİPİNE GÖRE:

**Karmaşık Görevler / Planlama:**
- Modlar: `UltraThink`, `ArchitectMode`, `ContextKeeper`
- Tetikleyici: "karmaşık", "plan yap", "tasarla", "mimari", "büyük özellik", "analiz et", "çok adımlı"
- Kullanım: Hem planlama hem de karmaşık implementasyon aşamalarında

**Kod Yazma:**
- Modlar: `AgentGuard`, `FileAware`, `StepByStep`
- Tetikleyici: "oluştur", "yaz", "implement", "geliştir"
- ⚠️ AgentGuard + FileAware ZORUNLU

**Hata Düzeltme:**
- Modlar: `DebugMaster`, `TestFirst`
- Tetikleyici: "bug", "hata", "çalışmıyor", "fix"

**Refaktör:**
- Modlar: `RefactorSafe`, `MultiFileSync`, `TestFirst`
- Tetikleyici: "refactor", "optimize", "temizle"

**Test Yazma:**
- Modlar: `TestFirst`, `FileAware`
- Tetikleyici: "test", "TDD", "coverage"

**Terminal İşlemi:**
- Modlar: `SafeExecutor`
- Tetikleyici: "komut", "çalıştır", "install", "script"
- ⚠️ ZORUNLU

**Çoklu Dosya:**
- Modlar: `MultiFileSync`, `FileAware`, `ContextKeeper`
- Tetikleyici: "birçok dosya", "tüm proje", "global değişiklik"

**Paket Yönetimi:**
- Modlar: `DependencyCheck`, `AgentGuard`
- Tetikleyici: "paket ekle", "npm", "yarn", "dependency"

**Dokümantasyon:**
- Modlar: `DocuGen`
- Tetikleyici: "dokümante et", "README", "açıklama ekle"

---

## MOD DOSYALARI

Her mod için ayrı dosya: `modes/` klasörü

```
C:\Users\Mehmet\.gemini\antigravity\global_workflows
├── ultrathink.md
├── agentguard.md
├── contextkeeper.md
├── safeexecutor.md
├── stepbystep.md
├── testfirst.md
├── fileaware.md
├── architectmode.md
├── debugmaster.md
├── refactorsafe.md
├── docugen.md
├── dependencycheck.md
└── multifilesync.md
├── productionsafe.md
```

---

## AI SÜRECİ

1. Kullanıcı görevini oku
2. Bu dosyadaki matristen hangi mod(lar) gerekli belirle
3. Sadece ilgili mod dosyalarını oku (`\global_workflows` klasöründen)
4. Seçilen modları aktif et ve görevi yerine getir

---

## ZORUNLU MODLAR

- **AgentGuard** → Her kod yazma işleminde
- **FileAware** → Her dosya işleminde
- **SafeExecutor** → Her terminal komutunda
- **StepByStep** → Production kodunda