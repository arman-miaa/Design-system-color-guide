
# 🎨 Frontend Design System — Professional Reference

> **Senior Frontend Architect's Complete Design System Notes**  
> Framework-agnostic principles for consistent, maintainable & scalable UI

---

## 📚 Documentation

### 🎨 [Semantic Color System](docs/COLOR_SYSTEM.md)
Professional color architecture with automatic light/dark mode.
- 5 categories of color tokens (Surface, Text, Brand, Feedback, UI Chrome)
- CSS custom properties with Tailwind 4 integration
- `next-themes` dark mode setup
- Hardcoded vs Semantic: real examples

### 📐 [Typography System](docs/TYPOGRAPHY_SYSTEM.md)
Complete font size, weight & hierarchy guide.
- 10-level typography scale (10px → 40px)
- Font weight decision guide (400/500/600/700)
- Line height & letter spacing rules
- Usage map: hero → heading → body → caption → label

### 📱 [Responsive Breakpoint System](docs/RESPONSIVE_BREAKPOINTS.md)
Device breakpoint architecture & layout patterns.
- Mobile-first strategy with decision flowchart
- 7 common responsive patterns (Grid, Sidebar, Modal, etc.)
- Container max-width guide
- Figma ↔ Developer handoff template

---

## 🎯 Why This Matters

| Problem | Solution |
|---------|----------|
| Inconsistent colors across pages | Semantic tokens — one source of truth |
| Dark mode requires manual fixes | Auto-switching via CSS variables |
| Random font sizes everywhere | Defined typography scale |
| Broken layouts on tablets | Standardized breakpoint system |
| Designer-Developer mismatch | Shared vocabulary & handoff guide |

---

## 🚀 How to Use

```
১. docs/ ফোল্ডারটি আপনার প্রজেক্টে copy করুন
২. COLOR_SYSTEM.md → globals.css setup
৩. TYPOGRAPHY_SYSTEM.md → Tailwind theme extend
৪. RESPONSIVE_BREAKPOINTS.md → Layout implementation
```

---

## ✅ Core Principles

```
✅ Semantic naming over hardcoded values
✅ Mobile-first responsive design
✅ Consistent typography hierarchy  
✅ Automatic dark mode (system preference)
✅ Accessibility (WCAG AA+) compliant
✅ Zero friction Figma ↔ Developer handoff
```

---

## 📁 Recommended Folder Structure

```
project/
├── docs/                          ← Design System Docs
│   ├── COLOR_SYSTEM.md
│   ├── TYPOGRAPHY_SYSTEM.md
│   └── RESPONSIVE_BREAKPOINTS.md
├── app/
│   └── globals.css                ← CSS Variables & Theme
└── components/
    └── ui/                        ← Reusable UI Components
```

---

## 🔗 Reference Links

- [Tailwind CSS](https://tailwindcss.com/docs)
- [next-themes](https://github.com/pacocoursey/next-themes)
- [shadcn/ui](https://ui.shadcn.com)
- [WCAG Guidelines](https://www.w3.org/WAI/standards-guidelines/wcag/)
- [oklch Color Picker](https://oklch.com)

---

> **Author:** Senior Frontend Architect  
> **Version:** 1.0  
> **Type:** Framework-Agnostic Design System Reference

```

---

