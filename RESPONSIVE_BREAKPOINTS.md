
# 📱 Responsive Breakpoint System — Professional Design Note
### Next.js + Tailwind CSS | Device Size & Layout Architecture

> **Author Note:** Senior Frontend Architect এর complete responsive breakpoint reference guide।  
> Figma Designer + Developer collaboration এর জন্য complete guideline।  
> পুরো ফাইলটি এক ক্লিকে copy করে আপনার project docs এ paste করুন।

---

## 🧠 কেন Breakpoint System দরকার?

Without a defined breakpoint system:
- Designer random device এ design করে
- Developer guess করে responsive করছে
- Production এ iPad/Tablet এ ভেঙে যায়
- Client বলে "এইটা mobile এ ঠিক নাই"
- QA জানে না কোন device এ test করবে

**Standardized breakpoint system** মানে — সবাই জানে:
- Figma তে কোন ২টা size design করতে হবে
- Developer কোন breakpoint এ কি change করবে
- QA কোন device এ test করবে

---

## 📦 Section 1: Tailwind Default Breakpoints

Tailwind CSS এর built-in breakpoints (mobile-first):

| Breakpoint | Min Width | Device Type |
|------------|-----------|-------------|
| **Default** | 0px | Mobile phone (base styles) |
| **sm** | 640px | Large phone landscape |
| **md** | 768px | Tablet portrait |
| **lg** | 1024px | Tablet landscape / Small laptop |
| **xl** | 1280px | Desktop / Laptop |
| **2xl** | 1536px | Large desktop / Monitor |

### Mobile-first Philosophy:

```tsx
// ✅ Mobile first: base styles → mobile এর জন্য
// তারপর বড় screen এ override

<p className="text-sm md:text-base lg:text-lg">
  Responsive text
</p>

// sm:  → 640px থেকে উপরে apply হবে
// md:  → 768px থেকে উপরে
// lg:  → 1024px থেকে উপরে
// xl:  → 1280px থেকে উপরে
// 2xl: → 1536px থেকে উপরে
```

---

## 📋 Section 2: Device-wise Breakpoint Guide

### 📱 Mobile Phone (Default → sm:)

```
Container:    max-width: 100% (full width)
Padding:      p-4 (16px)
Font Base:    text-body-sm (14px)
Grid:         1 column (grid-cols-1)
Sidebar:      Hidden or bottom
Navigation:   Hamburger menu
Card:         Full width, stacked
Table:        Horizontal scroll
Modal:        Full screen
```

### 📱 Large Phone (sm: 640px+)

```
Container:    max-w-xl (576px)
Padding:      p-6 (24px)
Grid:         2 columns (sm:grid-cols-2)
Sidebar:      Still hidden/bottom
```

### 💻 Tablet (md: 768px+)

```
Container:    max-w-3xl (768px)
Padding:      p-8 (32px)
Font Base:    text-body (16px)
Grid:         2-3 columns (md:grid-cols-2/3)
Sidebar:      Collapsible icon mode
Table:        Full table visible
Modal:        Centered with max-width
```

### 💻 Laptop (lg: 1024px+)

```
Container:    max-w-5xl or max-w-6xl
Padding:      p-10 (40px)
Font Base:    Full desktop scale
Grid:         3-4 columns (lg:grid-cols-3/4)
Sidebar:      Full expanded (240-280px)
Layout:       Sidebar + Content side-by-side
Navigation:   Horizontal
```

### 🖥️ Desktop (xl: 1280px+)

```
Container:    max-w-7xl (1280px)
Padding:      p-12 (48px)
Grid:         4-5 columns (xl:grid-cols-4/5)
Sidebar:      Expanded (280-320px)
Layout:       Full multi-column
Whitespace:   More breathing room
```

### 🖥️ Large Monitor (2xl: 1536px+)

```
Container:    max-w-[1400px] or max-w-[1600px]
Padding:      p-16 (64px)
Grid:         5-6 columns
Extra:        More whitespace, larger gaps
```

---

## 🗺️ Section 3: Breakpoint Decision Flowchart

```
START — Mobile First Design
  │
  ├─ Base styles: Mobile (0px+)
  │   ├─ Single column
  │   ├─ Hamburger menu
  │   └─ 14px body text
  │
  ├─ sm: (640px+) ব্যবহার করবেন যখন:
  │   ├─ Mobile landscape এ layout change দরকার
  │   ├─ 2-column grid শুরু করতে চান
  │   └─ Cards পাশাপাশি দেখাতে চান
  │
  ├─ md: (768px+) ব্যবহার করবেন যখন:
  │   ├─ Tablet এ sidebar show/hide
  │   ├─ Font size bump (14px → 16px)
  │   ├─ Padding increase (16px → 24px)
  │   └─ Table full width দেখাতে চান
  │
  ├─ lg: (1024px+) ব্যবহার করবেন যখন:
  │   ├─ Desktop layout (sidebar + content)
  │   ├─ 3+ column grid
  │   ├─ Navigation horizontal
  │   └─ Sidebar full expanded
  │
  ├─ xl: (1280px+) ব্যবহার করবেন যখন:
  │   ├─ Large desktop extra whitespace
  │   ├─ Complex dashboard layout
  │   ├─ 4+ column grid
  │   └─ Container max-width increase
  │
  └─ 2xl: (1536px+) ব্যবহার করবেন যখন:
      ├─ Ultra-wide monitor optimization
      ├─ Data-heavy tables/dashboards
      └─ Maximum whitespace
```

### Quick Rule of Thumb:

```
sm:  → Grid changes (1→2 columns)
md:  → Typography + Sidebar changes
lg:  → Layout changes (stack → side-by-side)
xl:  → Spacing + Container max-width
2xl: → Large screen polish
```

---

## 🎨 Section 4: Common Responsive Patterns

### Pattern 1: Grid Layout

```tsx
<div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4">
  {cards.map(card => <Card key={card.id} />)}
</div>
```

| Screen | Columns | Gap |
|--------|---------|-----|
| Mobile | 1 | 16px |
| sm: 640px | 2 | 16px |
| lg: 1024px | 3 | 16px |
| xl: 1280px | 4 | 16px |

### Pattern 2: Sidebar + Content Layout

```tsx
<div className="flex flex-col lg:flex-row gap-6">
  {/* Sidebar */}
  <aside className="w-full lg:w-64 xl:w-72 shrink-0">
    <Sidebar />
  </aside>
  
  {/* Content */}
  <main className="flex-1 min-w-0">
    <Content />
  </main>
</div>
```

| Screen | Layout | Sidebar Width |
|--------|--------|---------------|
| Mobile | Stacked (top/bottom) | Full width |
| lg: 1024px | Side-by-side | 256px (w-64) |
| xl: 1280px | Side-by-side | 288px (w-72) |

### Pattern 3: Padding Scale

```tsx
<div className="p-4 sm:p-6 md:p-8 lg:p-10 xl:p-12">
  Content
</div>
```

| Screen | Padding |
|--------|---------|
| Mobile | 16px (p-4) |
| sm: 640px | 24px (p-6) |
| md: 768px | 32px (p-8) |
| lg: 1024px | 40px (p-10) |
| xl: 1280px | 48px (p-12) |

### Pattern 4: Typography Scale

```tsx
<h1 className="text-heading-2 md:text-heading-1 lg:text-display">
  Dashboard
</h1>

<p className="text-body-sm md:text-body">
  Description text that scales with device
</p>
```

| Element | Mobile | md: 768px | lg: 1024px |
|---------|--------|-----------|------------|
| h1 | text-heading-2 (24px) | text-heading-1 (32px) | text-display (40px) |
| p | text-body-sm (14px) | text-body (16px) | text-body (16px) |

### Pattern 5: Hide/Show Elements

```tsx
{/* Mobile menu button — only on small screens */}
<button className="block lg:hidden">
  <MenuIcon />
</button>

{/* Desktop navigation — hidden on mobile */}
<nav className="hidden lg:flex items-center gap-6">
  <Link href="/dashboard">Dashboard</Link>
  <Link href="/orders">Orders</Link>
  <Link href="/settings">Settings</Link>
</nav>

{/* Tablet and above */}
<div className="hidden md:block">
  <Filters />
</div>
```

| Element | Mobile | Tablet (md:) | Desktop (lg:) |
|---------|--------|--------------|---------------|
| Hamburger | ✅ Visible | ✅ Visible | ❌ Hidden |
| Nav Links | ❌ Hidden | ❌ Hidden | ✅ Visible |
| Filters | ❌ Hidden | ✅ Visible | ✅ Visible |

### Pattern 6: Table Responsive

```tsx
<div className="overflow-x-auto">
  <table className="w-full min-w-[600px] md:min-w-full">
    ...
  </table>
</div>
```

| Screen | Behavior |
|--------|----------|
| Mobile | Horizontal scroll |
| md: 768px+ | Full table visible |

### Pattern 7: Modal/Dialog Responsive

```tsx
<div className="fixed inset-0 z-50 flex items-center justify-center p-4">
  <div className="bg-card w-full max-w-lg max-h-[90vh] overflow-y-auto rounded-2xl p-6">
    ...
  </div>
</div>
```

---

## 📏 Section 5: Container Max-Width Guide

```tsx
// Responsive container (Tailwind default)
<div className="container mx-auto">
  Auto-responsive width
</div>

// Fixed max-width containers
<div className="max-w-sm mx-auto">   // 384px  — Small card
<div className="max-w-md mx-auto">   // 448px  — Form
<div className="max-w-lg mx-auto">   // 512px  — Modal
<div className="max-w-xl mx-auto">   // 576px  — Narrow content
<div className="max-w-2xl mx-auto">  // 672px  — Blog post
<div className="max-w-3xl mx-auto">  // 768px  — Content page
<div className="max-w-4xl mx-auto">  // 896px  — Wide content
<div className="max-w-5xl mx-auto">  // 1024px — Standard dashboard
<div className="max-w-6xl mx-auto">  // 1152px — Wide dashboard
<div className="max-w-7xl mx-auto">  // 1280px — Full dashboard
```

### When to Use:

| Container | Use Case |
|-----------|----------|
| `max-w-sm` → `max-w-md` | Forms, small cards, modals |
| `max-w-lg` → `max-w-xl` | Narrow content, single column |
| `max-w-2xl` → `max-w-3xl` | Blog, article, documentation |
| `max-w-4xl` → `max-w-5xl` | Standard dashboard, list pages |
| `max-w-6xl` → `max-w-7xl` | Complex dashboard, data tables |

---

## 📐 Section 6: Responsive Spacing Guide

### Section Spacing:

```tsx
<section className="py-12 md:py-16 lg:py-20 xl:py-24">
  ...
</section>
```

### Card Gaps:

```tsx
<div className="space-y-4 md:space-y-6">
  {items.map(item => <Card />)}
</div>
```

### Page Header Spacing:

```tsx
<div className="mb-6 md:mb-8 lg:mb-10">
  <h1>...</h1>
</div>
```

---

## 🎯 Section 7: Figma Designer ↔ Developer Handoff

### Figma Designer তৈরি করবে ২টা Frame:

```
Frame 1: Mobile (375px × auto)
  - iPhone SE/6/7/8 width
  - Single column
  - Hamburger menu
  - Stacked cards
  - text-body-sm (14px) base
  - p-4 (16px) padding

Frame 2: Desktop (1440px × auto)
  - Standard laptop width
  - Multi column
  - Full sidebar (280px)
  - Horizontal navigation
  - text-body (16px) base
  - p-10 (40px) padding
```

### Developer Implementation:

```tsx
// Figma Mobile (375px)  → Default/base classes
// Figma Desktop (1440px) → lg: or xl: classes

// Example: Figma mobile এ 24px, desktop এ 32px
<h1 className="text-heading-2 lg:text-heading-1">
  Page Title
</h1>

// Example: Figma mobile এ stacked, desktop এ side-by-side
<div className="flex flex-col lg:flex-row gap-4 lg:gap-6">
  <aside className="w-full lg:w-64">Sidebar</aside>
  <main className="flex-1">Content</main>
</div>
```

---

## 🛠️ Section 8: Testing Checklist

### Devices to Test:

```
📱 MOBILE:
□ iPhone SE (375px)
□ iPhone 12/13/14 (390px)
□ iPhone 14 Pro Max (430px)
□ Samsung Galaxy (412px)

📱 TABLET:
□ iPad Mini (768px)
□ iPad Air (820px)
□ iPad Pro (1024px)

💻 DESKTOP:
□ Laptop (1366px - most common)
□ Desktop (1440px)
□ Desktop (1920px)
□ Ultra-wide (2560px)
```

### Quick Test in Browser:

```
Chrome DevTools → Device Toolbar (Ctrl+Shift+M)
  ├─ iPhone SE (375px)
  ├─ iPad (768px)
  ├─ iPad Pro (1024px)
  └─ Responsive mode → drag to test any width
```

---

## ❌ Section 9: Common Responsive Mistakes

```
❌ Desktop-first design (max-width breakpoints)
❌ Mobile এ content hide করে দেওয়া
❌ Fixed width container (w-[1200px])
❌ Mobile এ tiny font size (< 14px)
❌ Touch target খুব ছোট (< 44px)
❌ Tablet breakpoint skip করা
❌ Overflow hidden দিয়ে content লুকানো
❌ Mobile এ hover state rely করা
❌ Desktop এ mobile menu দেখানো
```

### ✅ Correct Approach:

```
✅ Mobile-first design (min-width breakpoints)
✅ Mobile এ simplified layout, content same
✅ Max-width container (max-w-7xl)
✅ Minimum 14px body text on mobile
✅ Minimum 44px touch targets
✅ Test on real tablet (768px)
✅ Overflow-x-auto for tables
✅ Click/tap events, not hover
✅ lg:hidden for mobile menu
```

---

## 📊 Section 10: Breakpoint Usage Statistics

Real-world project এ কোন breakpoint কতবার use হয়:

```
Distribution in a typical project:

Default (mobile):    ████████████████████ 100% (always)
sm: (640px):         ████████             40%
md: (768px):         ██████████████       70%
lg: (1024px):        ████████████████████ 90%
xl: (1280px):        ██████               30%
2xl: (1536px):       ██                   10%
```

**Most used:** `md:` এবং `lg:` — এই দুটি breakpoint সবচেয়ে বেশি ব্যবহার হয়।

---

## ✅ Section 11: Complete Responsive Checklist

```
SETUP:
□ Mobile-first CSS (min-width breakpoints)
□ <meta name="viewport"> in layout
□ html suppressHydrationWarning
□ Container max-width ব্যবহার করছি (fixed width না)

LAYOUT:
□ Mobile: single column, stacked
□ lg: sidebar + content side-by-side
□ min-w-0 on flex children (prevent overflow)
□ overflow-x-auto for tables

TYPOGRAPHY:
□ Mobile: text-body-sm (14px) base
□ md: text-body (16px) base
□ Headings scale with breakpoints
□ No text overflow (truncate/break-words)

SPACING:
□ Mobile: p-4 (16px)
□ md: p-6/p-8 (24px/32px)
□ lg: p-8/p-10 (32px/40px)
□ Gap scales with screen size

INTERACTIONS:
□ Touch targets minimum 44x44px
□ No hover-only interactions on mobile
□ Hamburger menu: lg:hidden
□ Desktop nav: hidden lg:flex

TESTING:
□ iPhone SE (375px)
□ iPad (768px)
□ Laptop (1366px)
□ Desktop (1440px/1920px)
□ No horizontal scroll on mobile
```

---

## 📌 Quick Reference Card

```
BREAKPOINTS:
Default  0px        Mobile phone
sm:      640px      Phone landscape
md:      768px      Tablet portrait
lg:      1024px     Laptop
xl:      1280px     Desktop
2xl:     1536px     Large monitor

WHAT CHANGES WHEN:
sm:  → Grid (1→2 cols), cards side-by-side
md:  → Font size (14→16px), sidebar toggle, padding
lg:  → Layout (stack→side), full sidebar, horizontal nav
xl:  → Container wider, more whitespace, 4+ cols
2xl: → Ultra-wide polish

COMMON PATTERNS:
grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4
flex-col lg:flex-row
p-4 sm:p-6 md:p-8 lg:p-10 xl:p-12
text-body-sm md:text-body
block lg:hidden
hidden lg:flex
w-full lg:w-64 xl:w-72

CONTAINER SIZES:
max-w-sm    384px   Card, form
max-w-md    448px   Form
max-w-lg    512px   Modal
max-w-xl    576px   Narrow
max-w-2xl   672px   Blog
max-w-3xl   768px   Content
max-w-4xl   896px   Wide content
max-w-5xl   1024px  Dashboard
max-w-6xl   1152px  Wide dashboard
max-w-7xl   1280px  Full dashboard
```

---

> **Final Note:** এই Breakpoint System follow করলে mobile থেকে ultra-wide monitor পর্যন্ত সব device এ আপনার application perfect দেখাবে।  
> Figma designer ২টা frame বানাবে, developer breakpoint ধরে implement করবে — zero confusion, pixel-perfect result।

*— Responsive Breakpoint System Reference v1.0 | Next.js + Tailwind CSS + Figma Handoff*
```