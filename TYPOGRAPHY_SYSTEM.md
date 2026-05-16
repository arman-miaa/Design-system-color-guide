
# 📐 Typography System — Professional Design Note
### Next.js + Tailwind CSS | Font Size, Weight & Line Height Architecture

> **Author Note:** Senior Frontend Architect এর complete typography reference guide।  
> Figma Designer + Developer collaboration এর জন্য complete guideline।

---

## 🧠 কেন Typography System দরকার?

Hardcoded font size (যেমন `text-[17px]`, `text-[23px]`) ব্যবহার করলে:
- Figma designer এর সাথে mismatch হয়
- Responsive breakpoint এ manually সব জায়গায় change করতে হয়
- Team consistency নষ্ট হয়
- Accessibility (WCAG) কমপ্লায়েন্স fail করে

**Semantic Typography System** মানে — প্রতিটি text element এর **role/purpose** অনুযায়ী নাম দেওয়া।
যেমন: `text-heading-1`, `text-body`, `text-caption` — এগুলো pixel value না, text এর **কী কাজ** সেটা বলে।

---

## 📦 Section 1: Typography Token Structure

প্রতিটি typography token এ ৪টি property define করতে হবে:

```
1. font-size      → কত বড় (px বা rem)
2. line-height    → লাইনের মধ্যে gap
3. font-weight    → কতটা bold (400, 500, 600, 700)
4. letter-spacing → অক্ষরের মধ্যে gap
```

### Token নামকরণ Convention:
```
naming pattern:  text-{role}

Examples:
  text-display      → hero title
  text-heading-1    → page title
  text-heading-2    → section title
  text-heading-3    → card title
  text-heading-4    → dialog title
  text-body         → paragraph
  text-body-sm      → secondary text
  text-caption      → timestamp, helper
  text-label        → badge, overline
  text-xs           → smallest label
```

---

## 📋 Section 2: Complete Typography Scale

### Professional Scale (10px → 40px):

| Token | Size | Line Height | Weight | Letter Spacing | Use Case |
|-------|------|-------------|--------|----------------|----------|
| `text-display` | 40px (2.5rem) | 1.2 | **700** (Bold) | -0.02em | Hero title |
| `text-heading-1` | 32px (2rem) | 1.3 | **600** (Semibold) | -0.01em | Page title |
| `text-heading-2` | 24px (1.5rem) | 1.35 | **600** | 0 | Section title |
| `text-heading-3` | 20px (1.25rem) | 1.4 | **600** | 0 | Card title |
| `text-heading-4` | 18px (1.125rem) | 1.45 | **500** (Medium) | 0 | Dialog title |
| `text-body` | 16px (1rem) | 1.6 | **400** (Regular) | 0 | Paragraph |
| `text-body-sm` | 14px (0.875rem) | 1.6 | **400** | 0 | Secondary text |
| `text-caption` | 12px (0.75rem) | 1.5 | **400** | 0.01em | Timestamp, helper |
| `text-label` | 11px (0.6875rem) | 1.4 | **600** | 0.08em | Badge, overline |
| `text-xs` | 10px (0.625rem) | 1.4 | **700** | 0.15em | Uppercase label |

---

## 🗺️ Section 3: কোন Text কোথায় Use করতে হয়

### Page Structure Map:

```
APPLICATION LAYER
│
├── HERO SECTION
│   ├── Title         → text-display (40px, 700)
│   └── Subtitle      → text-body (16px, 400, muted)
│
├── PAGE HEADER
│   ├── Title         → text-heading-1 (32px, 600)
│   ├── Description   → text-body-sm (14px, 400, muted)
│   └── Breadcrumb    → text-caption (12px, 400)
│
├── CARD COMPONENT
│   ├── Title         → text-heading-3 (20px, 600)
│   ├── Description   → text-body-sm (14px, 400)
│   ├── Meta Info     → text-caption (12px, muted)
│   └── Badge/Status  → text-label (11px, 600, uppercase)
│
├── TABLE
│   ├── Header        → text-xs (10px, 700, uppercase)
│   ├── Cell          → text-body-sm (14px, 400)
│   └── ID/Code       → text-caption (12px, mono)
│
├── FORM
│   ├── Label         → text-label (11px, 600, uppercase)
│   ├── Input Text    → text-body-sm (14px, 400)
│   ├── Placeholder   → text-body-sm + muted
│   └── Error         → text-caption (12px, destructive)
│
├── MODAL / DIALOG
│   ├── Title         → text-heading-4 (18px, 500)
│   └── Body          → text-body-sm (14px, 400)
│
├── SIDEBAR
│   ├── Section Title → text-label (11px, 600, uppercase)
│   ├── Nav Item      → text-body-sm (14px, 400)
│   └── Active Item   → text-body-sm + medium
│
└── FOOTER
    ├── Heading       → text-heading-4 (18px, 500)
    ├── Link          → text-caption (12px, 400)
    └── Copyright     → text-xs (10px)
```

---

## 🎨 Section 4: Typography + Color Pairing Rules

### Heading Colors:
```
text-heading-1 + text-foreground       → সবচেয়ে prominent
text-heading-2 + text-foreground       → section title
text-heading-3 + text-card-foreground  → card title
```

### Body Text Colors:
```
text-body + text-foreground            → main content
text-body + text-muted-foreground      → description/subtitle
text-caption + text-muted-foreground   → meta info, timestamp
```

### Label/Badge Colors:
```
text-label + text-primary-foreground   → primary badge
text-label + text-success              → success badge
text-label + text-destructive          → error badge
text-label + text-warning              → pending badge
```

### Link Colors:
```
text-body-sm + text-primary + underline              → inline link
text-caption + text-muted-foreground + hover:text-foreground → subtle link
```

---

## 🔍 Section 5: Real-World Code Examples

### Example 1: Page Header

```tsx
<div className="mb-8">
  {/* Breadcrumb */}
  <p className="text-xs uppercase tracking-[0.18em] text-muted-foreground mb-2">
    Orders / Details
  </p>
  
  {/* Page Title */}
  <h1 className="text-heading-1 text-foreground">
    Order #AUR-8821
  </h1>
  
  {/* Description */}
  <p className="text-body-sm text-muted-foreground mt-2 max-w-2xl">
    Manage your artisan jewelry inventory and logistics.
  </p>
</div>
```

### Example 2: Card Component

```tsx
<div className="bg-card border border-border rounded-xl p-5">
  {/* Badge */}
  <span className="text-label uppercase tracking-[0.15em] text-primary bg-primary/10 px-2 py-0.5 rounded">
    Best Seller
  </span>
  
  {/* Title */}
  <h3 className="text-heading-3 text-card-foreground mt-3">
    Ethereal Solitaire Ring
  </h3>
  
  {/* Description */}
  <p className="text-body-sm text-muted-foreground mt-2">
    Crafted in 18K White Gold with 2.5ct ethically sourced diamond
  </p>
  
  {/* Meta */}
  <div className="flex items-center gap-2 mt-4">
    <span className="text-caption text-muted-foreground">Oct 24, 2023</span>
    <span className="text-caption text-muted-foreground">·</span>
    <span className="text-caption text-muted-foreground">5 min read</span>
  </div>
</div>
```

### Example 3: Table Component

```tsx
<table className="w-full">
  <thead>
    <tr className="border-b border-border bg-muted">
      <th className="text-xs uppercase tracking-[0.15em] text-muted-foreground px-4 py-3 text-left">
        Order ID
      </th>
      <th className="text-xs uppercase tracking-[0.15em] text-muted-foreground px-4 py-3 text-left">
        Customer
      </th>
      <th className="text-xs uppercase tracking-[0.15em] text-muted-foreground px-4 py-3 text-left">
        Status
      </th>
    </tr>
  </thead>
  <tbody>
    <tr className="border-b border-border">
      <td className="text-caption font-mono text-muted-foreground px-4 py-3">
        #AUR-8821
      </td>
      <td className="text-body-sm text-foreground px-4 py-3">
        Eleanor Thorne
      </td>
      <td className="px-4 py-3">
        <span className="text-label text-success bg-success/10 px-2 py-0.5 rounded">
          COMPLETED
        </span>
      </td>
    </tr>
  </tbody>
</table>
```

### Example 4: Form Input

```tsx
<div className="space-y-1.5">
  <label className="text-label uppercase tracking-[0.15em] text-muted-foreground">
    Email Address
  </label>
  <input 
    type="email" 
    placeholder="you@example.com"
    className="text-body-sm border border-input rounded-lg px-3 py-2 w-full"
  />
  <p className="text-caption text-destructive">Invalid email address</p>
</div>
```

### Example 5: Sidebar Navigation

```tsx
<aside className="bg-sidebar border-r border-border p-4">
  <p className="text-label uppercase tracking-[0.15em] text-muted-foreground mb-3 px-2">
    Main Menu
  </p>
  
  <nav className="space-y-1">
    <a href="/dashboard" className="text-body-sm font-medium bg-primary/10 text-primary px-3 py-2 rounded-lg block">
      Dashboard
    </a>
    <a href="/orders" className="text-body-sm text-sidebar-foreground hover:bg-accent px-3 py-2 rounded-lg block">
      Orders
    </a>
    <a href="/settings" className="text-body-sm text-sidebar-foreground hover:bg-accent px-3 py-2 rounded-lg block">
      Settings
    </a>
  </nav>
</aside>
```

---

## 📱 Section 6: Responsive Typography

### Mobile → Desktop Font Scaling:

```tsx
// Hero: smaller on mobile, full size on tablet+
<h1 className="text-heading-1 md:text-display">Welcome</h1>

// Page title: scales up
<h1 className="text-heading-2 md:text-heading-1">Dashboard</h1>

// Section title
<h2 className="text-heading-3 md:text-heading-2">Recent Orders</h2>

// Card title
<h3 className="text-heading-4 md:text-heading-3">Card Title</h3>

// Body text
<p className="text-body-sm md:text-body">Description text</p>
```

### Recommended Scale Per Device:

| Token | Mobile (default) | Tablet (md:) | Desktop (lg:) |
|-------|-----------------|--------------|---------------|
| Display | `text-heading-1` (32px) | `text-display` (40px) | `text-display` (40px) |
| Heading-1 | `text-heading-2` (24px) | `text-heading-1` (32px) | `text-heading-1` (32px) |
| Heading-2 | `text-heading-3` (20px) | `text-heading-2` (24px) | `text-heading-2` (24px) |
| Heading-3 | `text-heading-4` (18px) | `text-heading-3` (20px) | `text-heading-3` (20px) |
| Body | `text-body-sm` (14px) | `text-body` (16px) | `text-body` (16px) |

---

## 🎯 Section 7: Font Weight Guide

### Weight Scale:

| Weight Name | Value | Use Case |
|-------------|-------|----------|
| **Regular** | 400 | Body text, paragraph, description |
| **Medium** | 500 | Dialog title, emphasis, subtle highlight |
| **Semibold** | 600 | Headings (h1-h4), active nav, labels |
| **Bold** | 700 | Hero title, key metrics, strong emphasis |

### Weight Usage Rules:

```
700 Bold  → শুধু hero title, key metric ( sparingly use )
600 Semibold → সব headings, labels, badges ( most used )
500 Medium   → dialog title, emphasis
400 Regular  → সব body text, caption ( default )
```

### ❌ Common Mistakes:
```
❌ সব জায়গায় 700 bold — visually overwhelming
❌ Body text এ 600 semibold — readability কমে
❌ Heading আর body same weight — hierarchy নষ্ট
```

### ✅ Correct Usage:
```tsx
<h1 className="text-heading-1">Dashboard</h1>           // 600
<p className="text-body text-muted-foreground">Desc</p>   // 400
<span className="text-label uppercase">Badge</span>       // 600
<strong className="font-semibold">Important</strong>      // 600
<b className="font-bold">Critical</b>                     // 700
```

---

## 📏 Section 8: Line Height Guide

### Line Height Scale:

| Text Type | Line Height | Rule |
|-----------|-------------|------|
| Display/Hero | 1.2 | Tight — short text |
| Headings | 1.3 - 1.45 | Slightly loose |
| Body | 1.5 - 1.6 | Comfortable reading |
| Caption/Label | 1.4 - 1.5 | Compact |

### Why Line Height Matters:

```
❌ line-height: 1.0
   "Text looks cramped and
   hard to read comfortably"
   
✅ line-height: 1.6
   "Text breathes naturally
   and is easy to scan quickly"
```

---

## 🔤 Section 9: Letter Spacing Guide

### Letter Spacing Scale:

| Usage | Value | Example |
|-------|-------|---------|
| Tight (headings) | -0.02em to -0.01em | Hero, page title |
| Normal | 0 | Body, description |
| Wide (uppercase) | 0.08em to 0.15em | Badge, label, overline |

### When to Use:

```tsx
// Uppercase labels — always add letter-spacing
<span className="text-label uppercase tracking-[0.15em]">VERIFIED</span>

// Hero title — tight for impact
<h1 className="text-display tracking-tight">Welcome</h1>

// Body text — normal spacing
<p className="text-body">Description here</p>
```

---

## 🛠️ Section 10: Tailwind 4 Setup

### Step 1: `globals.css` এ Typography Tokens

```css
:root {
  /* Font Sizes */
  --text-display:    2.5rem;   /* 40px */
  --text-heading-1:  2rem;     /* 32px */
  --text-heading-2:  1.5rem;   /* 24px */
  --text-heading-3:  1.25rem;  /* 20px */
  --text-heading-4:  1.125rem; /* 18px */
  --text-body:       1rem;     /* 16px */
  --text-body-sm:    0.875rem; /* 14px */
  --text-caption:    0.75rem;  /* 12px */
  --text-label:      0.6875rem;/* 11px */
  --text-xs:         0.625rem; /* 10px */

  /* Line Heights */
  --leading-display:   1.2;
  --leading-heading:   1.35;
  --leading-body:      1.6;
  --leading-caption:   1.5;
  --leading-label:     1.4;

  /* Letter Spacing */
  --tracking-tight:   -0.02em;
  --tracking-normal:   0;
  --tracking-wide:     0.01em;
  --tracking-wider:    0.08em;
  --tracking-widest:   0.15em;
}
```

### Step 2: Tailwind 4 `@theme inline` Map

```css
@theme inline {
  --font-size-display:    var(--text-display);
  --font-size-heading-1:  var(--text-heading-1);
  --font-size-heading-2:  var(--text-heading-2);
  --font-size-heading-3:  var(--text-heading-3);
  --font-size-heading-4:  var(--text-heading-4);
  --font-size-body:       var(--text-body);
  --font-size-body-sm:    var(--text-body-sm);
  --font-size-caption:    var(--text-caption);
  --font-size-label:      var(--text-label);
  --font-size-xs:         var(--text-xs);
}
```

### Step 3: Font Family Setup (next/font)

```tsx
// app/layout.tsx
import { Inter, JetBrains_Mono } from 'next/font/google';

const inter = Inter({ 
  subsets: ['latin'],
  variable: '--font-sans',
});

const jetbrainsMono = JetBrains_Mono({
  subsets: ['latin'],
  variable: '--font-mono',
});

export default function RootLayout({ children }) {
  return (
    <html className={`${inter.variable} ${jetbrainsMono.variable}`}>
      <body className="font-sans text-body text-foreground bg-background">
        {children}
      </body>
    </html>
  );
}
```

---

## 🎯 Section 11: Typography Best Practices

### ✅ DO's:

```
✅ Heading hierarchy বজায় রাখুন: h1 → h2 → h3 (skip করবেন না)
✅ Body text minimum 16px (desktop), 14px (mobile)
✅ Line height body text: 1.5-1.6
✅ Max-width paragraph: 65-75 characters (~32rem)
✅ Heading weight: 600 (semibold), hero: 700 (bold)
✅ Uppercase text এ letter-spacing 0.08em-0.15em যোগ করুন
✅ Mobile এ heading size একটু কমান
✅ Font stack এ fallback fonts রাখুন
✅ font-sans সব UI elements এর জন্য default হিসেবে ব্যবহার করুন
✅ font-mono শুধু code, IDs, technical data এর জন্য
```

### ❌ DON'Ts:

```
❌ Body text 14px এর নিচে নামাবেন না (accessibility fail)
❌ Heading এ 700 bold বেশি use করবেন না — overwhelming
❌ ৩ লাইনের বেশি center-align করবেন না
❌ Pure black (#000) text ব্যবহার করবেন না — harsh
❌ Line height 1.0 এর কাছাকাছি রাখবেন না — crammed
❌ Body text এ negative letter-spacing দেবেন না
❌ All caps ৩ words এর বেশি করবেন না — hard to read
❌ একাধিক font family mix করবেন না (max 2: sans + mono)
❌ Inline style এ font-size দেবেন না
```

---

## 📐 Section 12: Visual Hierarchy Map

```
📰 TYPOGRAPHY WEIGHT DISTRIBUTION

┌─────────────────────────────────────────────┐
│ DISPLAY (40px, 700, -0.02em)                │ ← HIGHEST
│ Hero section only                           │   Use sparingly
├─────────────────────────────────────────────┤
│ HEADING 1 (32px, 600, -0.01em)              │
│ Page title                                  │
├─────────────────────────────────────────────┤
│ HEADING 2 (24px, 600)                       │
│ Section title                               │
├─────────────────────────────────────────────┤
│ HEADING 3 (20px, 600)                       │
│ Card title                                  │
├─────────────────────────────────────────────┤
│ HEADING 4 (18px, 500)                       │
│ Dialog title                                │
├─────────────────────────────────────────────┤
│ BODY (16px, 400)                            │ ← BASELINE
│ Paragraph, main content                     │   Default
├─────────────────────────────────────────────┤
│ BODY SM (14px, 400)                         │
│ Description, secondary info                 │
├─────────────────────────────────────────────┤
│ CAPTION (12px, 400, 0.01em)                 │
│ Timestamp, meta, helper text                │
├─────────────────────────────────────────────┤
│ LABEL (11px, 600, 0.08em, uppercase)        │ ← LOWEST
│ Badge, overline, table header               │   Small but bold
├─────────────────────────────────────────────┤
│ XS (10px, 700, 0.15em, uppercase)          │
│ Smallest label                              │
└─────────────────────────────────────────────┘
```

---

## ✅ Section 13: Complete Typography Checklist

```
SETUP:
□ next/font দিয়ে font-sans, font-mono setup
□ globals.css এ typography tokens define
□ @theme inline এ Tailwind map
□ body তে font-sans + text-body + text-foreground
□ html এ suppressHydrationWarning

HIERARCHY:
□ Heading hierarchy h1→h2→h3 correct
□ Hero title text-display (700)
□ Page title text-heading-1 (600)
□ Card title text-heading-3 (600)
□ No skipped heading levels

READABILITY:
□ Body text 16px desktop, 14px mobile
□ Line height 1.5-1.6 body text
□ Max-width paragraph ~32rem (65-75 chars)
□ Letter spacing uppercase labels (0.08em+)

CONSISTENCY:
□ No hardcoded [text-[17px]]
□ All badges use text-label
□ All timestamps use text-caption
□ All descriptions use text-body-sm
□ All table headers use text-xs uppercase

RESPONSIVE:
□ Mobile: smaller headings
□ md: bump body to 16px
□ lg: full desktop scale
```

---

## 📌 Quick Reference Card

```
CLASS               SIZE    WEIGHT  LINE-H  LETTER      USE CASE
text-display        40px    700     1.2     -0.02em     Hero title
text-heading-1      32px    600     1.3     -0.01em     Page title
text-heading-2      24px    600     1.35    0           Section title
text-heading-3      20px    600     1.4     0           Card title
text-heading-4      18px    500     1.45    0           Dialog title
text-body           16px    400     1.6     0           Paragraph
text-body-sm        14px    400     1.6     0           Description
text-caption        12px    400     1.5     +0.01em     Timestamp
text-label          11px    600     1.4     +0.08em     Badge
text-xs             10px    700     1.4     +0.15em     Label
```

### Font Weight Quick Guide:
```
400 Regular  → Body, description (default)
500 Medium   → Dialog title, subtle emphasis
600 Semibold → Headings, labels, active nav
700 Bold     → Hero, key metrics (rare)
```

### Font Family Quick Guide:
```
font-sans  → All UI elements (Inter, system)
font-serif → Quotes, luxury/elegant sections
font-mono  → Order IDs, codes, technical data
```

---

> **Final Note:** এই Typography System আপনার পুরো project কে দেবে consistent look & feel।  
> Figma designer text styles define করবে, developer tokens use করবে — zero friction।  
> Mobile থেকে desktop পর্যন্ত সব device এ perfect readability guarantee।

*— Typography System Reference v1.0 | Next.js + Tailwind 4 + Figma Handoff*
```