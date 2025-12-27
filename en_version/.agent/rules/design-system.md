# Design System Rule - UI Consistency

## Activation
- **Mode:** Glob
- **Glob Pattern:** `*.css, *.scss, *.styled.*, components/**, ui/**`
- **Description:** Web design system guidelines including 8-point grid, typography, colors, and component sizing. Auto-activates for style and UI component files.

---

## Core Principle

Every design element must be mathematically consistent. No random values - every measurement is a deliberate choice.

---

## Spacing System (8-Point Grid)

All spacing must be multiples of 8:

```
4px   - Minimum (micro interactions)
8px   - XS - Very small spacing
16px  - SM - Small (icon-text gap)
24px  - MD - Medium (card inner elements)
32px  - LG - Large (between components)
48px  - XL - Section inner groups
64px  - 2XL - Between sections
96px  - 3XL - Major sections
128px - 4XL - Hero section padding
```

### Padding Structure
- Card/Container: 24px or 32px
- Button: 12px vertical, 24px horizontal
- Input: 12px vertical, 16px horizontal
- Section: 64px-96px (Desktop), 32px-48px (Mobile)

---

## Typography Scale

```
12px  - Caption / Helper text
14px  - Small text / Metadata
16px  - Body text (Base)
18px  - Large body (reading)
20px  - Lead paragraph
24px  - H4 / Small heading
32px  - H3 / Medium heading
40px  - H2 / Large heading
48px  - H1 / Display heading
64px  - Hero heading
```

### Line Height
- Headings (H1-H3): 1.2 - 1.3
- Body text: 1.5 - 1.6
- Small text: 1.4
- Hero text: 1.1

### Font Weight
- 400: Regular (Body)
- 500: Medium (Subtle emphasis)
- 600: Semibold (Subheadings, buttons)
- 700: Bold (Headings)

---

## Color System

### Contrast Ratios (WCAG 2.1)
- Normal text: 4.5:1 minimum
- Large text (18px+): 3:1 minimum
- UI components: 3:1 minimum
- AAA standard: 7:1 (ideal)

### Palette Structure
```
Primary: 10 shades (50-950)
Secondary: 10 shades
Neutral/Gray: 10 shades
Semantic: Success, Warning, Error, Info
```

---

## Component Sizing

### Buttons
```
Small:   Height 32px, Padding 8px 16px, Font 14px
Medium:  Height 40px, Padding 12px 24px, Font 16px
Large:   Height 48px, Padding 14px 32px, Font 18px
XLarge:  Height 56px, Padding 16px 40px, Font 20px
```

### Border Radius
```
0px    - None (sharp)
4px    - Small (buttons, badges)
8px    - Medium (cards, modals) <- Default
16px   - Large (feature cards)
9999px - Full (pills, avatars)
```

### Icons
```
16px - Small (inline)
20px - Medium (buttons)
24px - Large (standalone)
32px - XL (highlights)
48px - 2XL (hero)
```

---

## Responsive Breakpoints

```
Mobile:       0px - 639px
Tablet SM:    640px - 767px
Tablet:       768px - 1023px
Desktop:      1024px - 1439px
Wide:         1440px+
```

### Container Widths
- Mobile: 100% width, 16px side padding
- Tablet: 768px max-width, 24px side padding
- Desktop: 1200px max-width, 32px side padding
- Wide: 1440px max-width, 48px side padding

---

## Visual Hierarchy

### Z-Index Scale
```
-1   - Behind
0    - Base
10   - Dropdown
20   - Sticky header
30   - Modal backdrop
40   - Modal content
50   - Tooltips
100  - Toast notifications
```

### Shadow System
```
shadow-sm:  0 1px 3px rgba(0,0,0,0.1)
shadow-md:  0 4px 6px rgba(0,0,0,0.1)
shadow-lg:  0 10px 15px rgba(0,0,0,0.1)
shadow-xl:  0 20px 25px rgba(0,0,0,0.1)
```

---

## Animation & Transitions

### Duration
```
75ms   - Instant
150ms  - Fast (hover)
200ms  - Normal (default)
300ms  - Moderate (dropdown)
500ms  - Slow (page)
```

### Easing
- ease-out: Most common (UI elements)
- ease-in-out: Smooth transitions
- ease-in: Exit animations

---

## Accessibility

### Touch Targets
- Minimum: 44x44px (Apple) / 48x48px (Google)
- Spacing between: 8px minimum

### Focus States
- Ring width: 2px - 4px
- Ring offset: 2px
- Use `:focus-visible` for keyboard only

---

## Checklist

- [ ] All spacing values are multiples of 8?
- [ ] Font sizes follow type scale?
- [ ] Line-height ratios correct?
- [ ] Color contrast WCAG compliant?
- [ ] Touch targets minimum 48x48px?
- [ ] Border radius consistent?
- [ ] Z-index systematic?
- [ ] Animation durations consistent?
- [ ] Responsive ratios maintained?

---

## Don't List

- Random values (15px, 18px, 22px, 35px)
- "Approximately" values
- Different padding per component
- Custom breakpoints (640, 1024, 1440 is enough)
- Inconsistent border-radius

---

**Version:** 2.0 (Antigravity Rule)
