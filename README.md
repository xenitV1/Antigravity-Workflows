# Global Workflows - Skills System

> [EN] Central skill management system for AI Agents. Appropriate skill(s) are automatically loaded based on the task type.
>
> [TR] AI Agent için merkezi skill yönetim sistemi. Görev tipine göre uygun skill(ler) otomatik olarak yüklenir.

---

## 🚀 Installation / Kurulum

1. Clone this repository / Bu repository'yi klonlayın
2. Copy `GEMINI.md` to your system directory / `GEMINI.md` dosyasını sistem dizinine kopyalayın:

```powershell
Copy-Item ".\GEMINI.md" "$HOME\.gemini\GEMINI.md"
```

---

## 📁 Structure / Yapı

```
global_workflows/
├── GEMINI.md              # Global rules / Global kurallar
├── CORE.md                # Central orchestrator / Merkezi orchestrator
└── skills/                # Specialized skill files / Özelleşmiş skill dosyaları
    ├── ultrathink.md      # Deep thinking protocol / Derin düşünme protokolü
    ├── architecture.md    # System design / Sistem tasarımı
    ├── design-system.md   # UI/UX guides / UI/UX rehberi
    ├── backend.md         # Server-side development / Server-side geliştirme
    ├── mobile.md          # Cross-platform mobile / Mobil geliştirme
    ├── testing.md         # TDD & testing strategies / Test stratejileri
    ├── debugging.md       # Systematic debugging / Hata ayıklama
    ├── refactoring.md     # Code improvement / Kod iyileştirme
    ├── production-deployment.md # DevOps/CI-CD
    ├── multi-file-sync.md # Multi-file changes / Çoklu dosya senkronizasyonu
    ├── dependency-management.md # Package management / Paket yönetimi
    └── documentation.md   # Technical docs / Teknik dokümantasyon
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

## 🔗 Skill Categories / Kategoriler

| Category / Kategori | Skills |
|:---:|---|
| **Thinking / Düşünme** | ultrathink, architecture |
| **Dev / Geliştirme** | backend, mobile, design-system |
| **Quality / Kalite** | testing, debugging, refactoring |
| **Ops / Operasyon** | production-deployment, multi-file-sync, dependency-management, documentation |

---

## 📄 License / Lisans

MIT License
