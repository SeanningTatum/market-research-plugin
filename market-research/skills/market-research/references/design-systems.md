# Design Systems Reference

This document contains the specifications for each available design system. The SKILL.md file contains the full Tailwind config, CSS, and Chart.js setup for the default **Newsprint** design. This file documents the alternative options.

## Table of Contents
1. [Newsprint (Default)](#newsprint) — fully specified in SKILL.md
2. [Clean Modern](#clean-modern)
3. [Corporate](#corporate)

---

## Newsprint

The Newsprint design is the default and is fully specified in SKILL.md Phase 2. Key characteristics:

- **Fonts:** Playfair Display (headlines), Lora (body), Inter (UI), JetBrains Mono (data)
- **Colors:** `newsprint: #F9F9F7`, `ink: #111111`, `muted: #E5E5E0`, `editorial: #CC0000`, `gain: #2E7D32`
- **Zero border-radius** on everything (`* { border-radius: 0 !important; }`)
- **Dot-grid background** with newsprint texture overlay
- **Border-as-separator** grids (`gap-0 border border-ink` with `border-r`/`border-b` on cells)
- **Hard offset shadow** on card hover (`box-shadow: 4px 4px 0px #111;`)
- **Drop caps** on opening paragraphs
- **Ornamental dividers** (`◇ ◇ ◇` or `◆ ◆ ◆`)
- **Inverted sections** (black bg, white text) for hero and highlights
- **Grayscale map** (`filter: grayscale(70%) contrast(1.05)`)

See SKILL.md for the complete Tailwind config, `<style>` block, and Chart.js defaults.

---

## Clean Modern

A minimal, contemporary design with generous whitespace, subtle shadows, and a blue accent.

### Tailwind Config
```html
<script>
tailwind.config = {
  theme: {
    extend: {
      fontFamily: {
        headline: ['Inter', 'system-ui', 'sans-serif'],
        body: ['Inter', 'system-ui', 'sans-serif'],
        ui: ['Inter', 'system-ui', 'sans-serif'],
        mono: ['JetBrains Mono', 'monospace'],
      },
      colors: {
        surface: '#FFFFFF',
        ink: '#1A1A2E',
        muted: '#E2E8F0',
        accent: '#2563EB',
        'accent-light': '#DBEAFE',
      }
    }
  }
}
</script>
```

### Fonts (Google Fonts)
```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
```

### Key Differences from Newsprint
- **Remove** `* { border-radius: 0 !important; }` — use `rounded-lg` (8px) on cards and containers
- **Remove** newsprint texture and dot-grid background — use plain white `bg-white`
- **Remove** drop caps, ornamental dividers, inverted sections
- **Cards:** Use `bg-white border border-muted rounded-lg shadow-sm hover:shadow-md` instead of `card-newsprint`
- **Tables:** Use `rounded-lg overflow-hidden` on table container, `bg-accent text-white` headers
- **Grids:** Use `gap-4` or `gap-6` instead of `gap-0` with borders
- **Map:** No grayscale filter, add `rounded-lg overflow-hidden` to container
- **Section headers:** `font-headline font-bold text-3xl` (smaller, no `font-black`)

### Chart.js Colors
```javascript
Chart.defaults.font.family = "'Inter', system-ui, sans-serif";
Chart.defaults.plugins.title.font = { family: "'Inter', system-ui, sans-serif", size: 16, weight: '700' };
// Use blue-based palette:
const PRIMARY = '#1A1A2E';
const ACCENT  = '#2563EB';
const N600    = '#475569';
const N500    = '#64748B';
const N400    = '#94A3B8';
const N200    = '#E2E8F0';
```

---

## Corporate

A professional, formal design suited for executive reports and institutional presentations.

### Tailwind Config
```html
<script>
tailwind.config = {
  theme: {
    extend: {
      fontFamily: {
        headline: ['Source Serif Pro', 'Georgia', 'serif'],
        body: ['Inter', 'system-ui', 'sans-serif'],
        ui: ['Inter', 'system-ui', 'sans-serif'],
        mono: ['JetBrains Mono', 'monospace'],
      },
      colors: {
        surface: '#FAFAFA',
        ink: '#1E3A5F',
        muted: '#D1D5DB',
        accent: '#C9A84C',
        'accent-dark': '#A88B3D',
      }
    }
  }
}
</script>
```

### Fonts (Google Fonts)
```html
<link href="https://fonts.googleapis.com/css2?family=Source+Serif+Pro:wght@400;600;700&family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
```

### Key Differences from Newsprint
- **Remove** `* { border-radius: 0 !important; }` — use minimal `rounded` (4px) on cards
- **Remove** newsprint texture — use plain `bg-surface` (#FAFAFA)
- **Remove** drop caps, ornamental dividers
- **Cards:** Use `bg-white border border-muted rounded shadow-sm` with navy accent borders
- **Tables:** Navy header (`bg-ink text-white`), gold highlights on top values (`text-accent font-bold`)
- **Grids:** Can use `gap-4` with individual card borders, or `gap-0` with border separators
- **Map:** Slight desaturation (`filter: saturate(0.7)`), navy-styled popups
- **Inverted sections:** Navy background (`bg-ink`) instead of pure black
- **Section headers:** `Source Serif Pro` with gold underline accent

### Chart.js Colors
```javascript
Chart.defaults.font.family = "'Inter', system-ui, sans-serif";
Chart.defaults.plugins.title.font = { family: "'Source Serif Pro', Georgia, serif", size: 16, weight: '700' };
// Use navy/gold palette:
const PRIMARY = '#1E3A5F';
const ACCENT  = '#C9A84C';
const N600    = '#4B5563';
const N500    = '#6B7280';
const N400    = '#9CA3AF';
const N200    = '#E5E7EB';
```
