---
description: Global agent kuralları. Tüm işlemlerde CORE.md yönergelerine uyulmalı ve uygun skills yüklenmelidir.
---

# GEMINI.md - Global Agent Kuralları

> Bu dosya sistemin temel çalışma kurallarını tanımlar.
> Her görev başlangıcında bu kurallar geçerlidir.

---

## 🚨 MUTLAK KURALLAR (Her Zaman Geçerli)

### 1. CORE.md Zorunluluğu

Kullanıcı herhangi bir görev verdiğinde:

1. **ÖNCE** `c:\Users\Mehmet\Desktop\global_workflows\CORE.md` dosyası okunmalıdır
2. CORE.md, görev tipine göre uygun skill(ler)i belirler
3. Belirlenen skill dosyası `skills/` dizininden yüklenir
4. Skill yüklenene kadar işleme **BAŞLANMAZ**

```
Görev Geldi
    │
    ▼
┌─────────────────┐
│  CORE.md Oku    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Skill(ler)i     │
│ Belirle         │
└────────┬────────┘
         │
         ▼
┌─────────────────┐     Hayır    ┌──────────────────┐
│ Skill Bulundu   │─────────────▶│ Kullanıcıdan     │
│ mu?             │              │ Dosya Yolu İste  │
└────────┬────────┘              └──────────────────┘
         │ Evet
         ▼
┌─────────────────┐
│ Skill'i Yükle   │
│ ve İşleme Başla │
└─────────────────┘
```

---

### 2. Skill Yükleme Protokolü

**Skill Bulunamazsa:**
```
⚠️ "[skill-name].md" skill dosyası bulunamadı.
Lütfen dosya yolunu gösterin veya skill dosyasını oluşturun.
Skills olmadan işleme başlanamaz.
```

**Skill Konumu:**
```
c:\Users\Mehmet\Desktop\global_workflows\skills\<skill-name>.md
```

---

### 3. Kod Kalite Kontrolleri (Her İşlem Sonrası)

Her kod değişikliğinden SONRA şu kontroller **MUTLAKA** yapılmalıdır:

#### ✅ Zorunlu Kontroller

| Kontrol | Komut | Açıklama |
|---------|-------|----------|
| **ESLint** | `npx eslint .` | Kod kalitesi ve stil kontrolü |
| **TypeScript** | `npx tsc --noEmit` | Tip güvenliği kontrolü |
| **Prettier** | `npx prettier --check .` | Kod formatlama kontrolü |

#### ✅ 2x Kod Review Kuralı

Yazılan kod **EN AZ 2 KERE** kontrol edilmelidir:

**1. İlk Kontrol (Yazım Sonrası):**
- Syntax hataları var mı?
- Değişken isimleri anlamlı mı?
- Import'lar doğru mu?

**2. İkinci Kontrol (Final Review):**
- Edge case'ler düşünüldü mü?
- Error handling yeterli mi?
- Type safety sağlandı mı?
- Best practices uygulandı mı?

---

### 4. İşlem Sonrası Kontrol Listesi

Her kod değişikliğinden sonra bu listeyi kontrol et:

```markdown
## ✅ Son Kontrol Listesi

### Kod Kalitesi
- [ ] ESLint hatası yok
- [ ] TypeScript hatası yok
- [ ] Kod 2. kez review edildi

### Güvenlik & Güvenilirlik
- [ ] Input validation yapıldı
- [ ] Error handling eklendi
- [ ] Edge case'ler düşünüldü

### Temizlik
- [ ] Kullanılmayan import yok
- [ ] Console.log temizlendi
- [ ] Gereksiz yorum yok
```

---

## 🔧 Skill Kategorileri

| Kategori | Skills | Kullanım |
|----------|--------|----------|
| **Düşünme** | `ultrathink`, `architecture` | Derin analiz, sistem tasarımı |
| **Geliştirme** | `backend`, `mobile`, `design-system` | Kod yazma |
| **Kalite** | `testing`, `debugging`, `refactoring` | Kalite güvence |
| **Operasyon** | `production-deployment`, `multi-file-sync`, `dependency-management`, `documentation` | Süreç yönetimi |

---

## 🎯 Örnek Akış

```
Kullanıcı: "User authentication API'si oluştur"

Agent:
1. CORE.md okundu
2. Görev analizi: Backend geliştirme + Güvenlik
3. Skill belirleme: backend.md
4. skills/backend.md yüklendi
5. İşleme başlanıyor...

[Kod yazıldı]

6. ✅ ESLint kontrolü yapıldı
7. ✅ TypeScript kontrolü yapıldı
8. ✅ Kod 2. kez review edildi
9. İşlem tamamlandı
```

---

## ⚠️ Kritik Uyarılar

> [!CAUTION]
> Skills yüklenmeden KOD YAZMA!

> [!WARNING]
> ESLint/TypeScript kontrolü yapılmadan işlemi TAMAMLAMA!

> [!IMPORTANT]
> Her kod değişikliği 2 KERE kontrol edilmeli!

---

**Son Güncelleme:** Aralık 2025
**Versiyon:** 1.0
