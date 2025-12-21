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

# 📋 Contents

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
13. [Checklist](#13-checklist)
14. [AI Specific Prompt Example](#14-ai-specific-prompt-example)
15. [Chain-of-Thought Prompt](#15-chain-of-thought-prompt)
16. [Dynamic Decision Making - Contextual Flexibility](#16-dynamic-decision-making---contextual-flexibility)
17. [Real World Examples](#17-real-world-examples)
18. [Core Principles](#18-core-principles)
19. [Flexibility vs Consistency Balance](#19-flexibility-vs-consistency-balance)
20. [Smart Prompt Injection](#20-smart-prompt-injection)
21. [Self-Correction Prompt](#21-self-correction-prompt)
22. [References and Resources](#22-references-and-resources)

---

# 1. Spacing System (8-Point Grid)

## 1.1 Base Rule

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

## 1.2 Padding Structure

- **Internal padding for Card/Container**: 24px or 32px
- **Button padding**: Vertical 12px, Horizontal 24px
- **Input field padding**: Vertical 12px, Horizontal 16px
- **Section padding**: 64px - 96px (Desktop), 32px - 48px (Mobile)

> **Note on 12px**: 12px is not strictly a multiple of 8 (1.5× base unit) but is accepted as an industry standard for compact touch-friendly designs. Alternative: 8px (tighter) or 16px (more spacious).

---

# 2. Layout & Grid System

## 2.1 Container System

```
Mobile:     100% width, 16px side padding
Tablet:     768px max-width, 24px side padding  (8 × 96 = 768)
Desktop:    1200px max-width, 32px side padding
Wide:       1440px max-width, 48px side padding
```

> All max-width values are multiples of 8: 768, 1200, 1440

## 2.2 Grid Columns

- **Desktop**: 12 column grid, 24px gutter
- **Tablet**: 8 column grid, 16px gutter
- **Mobile**: 4 column grid, 16px gutter

## 2.3 Aspect Ratios

Standard ratios for images and media:

- **Hero images**: 16:9 or 21:9
- **Card images**: 4:3 or 1:1
- **Portrait**: 3:4
- **Avatar**: 1:1 (perfect square)
- **Video embed**: 16:9

---

# 3. Typography Scale (Type Scale)

## 3.1 Modern Font Sizing (Practical Scale - Tailwind Based)

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

## 3.2 Line Height Ratios

- **Headings (H1-H3)**: 1.2 - 1.3
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

- **Large headings (48px+)**: -0.02em (tighter)
- **Normal headings**: 0
- **Body text**: 0
- **Small caps / Uppercase**: 0.05em - 0.1em (looser)
- **Button text**: 0.02em

---

# 4. Color System

## 4.1 Contrast Ratios (WCAG 2.1)

- **Normal text**: Minimum 4.5:1
- **Large text (18px+)**: Minimum 3:1
- **UI components**: Minimum 3:1
- **AAA standard**: 7:1 (ideal)

## 4.2 Color Palette Structure

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
100% - Fully opaque (default)
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

> Note: While 12px is commonly used, it doesn't fit the 8-point grid perfectly. Prefer 8px or 16px for consistency.

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
Tablet:       768px - 1023px  (Critical for iPad portrait)
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

/* With CSS Custom Properties */
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

/* Usage */
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
/* Show focus for keyboard navigation */
:focus-visible {
  outline: 2px solid var(--primary-500);
  outline-offset: 2px;
}

/* Hide focus for mouse click */
:focus:not(:focus-visible) {
  outline: none;
}

/* Thicker offset for dark background */
.dark :focus-visible {
  outline-offset: 4px;
}
```

> **Best Practice**: Use `:focus-visible` to show the focus ring only during keyboard navigation. This provides a cleaner experience for mouse users.

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
ease-in:      Slow start (cubic-bezier(0.4, 0, 1, 1))
ease-out:     Slow end (cubic-bezier(0, 0, 0.2, 1)) - Most commonly used
ease-in-out:  Both (cubic-bezier(0.4, 0, 0.2, 1))
ease-bounce:  For spring effect
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

Use container queries instead of viewport media queries for component-based responsive design:

```css
/* Define container */
.card-container {
  container-type: inline-size;
  container-name: card;
}

/* Style according to container width */
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

Adapt to user system preferences:

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

Use logical properties instead of physical ones for LTR/RTL support:

```css
/* Old way (LTR only) */
.old-way {
  margin-left: 16px;
  padding-right: 24px;
  border-left: 2px solid;
}

/* New way (LTR & RTL) */
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
- **Optimal size**: 48x48px or larger
- **Spacing between**: Minimum 8px

## 12.2 Focus Indicators

- **Visibility**: Must always be visible
- **Contrast**: 3:1 minimum (with background)
- **Thickness**: Minimum 2px

---

# 13. Checklist

Check for every design element:

- [ ] Are all spacing values multiples of 8?
- [ ] Are font sizes aligned with the type scale?
- [ ] Are line-height ratios correct?
- [ ] Are color contrast ratios WCAG compliant?
- [ ] Are touch targets at least 48x48px?
- [ ] Does border radius use a consistent system?
- [ ] Are z-index values systematic?
- [ ] Are animation durations consistent?
- [ ] Are ratios preserved in responsive breakpoints?
- [ ] Is white space hierarchy logical?

---

# 14. AI Specific Prompt Example

### Simple Version

```
"Please design strictly adhering to the following rules:

SPACING: Use only 8px multipliers (8, 16, 24, 32, 48, 64, 96)
TYPOGRAPHY: 16px base, 1.250 scale ratio (16, 20, 24, 32, 40, 48, 64)
LINE-HEIGHT: Headings 1.2, body text 1.5
GRID: 12-column, 24px gutter, 1200px max-width
BORDER-RADIUS: 8px standard, 16px special components
SHADOWS: Use Tailwind shadow scale
COLORS: WCAG AAA contrast (7:1 minimum)
BUTTONS: 40px height, 12px/24px padding, 4px radius
RESPONSIVE: 640px, 1024px, 1440px breakpoints
ANIMATIONS: 200ms default, ease-out easing

Every single value must fit this system, do not use random numbers."
```

---

# 15. Chain-of-Thought Prompt

This prompt ensures the AI thinks and checks at every step:

```
"While designing, ask yourself and answer the following questions at each stage:

## 📐 LAYOUT PHASE
1. 'What should be my Container width?'
   → 100% for Mobile (16px padding)
   → Am I using 1200px max-width for Desktop?

2. 'Is my Grid system correct?'
   → Am I using 12 columns?
   → Is the Gutter 24px?
   → Does every element fit the grid?

3. 'Are spacing between sections consistent?'
   → Did I use 64px or 96px?
   → Are there random values like 50px, 70px? (MUST NOT BE!)

## 🔤 TYPOGRAPHY PHASE
4. 'Do my font sizes fit the scale?'
   → H1: 48px ✓
   → H2: 32px ✓
   → H3: 24px ✓
   → Body: 16px ✓
   → Are there values like 17px, 19px, 28px? (MUST NOT BE!)

5. 'Are my line-height ratios correct?'
   → Did I use 1.2 for headings?
   → Did I use 1.5 for body text?

6. 'Is the font weight hierarchy logical?'
   → H1 boldest (700-800)?
   → Body normal (400)?
   → Did I use 500-600 for subtle emphasis?

## 🎨 COLOR AND CONTRAST PHASE
7. 'Are contrast ratios sufficient?'
   → Are main texts 7:1?
   → Are even small texts above 4.5:1?
   → Did I check with a contrast checker?

8. 'Is the color system consistent?'
   → Are primary, secondary, neutral defined?
   → Does each color have 10 shades?
   → Did I use a systematic palette or random hex codes?

## 📦 COMPONENT PHASE
9. 'Are button sizes standard?'
   → Did I use Height: 40px (medium)?
   → Padding: 12px/24px (vertical/horizontal)?
   → Border-radius: 4px or 8px?
   → Are there values like 38px height or 11px padding? (MUST NOT BE!)

10. 'Is card padding consistent?'
    → Did I use 24px or 32px?
    → Does every card use the same padding system?

11. 'Are icon sizes standard?'
    → One of 16px, 20px, 24px options?
    → Are icons inline with text 16px?

## ⚡ SPACING PHASE (MOST IMPORTANT!)
12. 'Checking ALL my spacing values:'
    → Margin-top: Multiple of 8? (e.g., 24px ✓, 25px ✗)
    → Margin-bottom: Multiple of 8?
    → Padding: Multiple of 8?
    → Gap (flexbox/grid): Multiple of 8?

13. 'Is spacing between elements hierarchical?'
    → Related elements: 8-16px
    → Groups inside component: 24-32px
    → Between components: 32-48px
    → Between sections: 64-96px

## 📱 RESPONSIVE PHASE
14. 'Are my breakpoints standard?'
    → 640px (mobile-tablet)
    → 1024px (tablet-desktop)
    → 1440px (desktop-wide)
    → Are there custom values like 900px? (MUST NOT BE!)

15. 'Are ratios preserved in mobile?'
    → Do font sizes shrink with responsive scaling?
    → Does padding drop to 16px on mobile?
    → Do grid columns drop to 4 on mobile?

## 🎭 VISUAL DETAILS
16. 'Is border-radius consistent?'
    → One of 4px, 8px, 16px options?
    → Are there custom values like 7px, 12px? (MUST NOT BE!)

17. 'Is the shadow system consistent?'
    → Did I use Tailwind shadow scale?
    → Are there custom shadow values? (Should not be!)

18. 'Are z-index values systematic?'
    → Increasing like 10, 20, 30, 40...?
    → Are there values like 15, 25? (MUST NOT BE!)

## ✅ FINAL CHECK
19. 'General consistency check:'
    → When the same component repeats, am I using EXACTLY the same values?
    → Do two side-by-side buttons have the same height/padding?
    → do all cards use the same border-radius?

20. 'Mathematical consistency:'
    → Are all my numbers multiples of 8?
    → Is my font scale consistent?
    → I haven't used any 'approximate' values, right?

## 🔴 DO NOT DO LIST
❌ DO NOT USE values like 15px, 18px, 22px, 35px
❌ DO NOT say 'Let it be around 30px', it must be exactly 32px
❌ DO NOT use different padding for every component
❌ DO NOT use random margin values
❌ DO NOT add Custom breakpoints (640, 1024, 1440 are enough)

## ✅ MUST DO LIST
✅ BEFORE setting any value, ASK 'Is this a multiple of 8?'
✅ BEFORE setting any font size, LOOK at the scale
✅ BEFORE setting any spacing, LOOK at the system table
✅ COPY values when the same component repeats (don't change!)
✅ CHECK all values ONE BY ONE when finished

After creating each component, answer these questions and show your answers.
If a value does not fit the system, STOP and fix it."
```

---

## 🎯 Example Thought Process Output

The AI should think like this:

```
🤔 Designing Button Component...

Question 1: What shoud be the Height?
→ Check: 40px for Medium size (✓ Multiple of 8)

Question 2: What should be the Padding?
→ Check: Vertical 12px, Horizontal 24px (✓ Both are multiples of 8 - vertical exception accepted)

Question 3: What should be the Border-radius?
→ Check: 4px standard for Button (✓ in system table)

Question 4: What should be the Font size?
→ Check: 16px base size (✓ in typography scale)

Question 5: What should be the Margin-bottom?
→ Check: 24px spacing with other elements (✓ Multiple of 8)

✅ ALL VALUES COMPLIANT WITH SYSTEM
```

---

# 16. Dynamic Decision Making - Contextual Flexibility

**IMPORTANT**: This system is NOT A ROBOT, it should think like a smart designer!

## 16.1 Flexible Thinking Principle

```
"While FOLLOWING design rules, evaluate every decision within the context of the project:

🎯 ASK THESE QUESTIONS FOR EVERY DECISION:

1. 'What kind of project is this?'
   → E-commerce? (More compact spacing)
   → Corporate site? (More spacious, professional)
   → Portfolio? (More bold, creative)
   → SaaS dashboard? (More functional, dense)
   → Blog? (More readable, relaxed)

2. 'What is the purpose of this component?'
   → CTA button → Larger padding (16px/32px), bold
   → Secondary button → Standard padding (12px/24px)
   → Text button → Minimal padding (8px/16px)

3. 'What is the user looking here for?'
   → To scan quickly? → More whitespace
   → To read in detail? → More comfortable line-height
   → To take quick action? → More emphasized CTA

4. 'Where is this area in the visual hierarchy?'
   → Hero section → More spacious (96px-128px padding)
   → Content section → Normal (64px padding)
   → Footer → More compact (48px padding)

5. 'Who is the target audience?'
   → Elderly users → Larger font (18px base)
   → Young, tech-savvy → Normal (16px base)
   → Professionals → More compact, efficient

## 🔀 FLEXIBLE DECISION EXAMPLES

### Example 1: Hero Section Padding
❌ ROBOT: "Always use 96px padding"
✅ SMART:
- Luxury brand site → 128px padding (more spacious, premium feel)
- Startup landing page → 96px padding (balanced)
- SaaS dashboard → 64px padding (more functional, less marketing)
📝 Reason: Brand tone affects padding amount

### Example 2: Card Spacing
❌ ROBOT: "Always use 24px padding"
✅ SMART:
- Product cards (e-commerce) → 16px padding (show more products)
- Blog post cards → 24px padding (comfortable reading)
- Feature cards (marketing) → 32px padding (make every card stand out)
📝 Reason: Content type determines spacing

### Example 3: Font Size
❌ ROBOT: "Body text is always 16px"
✅ SMART:
- Long blog posts → 18px (to avoid eye strain)
- Dashboard tables → 14px (fit more data)
- Marketing copy → 16px (standard)
- Legal text → 12px (should not take too much space but readable)
📝 Reason: Content length and purpose affects font size

### Example 4: Button Size
❌ ROBOT: "Every button is 40px height"
✅ SMART:
- Primary CTA (Hero) → 56px height (very important, must be emphasized)
- Form submit button → 48px height (important but not as much as primary)
- In-content button → 40px height (standard)
- Table action button → 32px height (compact, functional)
📝 Reason: Button importance and location determines size

### Example 5: Section Spacing
❌ ROBOT: "Between sections is always 64px"
✅ SMART:
- Hero → Next section: 96px (strong separation)
- Related content sections: 48px (feel close to each other)
- Before Footer: 128px (clear separation)
📝 Reason: Relationship of sections affects spacing

## 🎨 CONTEXTUAL DECISION TREE

```
When Deciding:
│
├─ 1️⃣ Look at System → Which values are appropriate? (8, 16, 24, 32...)
│ │
│ ├─ 2️⃣ Evaluate Project → What kind of site?
│ │ │
│ │ ├─ 3️⃣ Consider Target Audience → Who will use it?
│ │ │ │
│ │ │ ├─ 4️⃣ Ask Component's Role → How important?
│ │ │ │ │
│ │ │ │ └─ 5️⃣ Decide → Appropriate to System but CONTEXTUAL
│ │ │ │
│ │ │ └─ EXPLAIN Decision → "Why did I choose this value?"

```

## 📊 REAL WORLD EXAMPLES

### E-Commerce Site
```
Situation: Designing product grid
Robot Approach: "Every product card 24px padding"
Smart Approach:
→ Analysis: User wants to see many products
→ Decision: 16px padding (more compact)
→ But: 24px on Mobile (touch targets must be large)
→ Reason: Efficiency on Desktop, usability on Mobile prioritized
```

### Blog Site
```
Situation: Designing article content area
Robot Approach: "16px font size, 1.5 line-height"
Smart Approach:
→ Analysis: Long reading time, eyes should not verify
→ Decision: 18px font size, 1.6 line-height
→ But: Max-width 680px (70 characters line length)
→ Reason: Reading comfort and retention optimization
```

### SaaS Dashboard
```
Situation: Designing data table
Robot Approach: "Always 64px section padding"
Smart Approach:
→ Analysis: User wants to see data, reduce scrolling
→ Decision: 32px section padding, 12px row spacing
→ But: Filtering area 48px padding (more prominent)
→ Reason: Functional tool, not marketing site
```

## 🔑 CORE PRINCIPLES

### 1. System Rules = BASE
✅ USE multiples of 8
✅ FOLLOW Typography scale
✅ PAY ATTENTION TO Contrast ratios

### 2. Context = DECISION MAKER
🤔 "Is this value logical for this project?"
🤔 "How does it affect user experience?"
🤔 "Is it suitable for the brand tone?"

### 3. Explanation = MANDATORY
📝 Write the REASON for every decision
📝 "Suitable for system but I chose Y because of X"
📝 If deviating from standard, WHY was it necessary?

## ⚖️ FLEXIBILITY vs. CONSISTENCY BALANCE

```
CONSISTENCY (Always)
├─ Mathematical system (multiples of 8)
├─ Contrast ratios (WCAG)
├─ Responsive breakpoints
└─ Same component = same values

FLEXIBILITY (Contextual)
├─ Padding amount (based on project type)
├─ Font size (based on content type)
├─ Spacing density (based on user goal)
└─ Visual weight (based on importance)
```

## 💬 SMART PROMPT INJECTION

```
"Take smart decisions while adhering to the system:

1. Look at system values FIRST for every decision (8, 16, 24...)
2. THEN evaluate the context of the project
3. Choose the value that is COMPLIANT with the system but CONTEXTUALLY MOST APPROPRIATE
4. EXPLAIN your decision:

Example:
'I chose 128px for Hero section padding (system: ✓ multiple of 8)
Reason: Luxury brand, should give premium feel, should be spacious.
Alternative 96px could be used but doesn't feel premium enough for this project.
Alternative 160px would be too much, increases scrolling.'

5. If you DEVIATED from standard (e.g., 48px button instead of 40px):
   → Explain: 'This is a primary CTA, should be more emphasized'
   → Prove: 'According to Heatmap data, larger CTAs increase conversion'
   → Verify: '48px is still compliant with system (8 x 6)'

DO NOT USE ANY VALUE THAT DOES NOT FIT THE SYSTEM!
But use the OPTIONS THE SYSTEM OFFERS smartly."
```

---

# 21. Self-Correction Prompt

```
"After completing the design:

1. List all pixel values
2. Divide each by 8
3. If not divisible exactly, DO NOT ROUND to nearest multiple of 8 (up or down)
4. Compare typography values with scale
5. FIX the mismatching ones and STATE 'Correction made'

Example:
❌ Found: margin-top: 30px
✅ Fixed: margin-top: 32px (8 x 4)
📝 Reason: 30px does not fit system, nearest multiple of 8 is 32px"
```

---

# 22. References and Resources

- **Material Design 3**: Google's 2025 design system
- **Tailwind CSS**: Utility-first spacing and typography
- **Radix UI**: Accessible component primitives
- **shadcn/ui**: Modern component system
- **WCAG 2.1 Level AAA**: Accessibility standards
- **8-Point Grid System**: IBM Design Language
- **Type Scale**: modularscale.com / type-scale.com
- **Contrast Checker**: WebAIM contrast checker

---

**Last Update**: December 2025
**Version**: 1.1

### Changelog v1.1
- Typography scale name corrected (Major Third → Practical Scale)
- 768px breakpoint added (iPad portrait support)
- Border radius system simplified (12px note added)
- Tablet container width corrected (720px → 768px)
- 12px padding explanation added
- Focus Visible modern approach added
- Modern CSS Features 2025 section added (Container Queries, System Preferences, Logical Properties)
- Fluid Typography and Fluid Spacing formulas updated
- Tailwind CSS breakpoint mapping added

Designs compliant with this guide will be both visually perfect and technically standardized.
