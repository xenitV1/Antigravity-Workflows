# Antigravity Workflows - AI Agent Skills System

> [EN] Comprehensive AI Agent skill system for Antigravity IDE. Includes rules, workflows, and skills with automatic activation.
>
> [TR] Antigravity IDE için kapsamlı AI Agent yetenek sistemi. Otomatik aktivasyon ile rules, workflows ve skills içerir.

---

## 🚀 Kurulum / Installation

### Windows (PowerShell)

```powershell
# 1. Dizinleri oluştur
New-Item -ItemType Directory -Force -Path "$HOME\.gemini\antigravity\global_workflows"
New-Item -ItemType Directory -Force -Path "$HOME\.agent\rules"
New-Item -ItemType Directory -Force -Path "$HOME\.agent\workflows"

# 2. GEMINI.md -> ~/.gemini/
Copy-Item ".\GEMINI.md" "$HOME\.gemini\GEMINI.md"

# 3. CORE.md -> ~/.gemini/antigravity/
Copy-Item ".\CORE.md" "$HOME\.gemini\antigravity\CORE.md"

# 4. Skills -> ~/.gemini/antigravity/global_workflows/
Copy-Item -Recurse ".\skills" "$HOME\.gemini\antigravity\global_workflows\"

# 5. Antigravity Rules -> ~/.agent/rules/
Copy-Item ".\.agent\rules\*" "$HOME\.agent\rules\" -Recurse

# 6. Antigravity Workflows -> ~/.agent/workflows/
Copy-Item ".\.agent\workflows\*" "$HOME\.agent\workflows\" -Recurse
```

### macOS/Linux (Bash)

```bash
# 1. Dizinleri oluştur
mkdir -p ~/.gemini/antigravity/global_workflows
mkdir -p ~/.agent/rules
mkdir -p ~/.agent/workflows

# 2. GEMINI.md -> ~/.gemini/
cp GEMINI.md ~/.gemini/GEMINI.md

# 3. CORE.md -> ~/.gemini/antigravity/
cp CORE.md ~/.gemini/antigravity/CORE.md

# 4. Skills -> ~/.gemini/antigravity/global_workflows/
cp -r skills ~/.gemini/antigravity/global_workflows/

# 5. Antigravity Rules -> ~/.agent/rules/
cp -r .agent/rules/* ~/.agent/rules/

# 6. Antigravity Workflows -> ~/.agent/workflows/
cp -r .agent/workflows/* ~/.agent/workflows/
```

---

## 📁 Kurulum Sonrası Yapı

```
~/.gemini/
├── GEMINI.md                           # Global kurallar
└── antigravity/
    ├── CORE.md                         # Merkezi orkestratör
    └── global_workflows/
        └── skills/                     # 13 skill dosyası
            ├── ultrathink.md
            ├── architecture.md
            ├── backend.md
            └── ...

~/.agent/                               # Antigravity IDE Native
├── rules/                              # 15 workspace rule
│   ├── ultrathink.md       (Model Decision)
│   ├── quality-gates.md    (Always On)
│   ├── backend.md          (Glob: *.ts, *.js)
│   ├── testing.md          (Glob: *.test.*)
│   └── ...
└── workflows/                          # 8 slash command
    ├── ultrathink.md       (/ultrathink)
    ├── plan.md             (/plan)
    ├── implement.md        (/implement)
    ├── review.md           (/review)
    ├── debug.md            (/debug)
    ├── test.md             (/test)
    ├── refactor.md         (/refactor)
    └── deploy.md           (/deploy)
```

---

## 🔧 Antigravity IDE Rules

### Aktivasyon Modları

| Mod | Açıklama | Örnek |
|-----|----------|-------|
| **Always On** | Her zaman aktif | `quality-gates.md` |
| **Model Decision** | AI karar verir | `ultrathink.md`, `debugging.md` |
| **Glob** | Dosya pattern'ine göre | `*.ts` -> `backend.md` |

### Rule Listesi (15 adet)

| Rule | Aktivasyon | Açıklama |
|------|------------|----------|
| `ultrathink.md` | Model Decision | Derin analiz protokolü |
| `core-orchestrator.md` | Model Decision | Skill yönlendirici |
| `quality-gates.md` | **Always On** | Kalite kontrolleri |
| `backend.md` | Glob: `*.ts, *.js` | Backend geliştirme |
| `testing.md` | Glob: `*.test.*` | Test stratejileri |
| `debugging.md` | Model Decision | Hata ayıklama |
| `architecture.md` | Model Decision | Sistem tasarımı |
| `refactoring.md` | Model Decision | Kod iyileştirme |
| `design-system.md` | Glob: `*.css` | UI tutarlılık |
| `mobile.md` | Glob: `*.tsx, App.*` | Mobil geliştirme |
| `production-deployment.md` | Model Decision | DevOps/CI-CD |
| `multi-file-sync.md` | Model Decision | Çoklu dosya |
| `dependency-management.md` | Glob: `package.json` | Paket yönetimi |
| `documentation.md` | Glob: `*.md` | Dokümantasyon |
| `optimization.md` | Model Decision | Performans |

---

## ⚡ Antigravity Workflows (Slash Commands)

| Workflow | Komut | Açıklama |
|----------|-------|----------|
| `ultrathink.md` | `/ultrathink` | Derin düşünme modu |
| `plan.md` | `/plan` | Görev planlama |
| `implement.md` | `/implement` | Özellik geliştirme |
| `review.md` | `/review` | Kod inceleme |
| `debug.md` | `/debug` | Hata ayıklama |
| `test.md` | `/test` | Test yazma |
| `refactor.md` | `/refactor` | Güvenli refactoring |
| `deploy.md` | `/deploy` | Production deployment |

---

## 🎯 Nasıl Çalışır?

### Antigravity IDE Akışı

```
Kullanıcı komutu verir
        │
        ▼
┌─────────────────────────┐
│ Glob Pattern Kontrolü   │ → *.ts dosyası? -> backend.md aktif
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│ Always On Rules         │ → quality-gates.md her zaman aktif
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│ Model Decision          │ → Karmaşık görev? -> ultrathink.md
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│ Workflow Çağrısı        │ → /debug -> debug.md workflow'u
└─────────────────────────┘
```

### Workflow Zincirleme

```
/plan -> /ultrathink (karmaşık görevler için)
/implement -> /plan + /test
/deploy -> /test + /review
```

---

## 📏 Kurallar

- ✅ Her işlemden sonra ESLint/TypeScript kontrolü
- ✅ Kod en az 2 kez review edilmeli
- ✅ Skill/Rule yüklenmeden işleme başlanmaz
- ✅ Sokratik Gerçeklik Kontrolü (5-Step) her eylemden önce

---

## 🌍 Dil Versiyonları

| Dil | Konum |
|-----|-------|
| 🇹🇷 Türkçe | `./` (root) |
| 🇺🇸 English | `./en_version/` |

---

## 📄 Lisans / License

MIT License

---

**Geliştiren / Developed by:** [@xenit-v0](https://x.com/xenit_v0)
**Versiyon:** 2.0 (Antigravity IDE Native Support)
