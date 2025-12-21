# Global Workflows - Skills System

> [EN] Central skill management system for AI Agents. Appropriate skill(s) are automatically loaded based on the task type.
>
> [TR] AI Agent için merkezi skill yönetim sistemi. Görev tipine göre uygun skill(ler) otomatik olarak yüklenir.

> [!IMPORTANT]
> **[EN] Absolute Paths Notice:** This repository contains absolute directory paths (e.g., `C:\Users\Mehmet\.gemini\antigravity\...`) that **MUST** be updated after cloning to match your local setup. Please update the paths in these files:
> * `.\GEMINI.md`
> * `.\CORE.md`
> * `.\en_version\GEMINI.md`
> * `.\en_version\CORE.md`
>
> **[TR] Mutlak Dizin Yolları Uyarısı:** Bu depoda yerel dizin yapınıza göre **GÜNCELLEMENİZ GEREKEN** mutlak dizin yolları (örn: `C:\Users\Mehmet\.gemini\antigravity\...`) bulunmaktadır. Projeyi klonladıktan sonra şu dosyalardaki yolları güncelleyin:
> * `.\GEMINI.md`
> * `.\CORE.md`
> * `.\en_version\GEMINI.md`
> * `.\en_version\CORE.md`

---

## 🌍 Language Versions / Dil Versiyonları

### 🇹🇷 Turkish (Default)
Original files are located in the root directory and `skills/` folder.
* **GEMINI.md**: `.\GEMINI.md`
* **CORE.md**: `.\CORE.md`
* **Skills**: `.\skills\*.md`

### 🇺🇸 English
Translated files are located in the `en_version` directory. Use these if you prefer an English-native workflow.
* **GEMINI.md**: `.\en_version\GEMINI.md`
* **CORE.md**: `.\en_version\CORE.md`
* **Skills**: `.\en_version\skills\*.md`

---

## 🚀 Installation / Kurulum

### [TR] Türkçe Kurulum
```powershell
Copy-Item ".\GEMINI.md" "$HOME\.gemini\GEMINI.md"
```

### [EN] English Installation
```powershell
Copy-Item ".\en_version\GEMINI.md" "$HOME\.gemini\GEMINI.md"
```

---

## 📁 Structure / Yapı (English Version)

```
global_workflows/en_version/
├── GEMINI.md              # Global rules
├── CORE.md                # Central orchestrator
└── skills/                # Specialized skill files
    ├── ultrathink.md      # Deep thinking protocol
    ├── architecture.md    # System design
    ├── design-system.md   # UI/UX guides
    ├── backend.md         # Server-side development
    ├── mobile.md          # Cross-platform mobile
    ├── testing.md         # TDD & testing strategies
    ├── debugging.md       # Systematic debugging
    ├── refactoring.md     # Code improvement
    ├── production-deployment.md # DevOps/CI-CD
    ├── multi-file-sync.md # Multi-file changes
    ├── dependency-management.md # Package management
    ├── documentation.md   # Technical docs
    └── optimization.md    # System & Flow Optimization [NEW]
```

## 🆕 New Features (v1.3)
- **[EN] Socratic Reality Check:** A 5-step protocol in `ultrathink.md` to align with user intent and prevent context drift.
- **[TR] Sokratik Gerçeklik Kontrolü:** `ultrathink.md` içinde yer alan, kullanıcı niyetini doğrulamak ve bağlam kaymasını önlemek için 5 adımlı protokol.
- **Clickable navigation:** `CORE.md` now features direct links to specific skill sections for precision.
- **Unified Structure:** All skills follow a standardized v2.0 format (ToC + Numbered Sections).
- **New Skills:** Added `optimization` and `testing` skills.

---

## 🎯 How It Works / Nasıl Çalışır?

1. **[EN]** `CORE.md` is read at every task. **[TR]** Her görevde `CORE.md` okunur.
2. **[EN] Selection:** The Agent uses the **Selective Reading Protocol** to only load relevant sections, preserving context limits. **[TR]** Agent, **Seçici Okuma Protokolü** ile sadece ilgili bölümleri yükler, bağlam limitini (token) korur.
3. **[EN] Planning:** `ultrathink.md` is used for deep analysis and **Socratic Reality Check**. **[TR]** `ultrathink.md` ile derin analiz ve **Sokratik Gerçeklik Kontrolü** yapılır.
4. **[EN] Execution:** The identified skill file is loaded from the `skills/` directory. **[TR]** Belirlenen skill dosyası `skills/` dizinden yüklenir.
5. **[EN] Quality:** Mandatory checks (ESLint/TSC) are performed after completion. **[TR]** İşlem sonrası zorunlu kontroller yapılır.

---

## 📏 Rules / Kurallar

- ✅ **[EN]** ESLint/TypeScript check after every change. **[TR]** Her işlemden sonra ESLint/TypeScript kontrolü.
- ✅ **[EN]** Code must be reviewed at least twice. **[TR]** Yazılan kod en az 2 kez review edilmeli.
- ✅ **[EN]** No work starts without loading skills. **[TR]** Skill yüklenene kadar işleme başlanmaz.

---

## 📄 License / Lisans

MIT License

---

**Developed by / Geliştiren:** [@xenit-v0](https://x.com/xenit_v0)
