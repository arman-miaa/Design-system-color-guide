# 🎨 Semantic Color System — Professional Design Note
### Next.js + Tailwind CSS | Light & Dark Mode Architecture
> **Author Note:** এটি একটি senior frontend architect এর personal reference note।  
> Future সব project এ এই guide follow করলে consistent, maintainable, scalable color system পাবে।

---

## 🧠 কেন Semantic Color System দরকার?

Hardcoded color (যেমন `bg-[#3b0014]`, `text-gray-700`) লেখা হলে:

- Dark mode করতে গেলে **প্রতিটা component manually পরিবর্তন** করতে হয়
- Design change হলে **শত শত জায়গায় খুঁজে** পরিবর্তন করতে হয়
- Team এ কাজ করলে **inconsistency** তৈরি হয়

**Semantic naming** মানে color এর actual value না, বরং **role/purpose** অনুযায়ী নাম দেওয়া।  
যেমন: `--background`, `--primary`, `--muted` — এগুলো কোনো specific color না, এগুলো **কী কাজ করে** সেটা বলে।

---

## 📦 Section 1: কত ধরনের Color Token দরকার?

একটি large-scale professional project এ সাধারণত **৫টি category** তে color token রাখা হয়:

```
1. Surface Colors      → background, card, popover, sidebar
2. Text Colors         → foreground, muted-foreground
3. Brand Colors        → primary, secondary, accent
4. Feedback Colors     → destructive, success, warning, info
5. UI Chrome Colors    → border, input, ring
```

এছাড়া **Chart / Data Viz** এর জন্য আলাদা `--chart-1` থেকে `--chart-5` রাখা হয়।

---

## 📋 Section 2: Color Token এর নাম কী হওয়া উচিত?

### ✅ Surface Tokens (পৃষ্ঠতল / layer রঙ)

| Token Name | কী বোঝায় |
|---|---|
| `--background` | পুরো page এর main background |
| `--foreground` | background এর উপরের default text color |
| `--card` | card component এর background |
| `--card-foreground` | card এর ভেতরের text color |
| `--popover` | dropdown, tooltip, modal এর background |
| `--popover-foreground` | popover এর ভেতরের text color |
| `--sidebar` | sidebar panel এর background |
| `--sidebar-foreground` | sidebar এর text color |

### ✅ Brand / Action Tokens

| Token Name | কী বোঝায় |
|---|---|
| `--primary` | main brand color, CTA button background |
| `--primary-foreground` | primary button এর উপরের text |
| `--secondary` | secondary button, subtle highlight |
| `--secondary-foreground` | secondary element এর text |
| `--accent` | hover state, active state, subtle highlight |
| `--accent-foreground` | accent background এর উপরের text |

### ✅ Feedback / Status Tokens

| Token Name | কী বোঝায় |
|---|---|
| `--destructive` | error, delete, danger — red zone |
| `--destructive-foreground` | destructive background এর text |
| `--success` | সফল action, verified status |
| `--success-foreground` | success background এর text |
| `--warning` | সতর্কতা, pending status |
| `--warning-foreground` | warning background এর text |
| `--info` | informational message |
| `--info-foreground` | info background এর text |

### ✅ UI Chrome Tokens

| Token Name | কী বোঝায় |
|---|---|
| `--border` | card, input, divider এর border color |
| `--input` | input field এর border/background |
| `--ring` | focus ring (accessibility) |
| `--muted` | disabled, placeholder এর background |
| `--muted-foreground` | secondary text, subtitle, caption |

---

## 🗺️ Section 3: কোন Color কোথায় Use করতে হয়?

```
Page Layout:
  └─ body background          → var(--background)
  └─ main text                → var(--foreground)

Cards & Panels:
  └─ card background          → var(--card)
  └─ card text                → var(--card-foreground)
  └─ card border              → var(--border)

Buttons:
  └─ primary button bg        → var(--primary)
  └─ primary button text      → var(--primary-foreground)
  └─ secondary button bg      → var(--secondary)
  └─ secondary button text    → var(--secondary-foreground)
  └─ destructive button       → var(--destructive)

Text Hierarchy:
  └─ heading / main text      → var(--foreground)
  └─ subtitle / caption       → var(--muted-foreground)
  └─ placeholder text         → var(--muted-foreground) + opacity

Form Elements:
  └─ input border             → var(--input)
  └─ input focus ring         → var(--ring)
  └─ disabled state           → var(--muted)

Status Badges:
  └─ success badge bg         → var(--success) [with opacity]
  └─ success badge text       → var(--success-foreground)
  └─ warning badge            → var(--warning)
  └─ error / alert            → var(--destructive)

Sidebar:
  └─ sidebar bg               → var(--sidebar)
  └─ sidebar text             → var(--sidebar-foreground)
  └─ sidebar active item      → var(--sidebar-primary)
  └─ sidebar hover            → var(--sidebar-accent)
```

---

## ☯️ Section 4: Light Mode vs Dark Mode — কীভাবে Color Pair কাজ করে?

Light mode এ `--background` = সাদা (oklch 1), dark mode এ সেটাই হয়ে যায় গাঢ় কালো (oklch 0.145)।  
Component এ কোথাও hardcode নেই — **শুধু variable পরিবর্তন হয়, component একই থাকে।**

```
                LIGHT MODE          DARK MODE
--background:   #FFFFFF             #1a1a1a (near black)
--foreground:   #0a0a0a (near blk)  #fafafa (near white)
--card:         #FFFFFF             #262626
--border:       #e5e5e5 (light)     rgba(255,255,255,0.1)
--primary:      #3b0014 (brand)     #e5e5e5 (inverted)
--muted:        #f5f5f5             #2d2d2d
--muted-fg:     #737373             #a3a3a3
```

**Rule:** Light mode এ dark text + light surface। Dark mode এ light text + dark surface।

---

## 🔍 Section 5: প্রতিটি Token বিস্তারিত Explanation

### `--background` / `--foreground`
সবচেয়ে base layer। `body` tag এ apply হয়।
```css
body {
  background-color: var(--background);
  color: var(--foreground);
}
```
Light: সাদা background, প্রায় কালো text।  
Dark: গাঢ় background, প্রায় সাদা text।

---

### `--card` / `--card-foreground`
Card component এর জন্য। Light mode এ background এর মতোই সাদা (বা সামান্য tinted),
dark mode এ background এর থেকে সামান্য lighter হয় যাতে elevation বোঝা যায়।

```tsx
<div className="bg-card text-card-foreground border border-border rounded-xl p-4">
  ...
</div>
```

---

### `--muted` / `--muted-foreground`
**সবচেয়ে বেশি ব্যবহৃত pair।**

- `--muted`: disabled button, skeleton loader, subtle section background
- `--muted-foreground`: subtitle, caption, placeholder, secondary info text

```tsx
<p className="text-muted-foreground text-sm">Last updated 2 hours ago</p>
<div className="bg-muted rounded-lg p-3">Disabled section</div>
```

---

### `--primary` / `--primary-foreground`
Brand এর main color। CTA button, active nav item, selected state।

```tsx
<button className="bg-primary text-primary-foreground px-4 py-2 rounded-lg">
  Get Started
</button>
```

Dark mode এ primary অনেক সময় **inverted** হয় — কারণ dark background এ dark primary দেখা যায় না।

---

### `--secondary` / `--secondary-foreground`
Primary এর পাশে supporting action। Ghost button, outline button, tags।

```tsx
<button className="bg-secondary text-secondary-foreground px-4 py-2 rounded-lg">
  Cancel
</button>
```

---

### `--accent` / `--accent-foreground`
Interactive state এর জন্য। Hover background, selected row, active sidebar item।
সাধারণত `--secondary` এর মতোই কিন্তু purely interaction এর জন্য।

```tsx
<div className="hover:bg-accent hover:text-accent-foreground cursor-pointer p-2 rounded">
  Menu Item
</div>
```

---

### `--destructive`
Delete, danger, error। সবসময় **red family** থেকে নেওয়া হয়।

```tsx
<button className="bg-destructive text-destructive-foreground">Delete</button>
<p className="text-destructive text-sm">Invalid email address</p>
```

---

### `--success` / `--warning` / `--info`
Status badge, toast notification, alert এর জন্য।  
এই তিনটি shadcn/ui তে default নেই — manually যোগ করতে হয়।

```tsx
// Status Badge
<span className="bg-success/15 text-success text-xs font-bold px-2 py-1 rounded-full">
  VERIFIED
</span>
```
`/15` মানে 15% opacity — এটা Tailwind 4 এর নতুন syntax।

---

### `--border` / `--input` / `--ring`
- `--border`: সব divider, card edge, table border
- `--input`: form input এর border (sometimes slightly different from --border)
- `--ring`: keyboard focus ring — accessibility এর জন্য অত্যন্ত গুরুত্বপূর্ণ

```css
* { @apply border-border outline-ring/50; }
input { @apply border-input focus:ring-2 ring-ring; }
```

---

## 🌫️ Section 6: Gray Shades কীভাবে Manage করতে হয়?

### ❌ ভুল পদ্ধতি (hardcoded grays):
```tsx
<p className="text-gray-500">Subtitle</p>
<div className="bg-gray-100">Panel</div>
<span className="border-gray-200">Card</span>
```
Dark mode এ এগুলো কাজ করে না। `gray-500` light mode এ ঠিক আছে,
কিন্তু dark mode এ `gray-500` এর বদলে `gray-400` দরকার হয়।

### ✅ সঠিক পদ্ধতি (semantic tokens):
```tsx
<p className="text-muted-foreground">Subtitle</p>
<div className="bg-muted">Panel</div>
<span className="border-border">Card</span>
```

**Rule:** শুধুমাত্র illustration, decorative element, বা absolutely static জায়গায়
hardcoded gray ব্যবহার করো। বাকি সব জায়গায় semantic token।

---

## 🏗️ Section 7: Tailwind + CSS Variables — Professional Setup

### Step 1: `globals.css` তে `:root` এবং `.dark` define করো

```css
:root {
  /* Surface */
  --background: oklch(1 0 0);
  --foreground: oklch(0.145 0 0);
  --card: oklch(1 0 0);
  --card-foreground: oklch(0.145 0 0);
  --popover: oklch(1 0 0);
  --popover-foreground: oklch(0.145 0 0);
  --sidebar: oklch(0.985 0 0);
  --sidebar-foreground: oklch(0.145 0 0);

  /* Brand */
  --primary: #3b0014;
  --primary-foreground: #ffffff;
  --secondary: oklch(0.97 0 0);
  --secondary-foreground: oklch(0.205 0 0);
  --accent: oklch(0.97 0 0);
  --accent-foreground: oklch(0.205 0 0);

  /* Feedback */
  --destructive: oklch(0.577 0.245 27.325);
  --destructive-foreground: oklch(1 0 0);
  --success: oklch(0.527 0.154 150.069);   /* ← manually add */
  --success-foreground: oklch(1 0 0);
  --warning: oklch(0.769 0.188 70.08);
  --warning-foreground: oklch(0.205 0 0);

  /* UI Chrome */
  --border: oklch(0.922 0 0);
  --input: oklch(0.922 0 0);
  --ring: oklch(0.708 0 0);
  --muted: oklch(0.97 0 0);
  --muted-foreground: oklch(0.556 0 0);

  /* Radius */
  --radius: 0.625rem;
}

.dark {
  --background: oklch(0.145 0 0);
  --foreground: oklch(0.985 0 0);
  --card: oklch(0.205 0 0);
  --card-foreground: oklch(0.985 0 0);
  --popover: oklch(0.205 0 0);
  --popover-foreground: oklch(0.985 0 0);
  --sidebar: oklch(0.205 0 0);
  --sidebar-foreground: oklch(0.985 0 0);

  --primary: oklch(0.922 0 0);
  --primary-foreground: oklch(0.205 0 0);
  --secondary: oklch(0.269 0 0);
  --secondary-foreground: oklch(0.985 0 0);
  --accent: oklch(0.269 0 0);
  --accent-foreground: oklch(0.985 0 0);

  --destructive: oklch(0.704 0.191 22.216);
  --success: oklch(0.627 0.154 150.069);
  --warning: oklch(0.769 0.188 70.08);

  --border: oklch(1 0 0 / 10%);
  --input: oklch(1 0 0 / 15%);
  --ring: oklch(0.556 0 0);
  --muted: oklch(0.269 0 0);
  --muted-foreground: oklch(0.708 0 0);
}
```

### Step 2: Tailwind 4 `@theme inline` এ map করো

```css
@theme inline {
  --color-background:       var(--background);
  --color-foreground:       var(--foreground);
  --color-card:             var(--card);
  --color-card-foreground:  var(--card-foreground);
  --color-primary:          var(--primary);
  --color-primary-foreground: var(--primary-foreground);
  --color-secondary:        var(--secondary);
  --color-muted:            var(--muted);
  --color-muted-foreground: var(--muted-foreground);
  --color-border:           var(--border);
  --color-input:            var(--input);
  --color-ring:             var(--ring);
  --color-destructive:      var(--destructive);
  --color-success:          var(--success);
  --color-warning:          var(--warning);
  --color-accent:           var(--accent);
  --color-accent-foreground: var(--accent-foreground);
  --color-sidebar:          var(--sidebar);
  --color-sidebar-foreground: var(--sidebar-foreground);
  --radius-lg: var(--radius);
  --radius-md: calc(var(--radius) - 2px);
  --radius-sm: calc(var(--radius) - 4px);
}
```

এরপর Tailwind class এ সরাসরি ব্যবহার করা যাবে:
```tsx
bg-background       → var(--background)
text-foreground     → var(--foreground)
bg-primary          → var(--primary)
text-muted-foreground → var(--muted-foreground)
border-border       → var(--border)
bg-success          → var(--success)
```

---

## 🎯 Section 8: কেন Semantic > Hardcoded?

| | Hardcoded | Semantic |
|---|---|---|
| Dark mode | প্রতিটা component পরিবর্তন | শুধু `:root` এ change |
| Design system change | শত জায়গায় খোঁজা | একটি variable পরিবর্তন |
| Team consistency | কে কোন gray নিল বলা কঠিন | সবাই same token ব্যবহার করে |
| Readability | `bg-[#f5f1ed]` মানে কী? | `bg-muted` — instantly বোঝা যায় |
| Reusability | নতুন project এ copy হয় না | `:root` copy করলেই হয় |

---

## 📐 Section 9: Clean Naming Convention

```
naming pattern:  --{scope}-{role}

scope = কোথায় ব্যবহার (card, sidebar, primary, muted...)
role  = কী ধরনের (foreground = text, background implicit)

Examples:
  --card-foreground       (card এর text)
  --sidebar-primary       (sidebar এর active/brand item)
  --primary-foreground    (primary button এর text)
  --muted-foreground      (muted zone এর text)
```

### Quick Rule:
```
কোনো কিছুর background  → var(--{name})
সেই background এর text  → var(--{name}-foreground)
```

---

## 🏛️ Section 10: Full Color Architecture Visual

```
APPLICATION LAYER
├── Page
│   ├── bg: --background
│   └── text: --foreground
│
├── Card / Panel
│   ├── bg: --card
│   ├── text: --card-foreground
│   └── border: --border
│
├── Sidebar
│   ├── bg: --sidebar
│   ├── text: --sidebar-foreground
│   ├── active: --sidebar-primary
│   └── hover: --sidebar-accent
│
├── Buttons
│   ├── primary → --primary + --primary-foreground
│   ├── secondary → --secondary + --secondary-foreground
│   ├── ghost/hover → --accent + --accent-foreground
│   └── danger → --destructive + --destructive-foreground
│
├── Form
│   ├── border: --input
│   └── focus ring: --ring
│
├── Typography
│   ├── heading: --foreground
│   ├── body: --foreground
│   └── caption/hint: --muted-foreground
│
└── Status
    ├── success → --success
    ├── warning → --warning
    ├── error → --destructive
    └── info → --info
```

---

## 🌗 Section 11: Light/Dark Mode Enable করার সঠিক উপায় (Next.js)

### `next-themes` ব্যবহার করো:

```bash
npm install next-themes
```

```tsx
// app/providers.tsx
"use client";
import { ThemeProvider } from "next-themes";

export function Providers({ children }: { children: React.ReactNode }) {
  return (
    <ThemeProvider attribute="class" defaultTheme="system" enableSystem>
      {children}
    </ThemeProvider>
  );
}
```

```tsx
// app/layout.tsx
import { Providers } from "./providers";

export default function RootLayout({ children }) {
  return (
    <html lang="en" suppressHydrationWarning>
      <body>
        <Providers>{children}</Providers>
      </body>
    </html>
  );
}
```

`attribute="class"` মানে — dark mode এ `<html class="dark">` হবে,
তখন CSS এর `.dark { ... }` block activate হবে।

---

## 💡 Section 12: Opacity Trick (খুব কাজের)

Tailwind 4 এ CSS variable দিয়ে opacity use করা যায়:

```tsx
// 15% opacity background, full color text
<span className="bg-success/15 text-success">
  VERIFIED
</span>

// 10% opacity for subtle dividers
<div className="border border-border/50">...</div>

// hover state
<div className="hover:bg-accent/80">...</div>
```

এটা অত্যন্ত useful status badge, subtle highlight, overlay এর জন্য।

---

## ✅ Section 13: Final Reference Checklist

প্রতিটি নতুন project এ এই checklist follow করো:

```
□ globals.css এ :root সব token define করেছি
□ globals.css এ .dark সব token define করেছি
□ @theme inline এ Tailwind এ map করেছি
□ next-themes install ও setup করেছি
□ layout.tsx এ suppressHydrationWarning দিয়েছি
□ body তে bg-background text-foreground দিয়েছি
□ success, warning, info token manually add করেছি
□ কোনো component এ hardcoded color নেই
□ gray শুধু decorative/static জায়গায় ব্যবহার করেছি
□ border সব জায়গায় border-border class দিয়েছি
□ input focus এ ring-ring ব্যবহার করেছি
```

---

## 📌 Quick Reference Card (মুখস্থ রাখার জন্য)

```
bg-background           → page background
text-foreground         → main text
bg-card                 → card background
text-card-foreground    → card text
bg-primary              → brand button
text-primary-foreground → brand button text
bg-muted                → disabled / subtle bg
text-muted-foreground   → subtitle / caption
border-border           → all borders
bg-destructive          → danger / error
bg-success              → verified / done
bg-warning              → pending / caution
```

---

> **Final Note:** এই system একবার ঠিকমতো setup করলে,
> পুরো application এ `className="dark"` toggle করলেই সব color automatically পরিবর্তন হয়ে যাবে।
> কোনো component এ হাত দিতে হবে না। এটাই professional grade dark mode।

*— Design System Reference v1.0 | Next.js + Tailwind 4 + next-themes*