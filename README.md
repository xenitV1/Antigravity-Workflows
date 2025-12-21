# Global Workflows - Skills System

> [EN] Central skill management system for AI Agents. Appropriate skill(s) are automatically loaded based on the task type.
>
> [TR] AI Agent için merkezi skill yönetim sistemi. Görev tipine göre uygun skill(ler) otomatik olarak yüklenir.

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
    └── documentation.md   # Technical docs
```

---

## 🎯 How It Works / Nasıl Çalışır?

1. **[EN]** `CORE.md` is read at every task. **[TR]** Her görevde `CORE.md` okunur.
2. **[EN]** Task is analyzed and appropriate skill(s) are identified. **[TR]** Görev analiz edilir ve uygun skill(ler) belirlenir.
3. **[EN]** Skill file is loaded from the `skills/` directory. **[TR]** Skill dosyası `skills/` dizininden yüklenir.
4. **[EN]** Quality checks are performed after completion. **[TR]** İşlem sonrası kalite kontrolleri yapılır.

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
