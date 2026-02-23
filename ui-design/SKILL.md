---
name: ui-design
description: Visual implementation skill — Pajamas-inspired design tokens, CSS component patterns, responsive layout, and accessibility markup. For behavioral UX principles (interaction patterns, copy, flows), see the ux-design skill.
---

# UI Design System — Visual Implementation

This skill provides design tokens, CSS patterns, component markup, and responsive layout rules. It implements the behavioral principles defined in the **ux-design** skill using a GitLab Pajamas-inspired visual system in vanilla CSS.

## When to Use This Skill

Use this skill when:
- Writing CSS or HTML for components
- Choosing colors, spacing, typography, or border-radius values
- Building responsive layouts
- Implementing ARIA attributes and screen reader markup
- Looking up component markup patterns (cards, buttons, forms, toasts)

For **interaction patterns, copy guidelines, and UX philosophy**, see the `ux-design` skill.

---

## Design Foundation: GitLab Pajamas

We follow GitLab Pajamas design principles (design.gitlab.com) but implement in **vanilla CSS** — keeping our projects framework-agnostic.

**What we take from Pajamas:**
- Design tokens (colors, spacing, typography)
- Component patterns (forms, buttons, cards)
- UX guidelines (accessibility, responsive design)

**What we don't use:**
- @gitlab/ui Vue components (we use vanilla HTML/CSS/JS)

**Reference links:**
- Design principles: https://design.gitlab.com/
- Color system: https://design.gitlab.com/product-foundations/colors
- Spacing: https://design.gitlab.com/product-foundations/spacing
- Components: https://design.gitlab.com/components/overview

---

## Design Tokens

### Colors

```css
:root {
  /* Background */
  --color-background: #fafafa;
  --color-background-subtle: #f0f0f0;

  /* Text — all meet WCAG AA (4.5:1) on #fafafa */
  --color-text: #1f2937;            /* 14.1:1 */
  --color-text-secondary: #4b5563;  /* 7.2:1  */
  --color-text-muted: #6b7280;      /* 4.6:1  */

  /* Primary (GitLab indigo) */
  --color-primary: #6366f1;
  --color-primary-hover: #4f46e5;

  /* Neutral */
  --color-border: #e5e7eb;
  --color-border-strong: #d1d5db;

  /* Semantic */
  --color-success: #22c55e;
  --color-success-bg: #dcfce7;
  --color-warning: #f59e0b;
  --color-warning-bg: #fef3c7;
  --color-danger: #ef4444;
  --color-danger-bg: #fee2e2;
  --color-info: #0ea5e9;
  --color-info-bg: #e0f2fe;
}
```

### Spacing Scale

```css
:root {
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-5: 24px;
  --space-6: 32px;
  --space-7: 48px;
  --space-8: 64px;
}
```

### Typography

```css
:root {
  /* Font family */
  --font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  --font-family-mono: 'SF Mono', Monaco, Consolas, 'Liberation Mono', monospace;

  /* Font sizes */
  --font-size-xs: 12px;
  --font-size-sm: 14px;
  --font-size-md: 16px;
  --font-size-lg: 18px;
  --font-size-xl: 20px;
  --font-size-2xl: 24px;
  --font-size-3xl: 30px;

  /* Line heights */
  --line-height-tight: 1.25;
  --line-height-normal: 1.5;
  --line-height-relaxed: 1.75;
}
```

### Border Radius

```css
:root {
  --radius-sm: 4px;
  --radius-md: 6px;
  --radius-lg: 8px;
  --radius-full: 9999px;
}
```

---

## Component Visual Patterns

### Card Layout

Cards use flex layout to push footer buttons to the bottom, regardless of content height.

```css
/* Card flex structure */
.card {
  display: flex;
  flex-direction: column;
}

.card-body {
  flex-grow: 1; /* pushes footer to bottom */
}
```

No borders between cards — use whitespace (gap) only.

### Button Colors

- **Primary**: `--color-primary` (indigo)
- **Secondary**: Gray outlined (`--color-border-strong`)
- **Danger**: `--color-danger` (red) — only for truly destructive actions, rare
- **No orange buttons**

### Section Header

When a section needs a named heading (see ux-design principle 7):

```css
/* Heading with whitespace only — NEVER add border-bottom */
.section-header {
  font-size: var(--font-size-xs);
  font-weight: 600;
  color: var(--color-text-muted);
  text-transform: uppercase;
  letter-spacing: 0.5px;
  margin-top: var(--space-4);
  margin-bottom: var(--space-2);
}
```

### Step Indicator Sizing

- Circle: 24x24px, font 13px, 600 weight
- Gap between steps: 32px (whitespace only, no connector lines)
- Active: dark circle (`--color-text`) with white text, bold label
- Inactive: subtle background (`--color-background-subtle`) with muted text

### Visual Audit Page Template

The audit page structure for rendering every component variant (see ux-design principle 9 for rules):

```html
<!-- Component variant -->
<div class="audit-section">
  <div class="audit-label">2. Book Card — s play</div>
  <div class="audit-desc">What it is and when it's used.</div>
  <div class="audit-where">Function: <code>renderBookCard(book, true)</code> · Where: Library</div>
  <!-- Exact production HTML using real app CSS -->
  <div class="book-list">...</div>
</div>

<!-- List context -->
<div class="audit-section">
  <div class="audit-label">A. Library — main list</div>
  <div class="audit-desc">How cards appear together in the library view.</div>
  <div class="book-list" style="border: 1px dashed var(--border);">
    <!-- 2 rows showing the card mix -->
  </div>
</div>
```

Rules: Links to the app's real `css/styles.css`. Uses relative CSS path. Disable interactive elements (`pointer-events: none`). List sections show 2 representative rows each.

---

## Input Width Guidelines

**Principle:** Input width should hint at expected content length. A postal code field shouldn't be full-width.

### Width Classes (3 sizes)

```css
/* IMPORTANT: Width on INPUT element, not label wrapper */
.input-xs .form-input { width: 100px; }   /* PSČ, CVV, codes */
.input-sm .form-input { width: 180px; }   /* dates, phone, IČO */
.input-md .form-input { width: 320px; }   /* names, emails */
```

### Rules

- Use `.input-xs` for: PSČ, CVV, verification codes, house numbers (Č.p.)
- Use `.input-sm` for: dates, phone numbers, IČO, DIČ, city names
- Use `.input-md` for: names, emails, street addresses
- **Full-width only for**: textareas, long descriptions

### Short Input Labels

For `.input-xs` fields, labels may be longer than the input. Keep labels on one line:

```css
.form-label-text-nowrap { white-space: nowrap; }
```

### Example: Address Form

```
┌─────────────────────────────────────────────────────┐
│ Ulice                      │ Č.p.     │ Město       │
│ [████████████████████████] │ [█████]  │ [█████████] │
│        .input-md           │ .input-xs│  .input-sm  │
└─────────────────────────────────────────────────────┘
```

### Implementation

```html
<div class="form-row">
  <label class="form-label input-md">
    <span class="form-label-text">Ulice</span>
    <input type="text" class="form-input" name="street">
  </label>
  <label class="form-label input-xs">
    <span class="form-label-text form-label-text-nowrap">Č.p.</span>
    <input type="text" class="form-input" name="house_number">
  </label>
  <label class="form-label input-sm">
    <span class="form-label-text">Město</span>
    <input type="text" class="form-input" name="city">
  </label>
</div>
```

```css
.form-row {
  display: flex;
  gap: var(--space-5);
  flex-wrap: wrap;
  align-items: flex-start;
}

/* Width on input, not label */
.input-xs .form-input { width: 100px; }
.input-sm .form-input { width: 180px; }
.input-md .form-input { width: 320px; }

/* Keep short labels on one line */
.form-label-text-nowrap { white-space: nowrap; }

/* Full-width on mobile */
@media (max-width: 576px) {
  .input-xs .form-input,
  .input-sm .form-input,
  .input-md .form-input {
    width: 100%;
  }
}
```

---

## Exception Pattern CSS

Visual implementations for patterns allowed by ux-design exceptions.

### Inline "or" Divider

Short centered divider for alternative input methods (e.g. paste URL **or** upload photo):

```css
.add-divider {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-3);
  margin: var(--space-5) 0;
  color: var(--color-text-muted);
  font-size: var(--font-size-sm);
}

.add-divider::before,
.add-divider::after {
  content: '';
  width: 60px;
  height: 1px;
  background: var(--color-border);
}
```

```html
<div class="add-divider"><span>nebo</span></div>
```

### Drop Zone

File upload areas with dashed border (functional pattern, not decoration):

```css
.drop-zone {
  border: 2px dashed var(--color-border-strong);
  border-radius: var(--radius-lg);
  padding: var(--space-7) var(--space-5);
  text-align: center;
  cursor: pointer;
}

.drop-zone:hover,
.drop-zone.drag-over {
  border-color: var(--color-primary);
  background: var(--color-info-bg);
}
```

### Filter Pills with Dual Meaning

Include vs. exclude pills need different active colors:

```css
.filter-pill.active { background: var(--color-primary); color: white; }
.filter-pill[data-exclude].active { background: var(--color-text); color: white; }
```

---

## Content Browsing CSS

Visual implementations for content browsing patterns (see ux-design Content Browsing UX for behavioral rules).

### Interactive Metadata (Meta Links)

```css
.meta-link {
  color: var(--color-text-secondary);
  cursor: pointer;
  transition: color 150ms ease;
}
.meta-link:hover,
.meta-link:active {
  color: var(--color-primary);
}
```

### Active Filters with Dismissible Chips

```html
<div class="active-filters">
  <span class="filter-chip">
    Autor: Douglas Adams
    <button aria-label="Zrušit filtr">×</button>
  </span>
</div>
```

```css
.active-filters {
  display: flex;
  gap: var(--space-2);
  padding: var(--space-2) var(--space-5);
  flex-wrap: wrap;
}
.filter-chip {
  display: flex;
  align-items: center;
  gap: var(--space-1);
  padding: var(--space-1) var(--space-3);
  background: rgba(99, 102, 241, 0.08);
  color: var(--color-primary);
  border-radius: 9999px;
  font-size: 13px;
  font-weight: 500;
}
.filter-chip button {
  background: none;
  border: none;
  color: inherit;
  font-size: 16px;
  cursor: pointer;
  padding: 0 0 0 4px;
  line-height: 1;
}
```

---

## Accessibility Implementation

### ARIA Attributes

```html
<!-- Buttons with icons -->
<button aria-label="Close">×</button>

<!-- Form errors -->
<input aria-invalid="true" aria-describedby="email-error">
<small id="email-error">Please enter a valid email</small>

<!-- Loading states -->
<button aria-busy="true">Loading...</button>

<!-- Toast notifications -->
<div role="status" aria-live="polite">Item archived. <button>Undo</button></div>
```

### Screen Reader Text

```css
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
```

---

## Responsive Design

### Breakpoints

```css
/* Mobile first approach */
@media (min-width: 576px) { /* Small */ }
@media (min-width: 768px) { /* Medium */ }
@media (min-width: 1024px) { /* Large */ }
@media (min-width: 1280px) { /* Extra large */ }
```

### Responsive Grid

```css
.card-grid {
  display: grid;
  gap: var(--space-4);
  grid-template-columns: 1fr;
}

@media (min-width: 576px) {
  .card-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .card-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}
```

### Touch Targets

Minimum touch target size: 44x44px on mobile.

---

## Component Library

See `components.md` for copy-paste ready HTML/CSS for:
- Buttons (primary, secondary, outline)
- Form inputs (text, email, password, textarea)
- Input width utilities
- Cards and Card grids
- Content cards (book cards, series cards)
- List views with actions
- Toast with undo
- Archive page pattern
- Empty states
- Step indicators
- Error messages
- Pills/Tags
- Loading states
- Navigation
- AI-assisted components
- Relative time / Time ago
- Link visibility
- Filter chip counts
- Multi-select OR filtering

## Examples

See `examples.md` for full page examples showing components in context.

---

*For behavioral UX principles (forgiving software, interaction patterns, copy guidelines, content browsing UX, lazy registration), see the `ux-design` skill at `~/.claude/skills/ux-design/`.*
