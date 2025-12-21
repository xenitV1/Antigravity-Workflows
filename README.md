# Global Workflows - Skills System

> AI Agent için merkezi skill yönetim sistemi. Görev tipine göre uygun skill(ler) otomatik olarak yüklenir.

## 🚀 Kurulum

1. Bu repository'yi klonlayın
2. `GEMINI.md` dosyasını sistem dizinine kopyalayın:

```powershell
Copy-Item ".\GEMINI.md" "C:\Users\Mehmet\.gemini\GEMINI.md"
```

## 📁 Yapı

```
global_workflows/
├── GEMINI.md              # Global kurallar (sistem dizinine kopyalanmalı)
├── CORE.md                # Merkezi orchestrator
└── skills/
    ├── ultrathink.md      # Derin düşünme protokolü
    ├── architecture.md    # Sistem tasarımı
    ├── design-system.md   # UI/UX rehberi
    ├── backend.md         # Server-side geliştirme
    ├── mobile.md          # Cross-platform mobile
    ├── testing.md         # TDD ve test stratejileri
    ├── debugging.md       # Sistematik hata ayıklama
    ├── refactoring.md     # Güvenli kod iyileştirme
    ├── production-deployment.md # DevOps/CI-CD
    ├── multi-file-sync.md # Çoklu dosya değişikliği
    ├── dependency-management.md # Paket yönetimi
    └── documentation.md   # Teknik dokümantasyon
```

## 🎯 Nasıl Çalışır?

1. Her görevde `CORE.md` okunur
2. Görev analiz edilir ve uygun skill(ler) belirlenir
3. Skill dosyası `skills/` dizininden yüklenir
4. İşlem tamamlandıktan sonra kod kalite kontrolleri yapılır

## 📏 Kurallar

- ✅ Her işlemden sonra ESLint/TypeScript kontrolü
- ✅ Yazılan kod en az 2 kez review edilmeli
- ✅ Skill yüklenmeden işleme başlanmaz

## 🔗 Skill Kategorileri

| Kategori | Skills |
|----------|--------|
| **Düşünme** | ultrathink, architecture |
| **Geliştirme** | backend, mobile, design-system |
| **Kalite** | testing, debugging, refactoring |
| **Operasyon** | production-deployment, multi-file-sync, dependency-management, documentation |

## 📄 Lisans

MIT License
