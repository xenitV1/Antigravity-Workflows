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

# Web Design Proportions and Consistency Guide

## 🎯 General Principle

Every design element must be mathematically consistent within a system. Random values should not be used; every measurement must be a conscious choice.

---

## 📏 Spacing System (8-Point Grid)

### Base Rule

All spacing must be multiples of 8. This is the gold standard of modern UI/UX.

```
4px   - Minimum spacing (micro interactions)
8px   - XS - Very small spacing
16px  - SM - Small spacing (between icon-text)
24px  - MD - Medium spacing (elements inside cards)
32px  - LG - Large spacing (between components)
48px  - XL - Groups inside sections
64px  - 2XL - Between sections
96px  - 3XL - Between major sections
128px - 4XL - Hero section padding
```

### Padding Structure

- **Internal padding for Card/Container**: 24px or 32px
- **Button padding**: Vertical 12px, Horizontal 24px
- **Input field padding**: Vertical 12px, Horizontal 16px
- **Section padding**: 64px - 96px (Desktop), 32px - 48px (Mobile)

> **Note on 12px**: 12px is not strictly a multiple of 8 (1.5× base unit) but is accepted as an industry standard for compact touch-friendly designs. Alternative: 8px (tighter) or 16px (more spacious).

---

## 📐 Layout & Grid System

### Container System

```
Mobile:     100% width, 16px side padding
Tablet:     768px max-width, 24px side padding  (8 × 96 = 768)
Desktop:    1200px max-width, 32px side padding
Wide:       1440px max-width, 48px side padding
```

> All max-width values are multiples of 8: 768, 1200, 1440

### Grid Columns

- **Desktop**: 12 column grid, 24px gutter
- **Tablet**: 8 column grid, 16px gutter
- **Mobile**: 4 column grid, 16px gutter

### Aspect Ratios

Standard ratios for images and media:

- **Hero images**: 16:9 or 21:9
- **Card images**: 4:3 or 1:1
- **Portrait**: 3:4
- **Avatar**: 1:1 (perfect square)
- **Video embed**: 16:9

---

## 🔤 Typography Scale (Type Scale)

### Modern Font Sizing (Practical Scale - Tailwind Based)

> Note: This scale is not the mathematical Major Third (1.250) but a Tailwind-style scale optimized for practical use.

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

### Line Height Ratios

- **Headings (H1-H3)**: 1.2 - 1.3
- **Body text**: 1.5 - 1.6
- **Small text**: 1.4
- **Hero text**: 1.1

### Font Weight Hierarchy

```
400 - Regular (Body text)
500 - Medium (Subtle emphasis)
600 - Semibold (Subheadings, buttons)
700 - Bold (Headings)
800 - Extra bold (Hero sections)
```

### Letter Spacing (Tracking)

- **Large headings (48px+)**: -0.02em (tighter)
- **Small caps / Uppercase**: 0.05em - 0.1em (looser)
- **Button text**: 0.02em

---

## 🎨 Color System

### Contrast Ratios (WCAG 2.1)

- **Normal text**: Minimum 4.5:1
- **Large text (18px+)**: Minimum 3:1
- **AAA standard**: 7:1 (ideal)

### Color Palette Structure

```
Primary: 10 shades (50, 100, 200...900, 950)
Neutral/Gray: 10 shades
Success, Warning, Error, Info: 5 shades each
```

---

## 🔲 Component Sizing

### Button Sizes

```
Small:   Height 32px, Padding 8px 16px, Font 14px
Medium:  Height 40px, Padding 12px 24px, Font 16px (Default)
Large:   Height 48px, Padding 14px 32px, Font 18px
```

### Border Radius System

```
2px    - Subtle (inputs)
4px    - Small (buttons, badges)
8px    - Medium (cards, modals) ← Default
16px   - Large (feature cards, hero sections)
9999px - Full rounded (pills, avatars)
```

---

## 📱 Responsive Breakpoints

```
Mobile:       0px - 639px
Tablet:       768px - 1023px
Desktop:      1024px - 1439px
Wide Desktop: 1440px+
```

---

## ⚡ Visual Hierarchy

### Z-Index Scale

```
-1    - Behind content
0     - Base layer
10    - Dropdown menus
20    - Sticky headers
30    - Modals backdrop
40    - Modal content
50    - Tooltips
100   - Toast notifications
```

### Shadow System (Elevation)

```
shadow-sm:   0 1px 3px rgba(0,0,0,0.1)
shadow-md:   0 4px 6px rgba(0,0,0,0.1)
shadow-lg:   0 10px 15px rgba(0,0,0,0.1)
```

---

## 🎭 Animation & Transitions

### Duration Scale

```
150ms  - Fast (hover states)
200ms  - Normal (default transition)
300ms  - Moderate (dropdown, modal)
500ms  - Slow (page transitions)
```

---

## 🧩 CONTEXTUAL DECISION MAKING - Smart Flexibility

### Smart Thinking Principle

"While following design rules, evaluate every decision within the project's context."

1. **What kind of project is this?** (E-commerce? Portfolio? SaaS?)
2. **What is the purpose of this component?**
3. **What is the user looking for?**
4. **Where is this in the visual hierarchy?**
5. **Who is the target audience?**

### Smart Examples

- **E-commerce**: Compact spacing to show more products.
- **Blog**: 18px font and relaxed line-height for readability.
- **SaaS**: High density (compact padding) for data management tools.
- **Hero Section**: Spacious (96px-128px padding) for premium branding.

---

## ✅ Checklist

- [ ] Are all spacing values multiples of 8?
- [ ] Are font sizes aligned with the type scale?
- [ ] Are color contrast ratios WCAG compliant?
- [ ] Are touch targets at least 48x48px?
- [ ] Is the visual hierarchy clear and consistent?

---

**Last Update**: December 2025
**Version**: 1.1
