---
name: design-system
description: Provides the official web design system guidelines including 8-point grid spacing, typography scale, color system, and component sizing rules. Use when designing or implementing UI components to ensure visual consistency and adherence to the project's design standards.
metadata:
  skillport:
    category: design
    tags:
      - design-system
      - ui
      - consistency
      - spacing
---

# Web Tasarım Oran-Orantı ve Tutarlılık Rehberi

## 🎯 Genel Prensip

Her tasarım elementi matematiksel olarak tutarlı bir sistem içinde olmalı. Rastgele değerler kullanılmamalı, her ölçü bilinçli bir seçim olmalı.

---

# 📋 İçindekiler

1. [Spacing System (8-Point Grid)](#1-spacing-system-8-point-grid)
2. [Layout & Grid System](#2-layout--grid-system)
3. [Typography Scale (Type Scale)](#3-typography-scale-type-scale)
4. [Color System](#4-color-system)
5. [Component Sizing](#5-component-sizing)
6. [Responsive Breakpoints](#6-responsive-breakpoints)
7. [Visual Hierarchy](#7-visual-hierarchy)
8. [Animation & Transitions](#8-animation--transitions)
9. [White Space Rules](#9-white-space-rules)
10. [Micro-interactions](#10-micro-interactions)
11. [Modern CSS Features (2025)](#11-modern-css-features-2025)
12. [Accessibility Standards](#12-accessibility-standards)
13. [Kontrol Listesi](#13-kontrol-listesi)
14. [Yapay Zekaya Özel Prompt Örneği](#14-yapay-zekaya-özel-prompt-örneği)
15. [Chain-of-Thought Prompt (Adım Adım Düşünme)](#15-chain-of-thought-prompt-adım-adım-düşünme)
16. [Dinamik Karar Alma - Bağlamsal Esneklik](#16-dinamik-karar-alma---bağlamsal-esneklik)
17. [Gerçek Dünya Örnekleri](#17-gerçek-dünya-örnekleri)
18. [Ana Prensipler](#18-ana-prensipler)
19. [Esneklik vs Tutarlılık Dengesi](#19-esneklik-vs-tutarlılık-dengesi)
20. [Akıllı Prompt Ekleme](#20-akıllı-prompt-ekleme)
21. [Self-Correction Prompt](#21-self-correction-prompt)
22. [Referanslar ve Kaynaklar](#22-referanslar-ve-kaynaklar)

---

# 1. Spacing System (8-Point Grid)

## 1.1 Temel Kural

Tüm boşluklar 8'in katları olmalı. Bu modern UI/UX'in altın standardıdır.

```
4px   - Minimum spacing (micro interactions)
8px   - XS - Çok küçük boşluklar
16px  - SM - Küçük boşluklar (icon-text arası)
24px  - MD - Orta boşluklar (card içi elementler)
32px  - LG - Büyük boşluklar (component'ler arası)
48px  - XL - Section içi gruplar
64px  - 2XL - Section'lar arası
96px  - 3XL - Major section'lar arası
128px - 4XL - Hero section padding
```

## 1.2 Padding Yapısı

- **Card/Container içi padding**: 24px veya 32px
- **Button padding**: Dikey 12px, Yatay 24px
- **Input field padding**: Dikey 12px, Yatay 16px
- **Section padding**: 64px - 96px (Desktop), 32px - 48px (Mobile)

> **12px Hakkında Not**: 12px tam olarak 8'in katı değildir (1.5× base unit) ancak compact touch-friendly tasarımlar için endüstri standardı olarak kabul edilir. Alternatif: 8px (daha tight) veya 16px (daha spacious).

---

# 2. Layout & Grid System

## 2.1 Container Sistem

```
Mobile:     100% width, 16px side padding
Tablet:     768px max-width, 24px side padding  (8 × 96 = 768)
Desktop:    1200px max-width, 32px side padding
Wide:       1440px max-width, 48px side padding
```

> Tüm max-width değerleri 8'in katıdır: 768, 1200, 1440

## 2.2 Grid Columns

- **Desktop**: 12 column grid, 24px gutter
- **Tablet**: 8 column grid, 16px gutter
- **Mobile**: 4 column grid, 16px gutter

## 2.3 Aspect Ratios

Görseller ve medya için standart oranlar:

- **Hero images**: 16:9 veya 21:9
- **Card images**: 4:3 veya 1:1
- **Portrait**: 3:4
- **Avatar**: 1:1 (perfect square)
- **Video embed**: 16:9

---

# 3. Typography Scale (Type Scale)

## 3.1 Modern Font Sizing (Practical Scale - Tailwind Based)

> Not: Bu scale matematiksel Major Third (1.250) değil, pratik kullanım için optimize edilmiş Tailwind-style bir scale'dir.

```
12px  - Caption / Helper text
14px  - Small text / Metadata
16px  - Body text (Base size)
18px  - (Optional) Large body for reading
20px  - Lead paragraph / Large body
24px  - H4 / Small heading
32px  - H3 / Medium heading
40px  - H2 / Large heading
48px  - H1 / Display heading
64px  - Hero heading
80px  - Extra large display
```

## 3.2 Line Height Oranları

- **Başlıklar (H1-H3)**: 1.2 - 1.3
- **Body text**: 1.5 - 1.6
- **Small text**: 1.4
- **Hero text**: 1.1

## 3.3 Font Weight Hierarchy

```
300 - Light (Decorative use only)
400 - Regular (Body text)
500 - Medium (Subtle emphasis)
600 - Semibold (Subheadings, buttons)
700 - Bold (Headings)
800 - Extra bold (Hero sections)
```

## 3.4 Letter Spacing (Tracking)

- **Büyük başlıklar (48px+)**: -0.02em (tighter)
- **Normal başlıklar**: 0
- **Body text**: 0
- **Small caps / Uppercase**: 0.05em - 0.1em (looser)
- **Button text**: 0.02em

---

# 4. Color System

## 4.1 Contrast Ratios (WCAG 2.1)

- **Normal text**: Minimum 4.5:1
- **Large text (18px+)**: Minimum 3:1
- **UI components**: Minimum 3:1
- **AAA standart**: 7:1 (ideal)

## 4.2 Renk Paleti Yapısı

```
Primary: 10 shades (50, 100, 200...900, 950)
Secondary: 10 shades
Neutral/Gray: 10 shades
Success: 5 shades (200, 400, 600, 800, 900)
Warning: 5 shades
Error: 5 shades
Info: 5 shades
```

## 4.3 Opacity Scale

```
100% - Tam opak (default)
90%  - Subtle reduction
75%  - Disabled states
60%  - Placeholder text
40%  - Dividers
20%  - Subtle backgrounds
10%  - Hover overlays
5%   - Very subtle tints
```

---

# 5. Component Sizing

## 5.1 Button Sizes

```
Small:   Height 32px, Padding 8px 16px, Font 14px
Medium:  Height 40px, Padding 12px 24px, Font 16px (Default)
Large:   Height 48px, Padding 14px 32px, Font 18px
XLarge:  Height 56px, Padding 16px 40px, Font 20px
```

## 5.2 Border Radius System

```
0px    - None (sharp corners)
2px    - Subtle (inputs)
4px    - Small (buttons, badges)
8px    - Medium (cards, modals) ← Default
16px   - Large (feature cards, hero sections)
24px   - XL (special components)
9999px - Full rounded (pills, avatars)
```

> Not: 12px yaygın kullanılsa da 8-point grid'e tam uymaz. Tutarlılık için 8px veya 16px tercih edin.

## 5.3 Icon Sizes

```
16px - Small icons (inline with text)
20px - Medium icons (buttons)
24px - Large icons (standalone)
32px - XL icons (feature highlights)
48px - 2XL icons (hero sections)
64px - 3XL icons (special features)
```

---

# 6. Responsive Breakpoints

## 6.1 Standard Breakpoints

```
Mobile:       0px - 639px
Tablet SM:    640px - 767px
Tablet:       768px - 1023px  (iPad portrait için kritik)
Desktop:      1024px - 1439px
Wide Desktop: 1440px+
```

## 6.2 Tailwind CSS Breakpoint Mapping

```
sm:  640px   → Tablet small
md:  768px   → Tablet
lg:  1024px  → Desktop
xl:  1280px  → Large desktop
2xl: 1536px  → Wide screens
```

## 6.3 Responsive Font Scaling

```css
/* Modern Fluid Typography Formula (2025) */
font-size: clamp(min, preferred, max)

/* CSS Custom Properties ile */
:root {
  /* Fluid type scale */
  --fluid-xs: clamp(0.75rem, 0.7rem + 0.25vw, 0.875rem); /* 12-14px */
  --fluid-sm: clamp(0.875rem, 0.8rem + 0.35vw, 1rem); /* 14-16px */
  --fluid-base: clamp(1rem, 0.9rem + 0.5vw, 1.125rem); /* 16-18px */
  --fluid-lg: clamp(1.25rem, 1rem + 1vw, 1.5rem); /* 20-24px */
  --fluid-xl: clamp(1.5rem, 1.2rem + 1.5vw, 2rem); /* 24-32px */
  --fluid-2xl: clamp(2rem, 1.5rem + 2.5vw, 3rem); /* 32-48px */
  --fluid-3xl: clamp(2.5rem, 2rem + 3vw, 4rem); /* 40-64px */
  --fluid-4xl: clamp(3rem, 2rem + 4vw, 5rem); /* 48-80px */
}

/* Kullanım */
h1 {
  font-size: var(--fluid-3xl);
}
h2 {
  font-size: var(--fluid-2xl);
}
h3 {
  font-size: var(--fluid-xl);
}
p {
  font-size: var(--fluid-base);
}
```

## 6.4 Fluid Spacing (Bonus)

```css
:root {
  --space-xs: clamp(0.5rem, 0.4rem + 0.5vw, 0.75rem); /* 8-12px */
  --space-sm: clamp(0.75rem, 0.6rem + 0.75vw, 1rem); /* 12-16px */
  --space-md: clamp(1rem, 0.8rem + 1vw, 1.5rem); /* 16-24px */
  --space-lg: clamp(1.5rem, 1rem + 2vw, 2.5rem); /* 24-40px */
  --space-xl: clamp(2rem, 1.5rem + 2.5vw, 4rem); /* 32-64px */
  --space-2xl: clamp(3rem, 2rem + 4vw, 6rem); /* 48-96px */
}
```

---

# 7. Visual Hierarchy

## 7.1 Z-Index Scale (Layering)

```
-1    - Behind content
0     - Base layer
10    - Dropdown menus
20    - Sticky headers
30    - Modals backdrop
40    - Modal content
50    - Tooltips
100   - Toast notifications
9999  - Emergency top layer
```

## 7.2 Shadow System (Elevation)

```
shadow-xs:   0 1px 2px rgba(0,0,0,0.05)
shadow-sm:   0 1px 3px rgba(0,0,0,0.1)
shadow-md:   0 4px 6px rgba(0,0,0,0.1)
shadow-lg:   0 10px 15px rgba(0,0,0,0.1)
shadow-xl:   0 20px 25px rgba(0,0,0,0.1)
shadow-2xl:  0 25px 50px rgba(0,0,0,0.15)
```

## 7.3 Focus States

- **Ring width**: 2px - 4px
- **Ring offset**: 2px
- **Ring color**: Primary color at 50% opacity
- **Outline style**: Solid, never dashed

## 7.4 Focus Visible (Modern Approach)

```css
/* Keyboard navigation için focus göster */
:focus-visible {
  outline: 2px solid var(--primary-500);
  outline-offset: 2px;
}

/* Mouse click için focus gizle */
:focus:not(:focus-visible) {
  outline: none;
}

/* Dark background için daha kalın offset */
.dark :focus-visible {
  outline-offset: 4px;
}
```

> **Best Practice**: `:focus-visible` kullanarak sadece keyboard navigation'da focus ring göster. Bu, mouse kullanıcıları için daha temiz bir deneyim sağlar.

---

# 8. Animation & Transitions

## 8.1 Duration Scale

```
75ms   - Instant (very subtle)
150ms  - Fast (hover states)
200ms  - Normal (default transition)
300ms  - Moderate (dropdown, modal)
500ms  - Slow (page transitions)
700ms  - Very slow (special effects)
```

## 8.2 Easing Functions

```
ease-in:      Başlangıç yavaş (cubic-bezier(0.4, 0, 1, 1))
ease-out:     Bitiş yavaş (cubic-bezier(0, 0, 0.2, 1)) - En çok kullanılan
ease-in-out:  İkisi de (cubic-bezier(0.4, 0, 0.2, 1))
ease-bounce:  Spring effect için
```

---

# 9. White Space Rules

## 9.1 Content Density

- **Tight**: 8px - 12px spacing (Data tables)
- **Normal**: 16px - 24px spacing (Default)
- **Relaxed**: 32px - 48px spacing (Marketing pages)
- **Spacious**: 64px+ spacing (Luxury/Premium)

## 9.2 Reading Width

- **Optimal**: 60-75 characters per line (600px - 750px)
- **Maximum**: 90 characters
- **Minimum**: 45 characters

### Paragraph Spacing

- **Between paragraphs**: 1.5em - 2em
- **Between sections**: 3em - 4em

---

# 10. Micro-interactions

## 10.1 Button States

```
Default:  Base state
Hover:    Lighten/Darken 10%, Scale 1.02, Shadow increase
Active:   Scale 0.98, Shadow decrease
Focus:    Ring outline
Disabled: Opacity 50%, Cursor not-allowed
```

## 10.2 Loading States

- **Skeleton width**: 100%, 75%, 50% (varied)
- **Animation duration**: 1500ms
- **Shimmer effect**: Linear gradient moving

---

# 11. Modern CSS Features (2025)

## 11.1 Container Queries

Component-based responsive tasarım için viewport yerine container'a göre stil uygula:

```css
/* Container tanımla */
.card-container {
  container-type: inline-size;
  container-name: card;
}

/* Container genişliğine göre stil */
@container card (min-width: 400px) {
  .card-content {
    display: grid;
    grid-template-columns: 1fr 2fr;
  }
}

@container card (max-width: 399px) {
  .card-content {
    display: flex;
    flex-direction: column;
  }
}
```

## 11.2 System Preferences (User Preferences)

Kullanıcının sistem tercihlerine göre uyum sağla:

```css
/* Dark mode preference */
@media (prefers-color-scheme: dark) {
  :root {
    --bg-primary: #0a0a0a;
    --text-primary: #fafafa;
  }
}

/* Reduced motion preference */
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}

/* High contrast preference */
@media (prefers-contrast: high) {
  :root {
    --border-color: currentColor;
    --focus-ring-width: 3px;
  }
}

/* Reduced transparency preference */
@media (prefers-reduced-transparency: reduce) {
  .glassmorphism {
    backdrop-filter: none;
    background: var(--bg-solid);
  }
}
```

## 11.3 CSS Logical Properties

LTR/RTL desteği için fiziksel yerine mantıksal özellikler kullan:

```css
/* Eskisi (LTR only) */
.old-way {
  margin-left: 16px;
  padding-right: 24px;
  border-left: 2px solid;
}

/* Yenisi (LTR & RTL) */
.new-way {
  margin-inline-start: 16px;
  padding-inline-end: 24px;
  border-inline-start: 2px solid;
}
```

---

# 12. Accessibility Standards

## 12.1 Touch Targets

- **Minimum size**: 44x44px (Apple) / 48x48px (Google)
- **Optimal size**: 48x48px veya daha büyük
- **Spacing between**: Minimum 8px

## 12.2 Focus Indicators

- **Visibility**: Her zaman görünür olmalı
- **Contrast**: 3:1 minimum (background ile)
- **Thickness**: Minimum 2px

---

# 13. Kontrol Listesi

Her tasarım elementi için kontrol et:

- [ ] Tüm spacing değerleri 8'in katları mı?
- [ ] Font boyutları type scale'e uygun mu?
- [ ] Line-height oranları doğru mu?
- [ ] Color contrast ratios WCAG standartlarına uygun mu?
- [ ] Touch target'lar minimum 48x48px mi?
- [ ] Border radius tutarlı bir sistem kullanıyor mu?
- [ ] Z-index değerleri sistematik mi?
- [ ] Animation duration'ları tutarlı mı?
- [ ] Responsive breakpoint'lerde oranlar korunuyor mu?
- [ ] White space hierarchy mantıklı mı?

---

# 14. Yapay Zekaya Özel Prompt Örneği

### Basit Versiyon

```
"Lütfen aşağıdaki kurallara KESİNLİKLE uyarak tasarım yap:

SPACING: Sadece 8px multiplier kullan (8, 16, 24, 32, 48, 64, 96)
TYPOGRAPHY: 16px base, 1.250 scale ratio (16, 20, 24, 32, 40, 48, 64)
LINE-HEIGHT: Başlıklar 1.2, body text 1.5
GRID: 12-column, 24px gutter, 1200px max-width
BORDER-RADIUS: 8px standard, 16px özel componentler
SHADOWS: Tailwind shadow scale kullan
COLORS: WCAG AAA contrast (7:1 minimum)
BUTTONS: 40px height, 12px/24px padding, 4px radius
RESPONSIVE: 640px, 1024px, 1440px breakpoints
ANIMATIONS: 200ms default, ease-out easing

Her bir değer bu sisteme uymalı, rastgele sayı kullanma."
```

---

# 15. Chain-of-Thought Prompt (Adım Adım Düşünme)

Bu prompt yapay zekayı her adımda düşünerek, kontrol ederek ilerlemesini sağlar:

```
"Tasarımı yaparken her aşamada aşağıdaki soruları kendine sor ve cevapla:

## 📐 LAYOUT AŞAMASI
1. "Container genişliğim ne olmalı?"
   → Mobil için 100% (16px padding)
   → Desktop için 1200px max-width mi kullanıyorum?

2. "Grid sistemim düzgün mü?"
   → 12 column kullanıyor muyum?
   → Gutter 24px mi?
   → Her element grid'e oturuyor mu?

3. "Section'lar arası boşluklar tutarlı mı?"
   → 64px veya 96px kullandım mı?
   → Rastgele 50px, 70px gibi değerler var mı? (OLMAMALI!)

## 🔤 TYPOGRAPHY AŞAMASI
4. "Font boyutlarım scale'e uygun mu?"
   → H1: 48px ✓
   → H2: 32px ✓
   → H3: 24px ✓
   → Body: 16px ✓
   → 17px, 19px, 28px gibi değerler var mı? (OLMAMALI!)

5. "Line-height oranlarım doğru mu?"
   → Başlıklarda 1.2 kullandım mı?
   → Body text'te 1.5 kullandım mı?

6. "Font weight hierarchy mantıklı mı?"
   → H1 en bold (700-800)?
   → Body normal (400)?
   → Subtle emphasis için 500-600 kullandım mı?

## 🎨 RENK VE KONTRAST AŞAMASI
7. "Kontrast oranları yeterli mi?"
   → Ana metinler 7:1 oranında mı?
   → Küçük metinler bile 4.5:1'in üzerinde mi?
   → Contrast checker ile kontrol ettim mi?

8. "Renk sistemi tutarlı mı?"
   → Primary, secondary, neutral tanımlı mı?
   → Her rengin 10 shade'i var mı?
   → Rastgele hex kodlar mı yoksa sistematik palet mi kullandım?

## 📦 COMPONENT AŞAMASI
9. "Button ölçüleri standart mı?"
   → Height: 40px (medium) kullandım mı?
   → Padding: 12px/24px (vertical/horizontal)?
   → Border-radius: 4px veya 8px?
   → 38px height veya 11px padding gibi değerler YOK DEĞİL Mİ?

10. "Card'ların padding'i tutarlı mı?"
    → 24px veya 32px kullandım mı?
    → Her card aynı padding sistemini kullanıyor mu?

11. "Icon boyutları standart mı?"
    → 16px, 20px, 24px seçeneklerinden biri mi?
    → Text ile inline olan iconlar 16px mı?

## ⚡ SPACING AŞAMASI (EN ÖNEMLİ!)
12. "TÜM spacing değerlerimi kontrol ediyorum:"
    → Margin-top: 8'in katı mı? (örn: 24px ✓, 25px ✗)
    → Margin-bottom: 8'in katı mı?
    → Padding: 8'in katı mı?
    → Gap (flexbox/grid): 8'in katı mı?

13. "Element arası boşluklar hiyerarşik mi?"
    → İlgili elementler: 8-16px
    → Component içi gruplar: 24-32px
    → Component'ler arası: 32-48px
    → Section'lar arası: 64-96px

## 📱 RESPONSIVE AŞAMASI
14. "Breakpoint'lerim standart mı?"
    → 640px (mobile-tablet)
    → 1024px (tablet-desktop)
    → 1440px (desktop-wide)
    → 900px gibi custom değerler YOK DEĞİL Mİ?

15. "Mobilde oranlar korunuyor mu?"
    → Font boyutları responsive scaling ile küçülüyor mu?
    → Padding'ler mobilde 16px'e düşüyor mu?
    → Grid columns mobile'da 4'e düşüyor mu?

## 🎭 GÖRSEL DETAYLAR
16. "Border-radius tutarlı mı?"
    → 4px, 8px, 16px seçeneklerinden biri mi?
    → 7px, 12px gibi custom değerler YOK DEĞİL Mİ?

17. "Shadow sistemi tutarlı mı?"
    → Tailwind shadow scale kullandım mı?
    → Custom shadow değerleri var mı? (olmamalı!)

18. "Z-index değerleri sistematik mi?"
    → 10, 20, 30, 40... şeklinde artıyor mu?
    → 15, 25 gibi değerler YOK DEĞİL Mİ?

## ✅ FİNAL KONTROL
19. "Genel tutarlılık kontrolü:"
    → Aynı component tekrar ettiğinde TAMAMEN aynı değerleri kullanıyor muyum?
    → İki button yan yana olsa aynı height/padding'e sahipler mi?
    → Tüm card'lar aynı border-radius kullanıyor mu?

20. "Matematiksel tutarlılık:"
    → Tüm sayılarım 8'in katı mı?
    → Font scale'im tutarlı mı?
    → Hiçbir yerde "yaklaşık" bir değer kullanmadım değil mi?

## 🔴 YAPMA LİSTESİ
❌ 15px, 18px, 22px, 35px gibi değerler KULLANMA
❌ "Yaklaşık 30px olsun" DEĞİL, tam 32px olmalı
❌ Her component için farklı padding KULLANMA
❌ Rastgele margin değerleri KULLANMA
❌ Custom breakpoint'ler EKLEME (640, 1024, 1440 yeterli)

## ✅ MUTLAKA YAP LİSTESİ
✅ Her değeri belirlemeden önce "Bu 8'in katı mı?" diye SOR
✅ Her font boyutunu belirlemeden önce scale'e BAK
✅ Her spacing'i belirlemeden önce sistem tablosuna BAK
✅ Aynı component tekrar edince değerleri KOPYALA (değiştirme!)
✅ Bitirince tüm değerleri TEK TEK kontrol ET

Her komponenti oluşturduktan sonra bu soruları cevapla ve cevaplarını göster.
Eğer bir değer sisteme uymuyorsa, DURDUR ve düzelt."
```

---

## 🎯 Örnek Düşünme Süreci Çıktısı

Yapay zeka böyle düşünmeli:

```
🤔 Button Component Tasarlıyorum...

Soru 1: Height ne olmalı?
→ Kontrol: Medium size için 40px (✓ 8'in katı)

Soru 2: Padding ne olmalı?
→ Kontrol: Vertical 12px, Horizontal 24px (✓ her ikisi de 8'in katı)

Soru 3: Border-radius ne olmalı?
→ Kontrol: Button için 4px standart (✓ sistem tablosunda var)

Soru 4: Font size ne olmalı?
→ Kontrol: 16px base size (✓ typography scale'de)

Soru 5: Margin-bottom ne olmalı?
→ Kontrol: Diğer elementlerle 24px boşluk (✓ 8'in katı)

✅ TÜM DEĞERLER SİSTEME UYGUN
```

---

# 16. Dinamik Karar Alma - Bağlamsal Esneklik

**ÖNEMLİ**: Bu sistem bir ROBOT DEĞİL, akıllı bir tasarımcı gibi düşünmeli!

## 16.1 Esnek Düşünme Prensibi

```
"Tasarım kurallarına UYARKEN, her kararı projenin bağlamında değerlendir:

🎯 HER KARAR İÇİN ŞU SORULARI SOR:

1. 'Bu proje ne tür bir proje?'
   → E-ticaret mi? (Daha compact spacing)
   → Kurumsal site mi? (Daha spacious, professional)
   → Portfolio mu? (Daha bold, creative)
   → SaaS dashboard mu? (Daha functional, dense)
   → Blog mu? (Daha readable, relaxed)

2. 'Bu componentin amacı ne?'
   → CTA button → Daha büyük padding (16px/32px), bold
   → Secondary button → Standart padding (12px/24px)
   → Text button → Minimal padding (8px/16px)

3. 'Kullanıcı buraya ne için bakıyor?'
   → Hızlı scan etmek için mi? → Daha fazla whitespace
   → Detaylı okumak için mi? → Daha rahat line-height
   → Hızlı aksiyon almak için mi? → Daha vurgulu CTA

4. 'Bu alan visual hierarchy'de nerede?'
   → Hero section → Daha spacious (96px-128px padding)
   → Content section → Normal (64px padding)
   → Footer → Daha compact (48px padding)

5. 'Target audience kimler?'
   → Yaşlı kullanıcılar → Daha büyük font (18px base)
   → Genç, tech-savvy → Normal (16px base)
   → Profesyoneller → Daha compact, efficient

## 🔀 ESNEK KARAR ÖRNEKLERİ

### Örnek 1: Hero Section Padding
❌ ROBOT: "Her zaman 96px padding kullan"
✅ AKILLI:
- Lüks marka site → 128px padding (daha spacious, premium feel)
- Startup landing page → 96px padding (balanced)
- SaaS dashboard → 64px padding (daha functional, less marketing)
📝 Sebep: Markanın tonu padding miktarını etkiler

### Örnek 2: Card Spacing
❌ ROBOT: "Her zaman 24px padding kullan"
✅ AKILLI:
- Ürün kartları (e-ticaret) → 16px padding (daha çok ürün görünsün)
- Blog post kartları → 24px padding (rahat okuma)
- Feature cards (marketing) → 32px padding (her kart öne çıksın)
📝 Sebep: İçerik tipi spacing'i belirler

### Örnek 3: Font Size
❌ ROBOT: "Body text her zaman 16px"
✅ AKILLI:
- Uzun blog yazıları → 18px (gözü yormamak için)
- Dashboard tables → 14px (daha çok data sığsın)
- Marketing copy → 16px (standart)
- Legal text → 12px (fazla yer kaplamamalı ama okunabilir)
📝 Sebep: İçerik uzunluğu ve amacı font size'ı etkiler

### Örnek 4: Button Size
❌ ROBOT: "Her button 40px height"
✅ AKILLI:
- Primary CTA (Hero) → 56px height (çok önemli, vurgulanmalı)
- Form submit button → 48px height (önemli ama primary kadar değil)
- In-content button → 40px height (standart)
- Table action button → 32px height (compact, functional)
📝 Sebep: Button'ın önemi ve konumu size'ı belirler

### Örnek 5: Section Spacing
❌ ROBOT: "Section'lar arası her zaman 64px"
✅ AKILLI:
- Hero → Next section: 96px (güçlü ayırım)
- Related content sections: 48px (birbirine yakın hissettir)
- Footer'dan önce: 128px (net ayrım)
📝 Sebep: Section'ların ilişkisi spacing'i etkiler

## 🎨 BAĞLAMSAL KARAR AĞACI

```
Kararı Verirken:
│
├─ 1️⃣ Sisteme bak → Hangi değerler uygun? (8, 16, 24, 32...)
│ │
│ ├─ 2️⃣ Projeyi değerlendir → Ne tür bir site?
│ │ │
│ │ ├─ 3️⃣ Hedef kitleyi düşün → Kim kullanacak?
│ │ │ │
│ │ │ ├─ 4️⃣ Component'in rolünü sor → Ne kadar önemli?
│ │ │ │ │
│ │ │ │ └─ 5️⃣ Karar ver → Sisteme UYGUN ama BAĞLAMSAL
│ │ │ │
│ │ │ └─ Kararını AÇIKLA → "Neden bu değeri seçtim?"

```

## 📊 GERÇEK DÜNYA ÖRNEKLERİ

### E-Ticaret Sitesi
```
Durum: Ürün grid'i tasarlıyorum
Robot Yaklaşım: "Her ürün kartı 24px padding"
Akıllı Yaklaşım:
→ Analiz: Kullanıcı çok ürün görmek istiyor
→ Karar: 16px padding (daha compact)
→ Ama: Mobilde 24px (dokunma hedefleri büyük olmalı)
→ Sebep: Desktop'ta efficiency, mobile'da usability öncelikli
```

### Blog Sitesi
```
Durum: Makale content area tasarlıyorum
Robot Yaklaşım: "16px font size, 1.5 line-height"
Akıllı Yaklaşım:
→ Analiz: Uzun okuma süresi, göz yorulmamalı
→ Karar: 18px font size, 1.6 line-height
→ Ama: Max-width 680px (70 karakter satır uzunluğu)
→ Sebep: Okuma konforu ve retention optimizasyonu
```

### SaaS Dashboard
```
Durum: Data table tasarlıyorum
Robot Yaklaşım: "Her zaman 64px section padding"
Akıllı Yaklaşım:
→ Analiz: Kullanıcı çok data görmek istiyor, scroll azaltmalı
→ Karar: 32px section padding, 12px row spacing
→ Ama: Filtreleme alanı 48px padding (daha prominent)
→ Sebep: Functional tool, marketing site değil
```

## 🔑 ANA PRENSİPLER

### 1. Sistem Kuralları = TEMEL
✅ 8'in katları KULLAN
✅ Typography scale'i TAKİP ET
✅ Contrast ratios'a DİKKAT ET

### 2. Bağlam = KARAR VERİCİ
🤔 "Bu değer bu proje için mantıklı mı?"
🤔 "Kullanıcı deneyimini nasıl etkiler?"
🤔 "Markanın tonuna uygun mu?"

### 3. Açıklama = ŞART
📝 Her kararın NEDENINI yaz
📝 "Sisteme uygun ama X nedeniyle Y'yi seçtim"
📝 Eğer standarttan sapıyorsan, NEDEN sapmak gerekti?

## ⚖️ ESNEKLIK vs. TUTARLILIK DENGESI

```
TUTARLILIK (Her zaman)
├─ Matematiksel sistem (8'in katları)
├─ Contrast ratios (WCAG)
├─ Responsive breakpoints
└─ Aynı component = aynı değerler

ESNEKLIK (Bağlamsal)
├─ Padding miktarı (proje tipine göre)
├─ Font size (içerik tipine göre)
├─ Spacing density (kullanıcı hedefine göre)
└─ Visual weight (importance'a göre)
```

## 💬 AKILLI PROMPT EKLEME

```
"Sisteme uyarken akıllı kararlar al:

1. Her karar için ÖNCE sistem değerlerine bak (8, 16, 24...)
2. SONRA projenin bağlamını değerlendir
3. Sisteme UYGUN ama bağlamsal olarak EN UYGUN değeri seç
4. Kararını AÇIKLA:

Örnek:
'Hero section padding için 128px seçtim (sistem: ✓ 8'in katı)
Sebep: Lüks marka, premium feel verilmeli, spacious olmalı.
Alternatif 96px olabilirdi ama bu proje için yeterince premium hissettirmez.
Alternatif 160px çok fazla olur, scroll artırır.'

5. Eğer standarttan SAPTIYSAN (örn: 40px yerine 48px button):
   → Açıkla: 'Bu bir primary CTA, daha vurgulu olmalı'
   → Kanıtla: 'Heatmap data'ya göre daha büyük CTA'lar conversion artırır'
   → Doğrula: '48px hala sisteme uygun (8 x 6)'

SİSTEME UYMAYAN HİÇBİR DEĞER KULLANMA!
Ama sistemin SUNDUĞU SEÇENEKLERİ akıllıca KULLAN."
```

---

# 21. Self-Correction Prompt

```
"Tasarımı tamamladıktan sonra:

1. Tüm pixel değerlerini listele
2. Her birini 8'e böl
3. Tam bölünmüyorsa, yakın 8'in katına YUVARLAMA (yukarı veya aşağı)
4. Typography değerlerini scale ile karşılaştır
5. Uymayanları DÜZELT ve 'Düzeltme yapıldı' diye BELIRT

Örnek:
❌ Buldum: margin-top: 30px
✅ Düzelttim: margin-top: 32px (8 x 4)
📝 Sebep: 30px sisteme uymuyor, en yakın 8'in katı 32px"
```

---

# 22. Referanslar ve Kaynaklar

- **Material Design 3**: Google'ın 2025 design system'i
- **Tailwind CSS**: Utility-first spacing ve typography
- **Radix UI**: Accessible component primitives
- **shadcn/ui**: Modern component system
- **WCAG 2.1 Level AAA**: Erişilebilirlik standartları
- **8-Point Grid System**: IBM Design Language
- **Type Scale**: modularscale.com / type-scale.com
- **Contrast Checker**: WebAIM contrast checker

---

**Son Güncelleme**: Aralık 2025
**Versiyon**: 1.1

### Changelog v1.1
- Typography scale ismi düzeltildi (Major Third → Practical Scale)
- 768px breakpoint eklendi (iPad portrait desteği)
- Border radius sistemi sadeleştirildi (12px notu eklendi)
- Tablet container width düzeltildi (720px → 768px)
- 12px padding açıklaması eklendi
- Focus Visible modern yaklaşımı eklendi
- Modern CSS Features 2025 bölümü eklendi (Container Queries, System Preferences, Logical Properties)
- Fluid Typography ve Fluid Spacing formülleri güncellendi
- Tailwind CSS breakpoint mapping eklendi

Bu rehbere uygun tasarımlar, hem görsel olarak mükemmel hem de teknik olarak standartlara uygun olacaktır.
