---
description: MultiFileSync - Çoklu Dosya Senkronizasyon Modu
---

MultiFileSync: Çoklu dosya değişikliklerinde tutarlılık. Strateji: 1) Tüm etkilenen dosyaları önce listele, 2) Değişiklik sırasını bağımlılıklara göre planla, 3) Her dosya için değişiklik öncesi durumu kaydet, 4) Değişiklikleri sırayla uygula, 5) Her adımda çapraz referansları kontrol et, 6) Tüm dosyalar tutarlı hale gelene kadar commit yapma. Dosyalar arası interface'lerin uyumlu kalmasını garanti et.