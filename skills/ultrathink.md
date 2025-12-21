---
name: ultrathink
description: Maksimum düşünme kapasitesi protokolü. Karmaşık mimari, derin analiz, çok adımlı planlama ve kritik karar verme için kullanılır.
metadata:
  skillport:
    category: thinking
    tags:
      - deep-analysis
      - critical-thinking
      - problem-solving
      - decision-making
---

# UltraThink - Derin Analiz Protokolü

> Bu skill **maksimum düşünme kapasitesini** aktive eder.
> Karmaşık problemler için sistematik, çok katmanlı analiz sağlar.

---

# 📋 İçindekiler

1. [Ne Zaman Kullanılmalı?](#1-ne-zaman-kullanılmalı)
2. [Düşünme Derinlik Seviyeleri](#2-düşünme-derinlik-seviyeleri)
3. [Faz 0: Meta-Planlama](#3-faz-0-meta-planlama)
4. [Faz 1: Problem Anlama](#4-faz-1-problem-anlama)
5. [Faz 2: Hipotez Üretimi](#5-faz-2-hipotez-üretimi)
6. [Faz 3: Çözüm Uzayı Keşfi](#6-faz-3-çözüm-uzayı-keşfi)
7. [Faz 4: Kritik Değerlendirme](#7-faz-4-kritik-değerlendirme)
8. [Faz 5: Edge Case Matrisi](#8-faz-5-edge-case-matrisi)
9. [Faz 6: Self-Correction Loop](#9-faz-6-self-correction-loop)
10. [Faz 7: Sentez ve Karar](#10-faz-7-sentez-ve-karar)
11. [Chain-of-Thought Prompt](#11-chain-of-thought-prompt)
12. [Kontrol Listesi](#12-kontrol-listesi)
13. [Yapma Listesi](#13-yapma-listesi)
14. [Mutlaka Yap Listesi](#14-mutlaka-yap-listesi)
15. [Düşünme Araçları Referansı](#15-düşünme-araçları-referansı)

---

# 1. Ne Zaman Kullanılmalı?

| Senaryo | Örnek |
|---------|-------|
| Mimari kararlar | "Monolith'i mikroservislere bölelim mi?" |
| Performans optimizasyonu | "Bu sorgu neden yavaş?" |
| Karmaşık bug analizi | "Race condition nereden kaynaklanıyor?" |
| Çok adımlı refaktör | "Bu 10 dosyayı nasıl refactor edelim?" |
| Sistem tasarımı | "Ölçeklenebilir bir auth sistemi tasarla" |
| Trade-off değerlendirmesi | "SQL vs NoSQL hangisi daha uygun?" |
| Risk analizi | "Bu değişikliğin potansiyel etkileri neler?" |

---

# 2. Düşünme Derinlik Seviyeleri

Problemi analiz ederek uygun derinlik seviyesini belirle:

| Seviye | Adım Sayısı | Ne Zaman? |
|--------|-------------|-----------|
| **Hafif** | 3-5 adım | Basit karar, tek boyutlu problem |
| **Orta** | 8-15 adım | Çoklu bağımlılık, orta karmaşıklık |
| **Derin** | 20-40 adım | Sistem geneli etki, yüksek risk |
| **Ultra** | 50+ adım | Kritik mimari karar, geri dönüşü zor |

---

# 3. Faz 0: Meta-Planlama

Her analize başlamadan ÖNCE şu soruları cevapla:

```markdown
## Meta-Planlama

### Problem Değerlendirmesi
- **Karmaşıklık (1-10):** [Puan]
- **Risk Seviyesi:** [Düşük/Orta/Yüksek/Kritik]
- **Etki Alanı:** [Lokal/Modül/Sistem Geneli]
- **Geri Dönüşü:** [Kolay/Zor/İmkansız]

### Düşünme Bütçesi
- **Tahmini adım sayısı:** [X adım]
- **Derinlik seviyesi:** [Hafif/Orta/Derin/Ultra]
- **Düşünme modu:** [Analitik/Kreatif/Kritik/Sistematik]

### Başarı Kriteri
- Bu analiz ne zaman "yeterli" sayılır?
- Hangi sorular cevaplanmalı?
- Minimum güven seviyesi: [%X]
```

---

# 4. Faz 1: Problem Anlama

## 4.1 Problemi Kendi Kelimelerinle İfade Et

```markdown
## Problem Tanımı

### Orijinal Talep
[Kullanıcının söylediği]

### Benim Anlayışım
[Kendi kelimelerimle problemi tarif et]

### Doğrulama Sorusu
"Doğru anlıyor muyum: [özet]?"
```

## 4.2 Bilgi Haritası

```markdown
## Bilgi Haritası

### ✅ Bilinenler (Kesin)
1. [Bilgi 1] - Kaynak: [nereden biliyoruz?]
2. [Bilgi 2] - Kaynak: [nereden biliyoruz?]

### ❓ Bilinmeyenler (Araştırılmalı)
1. [Soru 1] - Nasıl öğrenebiliriz?
2. [Soru 2] - Nasıl öğrenebiliriz?

### ⚠️ Varsayımlar (Doğrulanmalı)
1. [Varsayım 1] - Yanlışsa ne olur?
2. [Varsayım 2] - Yanlışsa ne olur?
```

## 4.3 Kısıtlar ve Gereksinimler

```markdown
## Kısıtlar

### Teknik Kısıtlar
- [Kısıt 1]
- [Kısıt 2]

### İş Kısıtları
- Zaman: [Süre]
- Bütçe: [Varsa]
- Kaynak: [Mevcut ekip/araç]

### Kalite Gereksinimleri
- Performans: [Metrik]
- Güvenlik: [Seviye]
- Ölçeklenebilirlik: [Hedef]
```

---

# 5. Faz 2: Hipotez Üretimi

## 5.1 İlk Hipotezler

```markdown
## Hipotez Listesi

### H1: [Hipotez Adı]
- **Açıklama:** [Ne olduğunu düşünüyoruz?]
- **Güven:** [%] 
- **Varsayımlar:** [Hangi varsayımlara dayanıyor?]
- **Test yöntemi:** [Nasıl doğrulayabiliriz?]

### H2: [Hipotez Adı]
[Aynı format...]

### H3: [Hipotez Adı]
[Aynı format...]
```

## 5.2 Hipotez Güven Kalibrasyonu

| Güven Seviyesi | Anlamı | Ne Yapmalı? |
|----------------|--------|-------------|
| **90-100%** | Çok güçlü kanıt | Hemen ilerle |
| **70-89%** | İyi kanıt, küçük belirsizlik | İlerle ama izle |
| **50-69%** | Karışık kanıt | Daha fazla analiz |
| **30-49%** | Zayıf kanıt | Alternatif ara |
| **0-29%** | Çok belirsiz | Yeniden düşün |

---

# 6. Faz 3: Çözüm Uzayı Keşfi

## 6.1 En Az 3 Alternatif Üret

```markdown
## Alternatif Çözümler

### Yaklaşım 1: [İsim]
**Açıklama:** [Özet]

| Kriter | Değerlendirme |
|--------|---------------|
| Performans | ⭐⭐⭐⭐⭐ |
| Karmaşıklık | ⭐⭐⭐ |
| Bakım Kolaylığı | ⭐⭐⭐⭐ |
| Uygulama Süresi | [Zaman] |
| Risk | [Düşük/Orta/Yüksek] |

**Avantajlar:**
- [+] ...
- [+] ...

**Dezavantajlar:**
- [-] ...
- [-] ...

---

### Yaklaşım 2: [İsim]
[Aynı format...]

---

### Yaklaşım 3: [İsim]
[Aynı format...]
```

## 6.2 Karşılaştırma Matrisi

```markdown
| Kriter | Ağırlık | Yaklaşım 1 | Yaklaşım 2 | Yaklaşım 3 |
|--------|---------|------------|------------|------------|
| Performans | 30% | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| Karmaşıklık | 20% | ⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐ |
| Maliyet | 25% | $$ | $ | $$$ |
| Risk | 25% | Düşük | Orta | Düşük |
| **TOPLAM** | 100% | [Puan] | [Puan] | [Puan] |
```

---

# 7. Faz 4: Kritik Değerlendirme

## 7.1 Devil's Advocate (Şeytanın Avukatı)

Her çözüm için şu soruları sor:

```markdown
## Kritik Sorular

### Zayıf Noktalar
- "Bu çözümün en zayıf noktası ne?"
- "Nerede başarısız olabilir?"
- "Hangi varsayım yanlış çıkarsa çöker?"

### Dışarıdan Bakış
- "Bir senior developer bunu nasıl eleştirirdi?"
- "6 ay sonra bu kodu gören ben ne düşünürdüm?"
- "Rakip takım buna ne derdi?"

### Ölçek Testi
- "10x yük altında ne olur?"
- "100x kullanıcı olunca?"
- "Data 1000x büyüyünce?"

### Güvenlik
- "OWASP Top 10 kontrol ettim mi?"
- "Hangi saldırı vektörleri açık?"
- "Veri sızıntısı riski var mı?"
```

## 7.2 Pre-Mortem Analizi

```markdown
## Pre-Mortem: "Bu Proje Başarısız Oldu"

Varsay ki 6 ay sonra bu proje BAŞARISIZ oldu. Neden?

### Olası Başarısızlık Nedenleri
1. [Neden 1] - Olasılık: [%]
2. [Neden 2] - Olasılık: [%]
3. [Neden 3] - Olasılık: [%]

### Her Neden İçin Önlem
| Başarısızlık | Önlem | Kimin Sorumluluğu? |
|--------------|-------|-------------------|
| [Neden 1] | [Önlem] | [Kim] |
| [Neden 2] | [Önlem] | [Kim] |
```

---

# 8. Faz 5: Edge Case Matrisi

## 8.1 Input Edge Cases

| Senaryo | Normal | Edge Case | Strateji |
|---------|--------|-----------|----------|
| Veri tipi | String | null/undefined | Default değer + log |
| Uzunluk | 1-100 char | 0 veya 10000+ | Validation + truncate |
| Format | UTF-8 | Emoji/Special chars | Sanitization |
| Boyut | <1MB | >100MB | Streaming + chunk |

## 8.2 State Edge Cases

| Senaryo | Normal | Edge Case | Strateji |
|---------|--------|-----------|----------|
| Concurrency | Sequential | Parallel writes | Mutex/Lock |
| Timing | <100ms | Timeout | Retry + fallback |
| Connection | Online | Offline | Queue + sync |
| Memory | Normal | High usage | GC + cleanup |

## 8.3 Business Edge Cases

| Senaryo | Normal | Edge Case | Strateji |
|---------|--------|-----------|----------|
| User | Active | Deleted mid-op | Graceful abort |
| Permission | Authorized | Role changed | Re-check + deny |
| Data | Complete | Partial/corrupt | Validation + reject |

---

# 9. Faz 6: Self-Correction Loop

## 9.1 Metacognitive Checkpoints

Her fazdan sonra şu soruları sor:

```markdown
## Metacognitive Check

### İlerleme Kontrolü
- [ ] İlerleme kaydediliyor mu, yoksa döngüde miyim?
- [ ] Bu analiz derinliği problem için yeterli mi?
- [ ] Önemli bir şeyi atlıyor olabilir miyim?

### Güven Kalibrasyonu
- Şu anki güven seviyem: [%]
- Bu güven seviyesi gerçekçi mi?
- Daha fazla kanıt gerekli mi?

### Revizyon İhtiyacı
- [ ] Önceki düşüncelerimi revize etmem gerekiyor mu?
- [ ] Hangi varsayımım değişti?
- [ ] Yeni bilgi hipotezlerimi nasıl etkiliyor?
```

## 9.2 Bias Tespiti ve Düzeltme

| Bias | Tehlike | Kontrol Sorusu | Düzeltme |
|------|---------|----------------|----------|
| **Anchoring** | İlk fikre takılma | "İlk fikrim en iyisi mi gerçekten?" | 3+ alternatif üret |
| **Confirmation** | Destekleyici kanıt arama | "Karşı kanıt aradım mı?" | Aktif olarak çürütmeye çalış |
| **Availability** | Akla gelen ilk örnek | "Base rate nedir?" | İstatistik/veri ara |
| **Sunk Cost** | Yatırımdan vazgeçememe | "Sıfırdan başlasam ne yapardım?" | Fresh evaluation |
| **Overconfidence** | Fazla güven | "Nasıl yanılabilirim?" | %10 hata payı ekle |

---

# 10. Faz 7: Sentez ve Karar

## 10.1 Final Karar Şablonu

```markdown
# 🧠 UltraThink Analiz Raporu

## Özet
[2-3 cümleyle ana bulguları özetle]

## Seçilen Çözüm
**Yaklaşım:** [İsim]
**Güven Seviyesi:** [%]
**Gerekçe:** [Neden bu seçildi - 2-3 cümle]

## Reddedilen Alternatifler
1. **[Alternatif 1]** - Red nedeni: [Kısa açıklama]
2. **[Alternatif 2]** - Red nedeni: [Kısa açıklama]

## Risk Matrisi
| Risk | Olasılık | Etki | Önlem |
|------|----------|------|-------|
| [Risk 1] | [%] | [Düşük/Orta/Yüksek] | [Strateji] |
| [Risk 2] | [%] | [Düşük/Orta/Yüksek] | [Strateji] |

## Aksiyon Planı
1. [ ] **Adım 1:** [Açıklama] - [Süre]
2. [ ] **Adım 2:** [Açıklama] - [Süre]
3. [ ] **Adım 3:** [Açıklama] - [Süre]

## Başarı Kriterleri
- [ ] [Kriter 1]
- [ ] [Kriter 2]
- [ ] [Kriter 3]

## Gözden Geçirme Tarihi
Bu karar [tarih] tarihinde yeniden değerlendirilmeli.
```

---

# 11. Chain-of-Thought Prompt

```
"Bu problemi çözerken şu adımları takip edeceğim:

1. META-PLANLAMA: Önce problemi değerlendir, karmaşıklığı belirle
2. ANLAMA: Problemi kendi kelimelerimle ifade et, bilinen/bilinmeyen ayır
3. HİPOTEZ: En az 3 hipotez üret, her birinin güven seviyesini belirle
4. ALTERNATİF: En az 3 çözüm yolu üret, karşılaştır
5. KRİTİK: Her çözümü sorgula, devil's advocate ol
6. EDGE CASE: Beklenmedik durumları listele
7. SELF-CHECK: Kendi düşüncemi sorgula, bias kontrol et
8. KARAR: Final kararı gerekçesiyle ver

Her adımda:
- Güven seviyemi belirt (%0-100)
- Belirsizlikleri işaretle
- Varsayımları açıkla
- Alternatif görüşleri değerlendir

Düşünme tamamlanana kadar cevap verme. Adımları göster."
```

---

# 12. Kontrol Listesi

Her UltraThink analizi için:

- [ ] Meta-planlama yapıldı (karmaşıklık, derinlik belirlendi)
- [ ] Problem 3 farklı açıdan ifade edildi
- [ ] En az 3 hipotez üretildi
- [ ] En az 3 çözüm alternatifi değerlendirildi
- [ ] Devil's advocate soruları soruldu
- [ ] Pre-mortem analizi yapıldı
- [ ] Edge case'ler listelendi
- [ ] Bias kontrolü yapıldı
- [ ] Güven seviyesi kalibre edildi
- [ ] Final karar gerekçelendirildi

---

# 13. Yapma Listesi

❌ İlk aklına gelen çözümü hemen uygulama
❌ Tek bir perspektiften bakma
❌ Varsayımları sorgulamadan kabul etme
❌ Alternatif üretmeden karar verme
❌ Edge case'leri düşünmeden kodlama
❌ Güven seviyeni %100 olarak gösterme
❌ Bias kontrolünü atlama
❌ Kararı gerekçelendirmeden verme

---

# 14. Mutlaka Yap Listesi

✅ Her problemi en az 3 farklı açıdan değerlendir
✅ Minimum 3 alternatif çözüm üret
✅ Her kararın güven seviyesini belirt
✅ Varsayımları açıkça yaz
✅ "Nasıl yanılabilirim?" sorusunu sor
✅ Edge case'leri listele ve stratejilerini belirle
✅ Kararını gerekçelendir
✅ Aksiyon planı ver
✅ Başarı kriterlerini tanımla

---

# 15. Düşünme Araçları Referansı

| Araç | Ne Zaman? | Nasıl? |
|------|-----------|--------|
| **First Principles** | Karmaşık problem | En temel gerçeklere in, oradan yapılandır |
| **Inversion** | Risk analizi | "Ne YAPMAMALIYIM?" sorusu |
| **Analogy** | Yeni problem | Benzer çözülmüş problemleri ara |
| **Systems Thinking** | Karmaşık sistem | Parçalar arası etkileşimi haritalandır |
| **Probabilistic** | Belirsizlik | Olasılıkları tahmin et ve güncelle |
| **Red Team** | Karar doğrulama | Kendi çözümüne saldır |

---

**Son Güncelleme:** Aralık 2025
**Versiyon:** 3.0
