# K9 Behavioral Architect Design System — Project Rules

## 🃏 Card Components

### Colored Card Variant
When a card needs color identity, **never use a thick left or top border accent**.
These patterns are **NOT part of the K9 Behavioral Architect Design System**:

```css
/* ❌ FORBIDDEN */
border-left: 3px solid var(--red);
border-left: 3px solid var(--grn);
border-top:  2px solid var(--blu);
/* etc. */
```

Instead, use: **thin uniform 1px border** (same thickness as the default `.card` border)
with a **semi-transparent background overlay**:

```html
<!-- ✅ CORRECT: red-accented card -->
<div class="card" style="border-color:rgba(239,68,68,0.35);background:rgba(239,68,68,0.07);">
```

### Color Overlay Reference

| Color  | Token    | border-color                  | background                   |
|--------|----------|-------------------------------|------------------------------|
| Red    | `--red`  | `rgba(239, 68,  68,  0.35)`  | `rgba(239, 68,  68,  0.07)` |
| Green  | `--grn`  | `rgba( 16, 185, 129, 0.35)`  | `rgba( 16, 185, 129, 0.07)` |
| Amber  | `--amb`  | `rgba(245, 158, 11,  0.35)`  | `rgba(245, 158, 11,  0.07)` |
| Blue   | `--blu`  | `rgba( 59, 130, 246, 0.35)`  | `rgba( 59, 130, 246, 0.07)` |
| Purple | `--pur`  | `rgba(139,  92, 246, 0.35)`  | `rgba(139,  92, 246, 0.07)` |
| Teal   | `--tel`  | `rgba( 20, 184, 166, 0.35)`  | `rgba( 20, 184, 166, 0.07)` |

---

## 🌙 Theme

Always use **dark mode** as the default for new presentations and UI components
unless explicitly asked otherwise. Light mode support is secondary.

---

## 🔤 Navigation Labels

In the App UI Kit, the `kennels` navigation item and all related data keys and
labels have been renamed to `owners` (e.g. `OWN-XX` identifiers). Use `owners`
everywhere — never `kennels`.
