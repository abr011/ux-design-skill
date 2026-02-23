# Component Library

Copy-paste ready HTML/CSS components using GitLab Pajamas design tokens and forgiving software patterns.

---

## Base Setup

Include these design tokens and base styles in every project:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title</title>
  <style>
    /* Design Tokens */
    :root {
      /* Background */
      --color-background: #fafafa;
      --color-background-subtle: #f0f0f0;

      /* Text */
      --color-text: #1f2937;
      --color-text-secondary: #6b7280;
      --color-text-muted: #9ca3af;

      /* Primary */
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

      /* Spacing */
      --space-1: 4px;
      --space-2: 8px;
      --space-3: 12px;
      --space-4: 16px;
      --space-5: 24px;
      --space-6: 32px;
      --space-7: 48px;
      --space-8: 64px;

      /* Typography */
      --font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
      --font-size-sm: 14px;
      --font-size-md: 16px;
      --line-height-normal: 1.5;

      /* Border Radius */
      --radius-sm: 4px;
      --radius-md: 6px;
      --radius-lg: 8px;
      --radius-full: 9999px;
    }

    /* Base Reset */
    *, *::before, *::after {
      box-sizing: border-box;
    }

    body {
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      line-height: var(--line-height-normal);
      color: var(--color-text);
      background: var(--color-background);
      margin: 0;
      padding: 0;
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: var(--space-5);
    }
  </style>
</head>
<body>
  <main class="container">
    <!-- Your content here -->
  </main>
</body>
</html>
```

---

## Buttons

### Primary Button

```html
<button class="btn btn-primary">Submit</button>
```

```css
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: var(--space-2) var(--space-4);
  font-family: var(--font-family);
  font-size: var(--font-size-md);
  font-weight: 500;
  line-height: 1.5;
  border-radius: var(--radius-md);
  cursor: pointer;
  transition: background 0.2s, border-color 0.2s;
  border: 1px solid transparent;
}

.btn-primary {
  background: var(--color-primary);
  color: white;
  border-color: var(--color-primary);
}

.btn-primary:hover {
  background: var(--color-primary-hover);
  border-color: var(--color-primary-hover);
}
```

### Secondary Button

```html
<button class="btn btn-secondary">Cancel</button>
```

```css
.btn-secondary {
  background: white;
  color: var(--color-text);
  border-color: var(--color-border-strong);
}

.btn-secondary:hover {
  background: var(--color-background-subtle);
}
```

### Outline Button

```html
<button class="btn btn-outline">Learn More</button>
```

```css
.btn-outline {
  background: transparent;
  color: var(--color-primary);
  border-color: var(--color-primary);
}

.btn-outline:hover {
  background: var(--color-primary);
  color: white;
}
```

### Danger Button

```html
<button class="btn btn-danger">Delete Forever</button>
```

```css
.btn-danger {
  background: var(--color-danger);
  color: white;
  border-color: var(--color-danger);
}

.btn-danger:hover {
  background: #dc2626;
}
```

### Disabled Button

```html
<button class="btn btn-primary" disabled>Disabled</button>
```

```css
.btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
```

### Button Group

```html
<div class="btn-group">
  <button class="btn btn-secondary">Cancel</button>
  <button class="btn btn-primary">Save</button>
</div>
```

```css
.btn-group {
  display: flex;
  gap: var(--space-2);
}
```

---

## Form Inputs

### Base Input Styles

```css
.form-label {
  display: block;
  margin-bottom: var(--space-4);
}

.form-label-text {
  display: block;
  font-size: var(--font-size-sm);
  font-weight: 500;
  color: var(--color-text);
  margin-bottom: var(--space-1);
}

.form-input {
  display: block;
  width: 100%;
  padding: var(--space-2) var(--space-3);
  font-family: var(--font-family);
  font-size: var(--font-size-md);
  line-height: 1.5;
  color: var(--color-text);
  background: white;
  border: 1px solid var(--color-border-strong);
  border-radius: var(--radius-md);
  transition: border-color 0.2s, box-shadow 0.2s;
}

.form-input:focus {
  outline: none;
  border-color: var(--color-primary);
  box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.15);
}

.form-input::placeholder {
  color: var(--color-text-muted);
}

.form-hint {
  display: block;
  font-size: var(--font-size-sm);
  color: var(--color-text-secondary);
  margin-top: var(--space-1);
}
```

### Text Input

```html
<label class="form-label">
  <span class="form-label-text">Full Name</span>
  <input type="text" class="form-input" name="name" placeholder="John Smith">
</label>
```

### Input with Error

```html
<label class="form-label">
  <span class="form-label-text">Email</span>
  <input type="email" class="form-input form-input-error" name="email" value="invalid-email" aria-invalid="true" aria-describedby="email-error">
  <small id="email-error" class="form-error">Please check the @ symbol and domain (e.g., name@example.com)</small>
</label>
```

```css
.form-input-error {
  border-color: var(--color-danger);
}

.form-input-error:focus {
  border-color: var(--color-danger);
  box-shadow: 0 0 0 3px rgba(239, 68, 68, 0.15);
}

.form-error {
  display: block;
  font-size: var(--font-size-sm);
  color: var(--color-danger);
  margin-top: var(--space-1);
}
```

### Input with Helper Text

```html
<label class="form-label">
  <span class="form-label-text">Password</span>
  <input type="password" class="form-input" name="password" placeholder="Your password">
  <small class="form-hint">At least 8 characters</small>
</label>
```

### Textarea

```html
<label class="form-label">
  <span class="form-label-text">Message</span>
  <textarea class="form-input" name="message" placeholder="Your message..." rows="4"></textarea>
</label>
```

---

## Input Width Utilities

**Principle:** Input width should hint at expected content length.

### Width Classes

**IMPORTANT:** Width is set on the `.form-input` element, not the label wrapper.

```html
<!-- PSČ, CVV - 5-6 chars -->
<label class="form-label input-xs">
  <span class="form-label-text form-label-text-nowrap">PSČ</span>
  <input type="text" class="form-input" name="zip" inputmode="numeric">
</label>

<!-- Date, phone, IČO - 10-12 chars -->
<label class="form-label input-sm">
  <span class="form-label-text">Datum narození</span>
  <input type="text" class="form-input" name="birthdate" placeholder="01.01.1990">
</label>

<!-- Name, email, address - ~30 chars -->
<label class="form-label input-md">
  <span class="form-label-text">Jméno</span>
  <input type="text" class="form-input" name="name">
</label>
```

```css
/* Input Width Utilities - width on INPUT, not label */
.input-xs .form-input { width: 100px; }   /* PSČ, CVV, codes */
.input-sm .form-input { width: 180px; }   /* dates, phone, IČO */
.input-md .form-input { width: 320px; }   /* names, emails */

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

### Form Row (Inline Fields)

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
```

### Width Reference Table

| Class | Width | Use For |
|-------|-------|---------|
| `.input-xs` | 100px | PSČ, CVV, verification codes, house numbers |
| `.input-sm` | 180px | dates, phone numbers, IČO, DIČ, city names |
| `.input-md` | 320px | names, emails, street addresses |
| (none) | 100% | textareas, long descriptions |

---

## Selection Controls (Avoid Dropdowns)

**Rule: < 5 options = Use radios or pills, not dropdown**

### Selectable Pills (for 2-4 options)

```html
<fieldset class="form-fieldset">
  <legend class="form-legend">Payment method</legend>
  <div class="selectable-pills">
    <label class="selectable-pill">
      <input type="radio" name="payment" value="card" checked>
      <span>Card</span>
    </label>
    <label class="selectable-pill">
      <input type="radio" name="payment" value="bank">
      <span>Bank Transfer</span>
    </label>
    <label class="selectable-pill">
      <input type="radio" name="payment" value="cash">
      <span>Cash</span>
    </label>
  </div>
</fieldset>
```

```css
.form-fieldset {
  border: none;
  padding: 0;
  margin: 0 0 var(--space-4) 0;
}

.form-legend {
  font-size: var(--font-size-sm);
  font-weight: 500;
  color: var(--color-text);
  margin-bottom: var(--space-2);
}

.selectable-pills {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-2);
}

.selectable-pill {
  display: flex;
  align-items: center;
  margin: 0;
  cursor: pointer;
}

.selectable-pill input[type="radio"] {
  display: none;
}

.selectable-pill span {
  padding: var(--space-2) var(--space-4);
  border: 1px solid var(--color-border-strong);
  border-radius: var(--radius-full);
  font-size: var(--font-size-sm);
  transition: all 0.2s;
}

.selectable-pill input:checked + span {
  background: var(--color-primary);
  color: white;
  border-color: var(--color-primary);
}

.selectable-pill:hover span {
  border-color: var(--color-primary);
}
```

### Radio Buttons (for 2-4 options with descriptions)

```html
<fieldset class="form-fieldset">
  <legend class="form-legend">Invoice frequency</legend>
  <div class="radio-group">
    <label class="radio-label">
      <input type="radio" name="frequency" value="monthly" checked>
      <span>Monthly</span>
    </label>
    <label class="radio-label">
      <input type="radio" name="frequency" value="quarterly">
      <span>Quarterly</span>
    </label>
    <label class="radio-label">
      <input type="radio" name="frequency" value="yearly">
      <span>Yearly</span>
    </label>
  </div>
</fieldset>
```

```css
.radio-group {
  display: flex;
  flex-direction: column;
  gap: var(--space-2);
}

.radio-label {
  display: flex;
  align-items: center;
  gap: var(--space-2);
  cursor: pointer;
}

.radio-label input[type="radio"] {
  width: 18px;
  height: 18px;
  accent-color: var(--color-primary);
}
```

### Rich Dropdown (for 5+ options)

When dropdown is necessary, show composed information to help users choose.

```html
<label class="form-label">
  <span class="form-label-text">Company</span>
  <div class="rich-select">
    <button type="button" class="rich-select-trigger" aria-expanded="false">
      <span class="rich-select-placeholder">Select company...</span>
    </button>
    <ul class="rich-select-options" role="listbox">
      <li role="option" data-value="acme">
        <strong>Acme Corp</strong>
        <small>ID: 12345 · Prague, Czech Republic</small>
      </li>
      <li role="option" data-value="techstart">
        <strong>TechStart s.r.o.</strong>
        <small>ID: 67890 · Brno, Czech Republic</small>
      </li>
      <li role="option" data-value="global">
        <strong>Global Industries</strong>
        <small>ID: 11111 · Berlin, Germany</small>
      </li>
    </ul>
    <input type="hidden" name="company" value="">
  </div>
</label>
```

```css
.rich-select {
  position: relative;
}

.rich-select-trigger {
  width: 100%;
  text-align: left;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  padding: var(--space-2) var(--space-3);
  background: white;
  border: 1px solid var(--color-border-strong);
  border-radius: var(--radius-md);
  cursor: pointer;
  font-family: var(--font-family);
  font-size: var(--font-size-md);
}

.rich-select-trigger::after {
  content: "▼";
  position: absolute;
  right: var(--space-3);
  top: 50%;
  transform: translateY(-50%);
  font-size: 12px;
  color: var(--color-text-muted);
}

.rich-select-placeholder {
  color: var(--color-text-muted);
}

.rich-select-value strong {
  display: block;
}

.rich-select-value small {
  color: var(--color-text-secondary);
}

.rich-select-options {
  display: none;
  position: absolute;
  top: 100%;
  left: 0;
  right: 0;
  background: white;
  border: 1px solid var(--color-border);
  border-radius: var(--radius-md);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  list-style: none;
  padding: 0;
  margin: var(--space-1) 0 0 0;
  max-height: 300px;
  overflow-y: auto;
  z-index: 100;
}

.rich-select.open .rich-select-options {
  display: block;
}

.rich-select-options li {
  padding: var(--space-3) var(--space-4);
  cursor: pointer;
  border-bottom: 1px solid var(--color-border);
}

.rich-select-options li:last-child {
  border-bottom: none;
}

.rich-select-options li:hover {
  background: var(--color-background-subtle);
}

.rich-select-options li strong {
  display: block;
  margin-bottom: var(--space-1);
}

.rich-select-options li small {
  color: var(--color-text-secondary);
}
```

```javascript
document.querySelectorAll('.rich-select').forEach(select => {
  const trigger = select.querySelector('.rich-select-trigger');
  const options = select.querySelector('.rich-select-options');
  const hidden = select.querySelector('input[type="hidden"]');

  trigger.addEventListener('click', () => {
    select.classList.toggle('open');
    trigger.setAttribute('aria-expanded', select.classList.contains('open'));
  });

  options.querySelectorAll('li').forEach(option => {
    option.addEventListener('click', () => {
      const value = option.dataset.value;
      const name = option.querySelector('strong').textContent;
      const detail = option.querySelector('small').textContent;

      hidden.value = value;
      trigger.innerHTML = `
        <span class="rich-select-value">
          <strong>${name}</strong>
          <small>${detail}</small>
        </span>
      `;
      select.classList.remove('open');
    });
  });

  document.addEventListener('click', (e) => {
    if (!select.contains(e.target)) {
      select.classList.remove('open');
    }
  });
});
```

### Simple Select (only when absolutely necessary)

```html
<label class="form-label">
  <span class="form-label-text">Country</span>
  <select class="form-input" name="country">
    <option value="">Select country...</option>
    <option value="us">United States</option>
    <option value="uk">United Kingdom</option>
    <option value="de">Germany</option>
  </select>
</label>
```

### Checkbox

```html
<label class="checkbox-label">
  <input type="checkbox" name="terms">
  <span>I agree to terms and conditions</span>
</label>
```

```css
.checkbox-label {
  display: flex;
  align-items: center;
  gap: var(--space-2);
  cursor: pointer;
}

.checkbox-label input[type="checkbox"] {
  width: 18px;
  height: 18px;
  accent-color: var(--color-primary);
}
```

---

## Cards

**Important:** Cards use flex layout to push footer buttons to the bottom, regardless of content height. No borders between sections - whitespace only.

### Basic Card

```html
<article class="card">
  <header class="card-header">Card Title</header>
  <div class="card-body">
    <p>Card content goes here. Keep it brief and focused.</p>
  </div>
</article>
```

```css
.card {
  display: flex;
  flex-direction: column;
  background: white;
  border: 1px solid var(--color-border);
  border-radius: var(--radius-lg);
  padding: var(--space-5);
}

.card-header {
  font-weight: 600;
  font-size: var(--font-size-md);
  margin-bottom: var(--space-3);
}

.card-body {
  flex-grow: 1;
  color: var(--color-text-secondary);
}

.card-body p {
  margin: 0;
}
```

### Card with Footer Actions

Footer buttons always at bottom, regardless of content height. No border-top - whitespace separation only.

```html
<article class="card">
  <header class="card-header">Project Name</header>
  <div class="card-body">
    <p>Project description and key information.</p>
  </div>
  <footer class="card-footer">
    <button class="btn btn-outline">View</button>
    <button class="btn btn-secondary" onclick="archiveItem(this)">Archive</button>
  </footer>
</article>
```

```css
/* Footer at bottom due to flex-grow on card-body. No border-top. */
.card-footer {
  display: flex;
  gap: var(--space-2);
  justify-content: flex-end;
  margin-top: var(--space-4);
  padding-top: var(--space-4);
}

### Clickable Card

```html
<article class="card card-clickable" onclick="location.href='#'">
  <header class="card-header">Clickable Card</header>
  <p class="card-body">Click anywhere on this card to navigate.</p>
</article>
```

```css
.card-clickable {
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;
}

.card-clickable:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}
```

### Card Grid

```html
<div class="card-grid">
  <article class="card">...</article>
  <article class="card">...</article>
  <article class="card">...</article>
</div>
```

```css
.card-grid {
  display: grid;
  gap: var(--space-4);
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
}
```

---

## Content Cards (Audiobooks / Media)

Patterns for browsing content with rich metadata: cover image, title, author, series position, genre tags, progress. These patterns apply to any media browsing app (audiobooks, podcasts, recipes, etc.).

### Book Card — Standard

The primary content card. Shows cover, title, author/narrator, series position (if applicable), genre tags, and duration or progress.

```html
<article class="book-card" data-id="abc123">
  <div class="book-card-cover">
    <img src="cover.jpg" alt="" loading="lazy">
  </div>
  <div class="book-card-info">
    <div class="book-card-title">Propast času</div>
    <div class="book-card-meta">Roman Bureš · Jiří Schwarz</div>
    <div class="book-card-series">Díl 1 z 3 — Propast času</div>
    <div class="book-card-tags">
      <span class="tag">sci-fi</span>
      <span class="tag">alternativní historie</span>
    </div>
    <div class="book-card-duration">12:34</div>
  </div>
</article>
```

```css
.book-card {
  display: flex;
  gap: var(--space-3);
  padding: var(--space-3) 0;
  cursor: pointer;
}

.book-card-cover {
  flex-shrink: 0;
  width: 80px;
  height: 80px;
  border-radius: var(--radius-sm);
  overflow: hidden;
}

.book-card-cover img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.book-card-info {
  flex: 1;
  min-width: 0; /* prevent text overflow */
}

.book-card-title {
  font-size: 15px;
  font-weight: 600;
  color: var(--color-text);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.book-card-meta {
  font-size: 13px;
  color: var(--color-text-secondary);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.book-card-series {
  font-size: 12px;
  color: var(--color-primary);
  margin-top: 2px;
}

.book-card-tags {
  display: flex;
  gap: var(--space-1);
  margin-top: var(--space-1);
  flex-wrap: wrap;
}

.book-card-tags .tag {
  font-size: 11px;
  padding: 1px 6px;
  background: var(--color-background-subtle);
  border-radius: var(--radius-full);
  color: var(--color-text-secondary);
}

.book-card-duration {
  font-size: 12px;
  color: var(--color-text-muted);
  margin-top: 2px;
}
```

**Variants:**
- **With play button**: Add a play icon overlay on the cover. Used in library lists.
- **With progress**: Replace duration with a progress bar + percentage. Used for in-progress books.
- **Compact (player bar)**: 64px cover, single-line metadata. Used in the player view header.
- **Mini (now-playing bar)**: 40px cover, title only + play/pause button. Used in sticky bottom bar.

### Series Card — Collapsed

Groups multiple books in the same series under one card. Shows the first book's cover, series name, book count, AI-generated series description, and reading status.

```html
<article class="series-card" data-series="Propast času">
  <div class="series-card-cover">
    <img src="cover-book1.jpg" alt="" loading="lazy">
    <span class="series-badge">Série</span>
  </div>
  <div class="series-card-info">
    <div class="series-card-title">Propast času</div>
    <div class="series-card-meta">Roman Bureš · 3 knihy</div>
    <div class="series-card-desc">
      Jedné noci se celý svět změnil. Lidské dějiny se roztříštily a střípky
      civilizací od pravěku až po budoucnost se složily do chaotické koláže.
    </div>
    <div class="series-card-status">Rozposloucháno · Díl 1</div>
  </div>
</article>
```

```css
.series-card {
  display: flex;
  gap: var(--space-3);
  padding: var(--space-3) 0;
  cursor: pointer;
}

.series-card-cover {
  position: relative;
  flex-shrink: 0;
  width: 80px;
  height: 80px;
  border-radius: var(--radius-sm);
  overflow: hidden;
}

.series-badge {
  position: absolute;
  top: 4px;
  left: 4px;
  background: rgba(0, 0, 0, 0.7);
  color: white;
  font-size: 10px;
  font-weight: 600;
  padding: 1px 5px;
  border-radius: var(--radius-sm);
  text-transform: uppercase;
}

.series-card-info {
  flex: 1;
  min-width: 0;
}

.series-card-title {
  font-size: 15px;
  font-weight: 600;
}

.series-card-meta {
  font-size: 13px;
  color: var(--color-text-secondary);
}

.series-card-desc {
  font-size: 13px;
  color: var(--color-text-secondary);
  margin-top: var(--space-1);
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.series-card-status {
  font-size: 12px;
  color: var(--color-primary);
  margin-top: 2px;
}
```

**Key design decisions:**
- Series description comes from AI (Gemini) or `SERIES_DESCRIPTIONS` manual dict — NOT from Audioteka (their descriptions are per-book marketing copy, not series summaries)
- "Série" badge on cover distinguishes from regular book cards at a glance
- Book count shown inline in meta (not as a separate badge)
- Reading status shows which part the user is on

### Series Card — Expanded

When a series card is tapped, it expands to show all books in the series with individual play buttons.

```html
<article class="series-card expanded">
  <div class="series-card-header">
    <div class="series-card-cover">
      <img src="cover-book1.jpg" alt="" loading="lazy">
    </div>
    <div class="series-card-info">
      <div class="series-card-title">Propast času</div>
      <div class="series-card-meta">Roman Bureš · 3 knihy</div>
      <div class="series-card-desc">...</div>
    </div>
  </div>
  <ul class="series-book-list">
    <li class="series-book-item">
      <span class="series-part">1</span>
      <span class="series-book-title">Propast času</span>
      <span class="series-book-status">35%</span>
      <button class="series-play-btn" aria-label="Přehrát">▶</button>
    </li>
    <li class="series-book-item">
      <span class="series-part">2</span>
      <span class="series-book-title">Císařovna</span>
      <span class="series-book-status"></span>
      <button class="series-play-btn" aria-label="Přehrát">▶</button>
    </li>
  </ul>
</article>
```

**Rules:**
- Expanded state shows inline book list (no navigation away from library)
- Each book has its own play button and progress indicator
- Part numbers are always 1-based (never 0)
- Player view shows only individual book cards with series info — never series cards

---

## List View

For detailed/searchable data display. Alternative to tables.

### Basic List

```html
<ul class="list-view">
  <li class="list-item">
    <div class="list-item-content">
      <strong>Item Name</strong>
      <small>Description or metadata</small>
    </div>
    <div class="list-item-actions">
      <button class="btn btn-outline">Edit</button>
      <button class="btn btn-secondary" onclick="archiveItem(this)">Archive</button>
    </div>
  </li>
  <li class="list-item">
    <div class="list-item-content">
      <strong>Another Item</strong>
      <small>More details here</small>
    </div>
    <div class="list-item-actions">
      <button class="btn btn-outline">Edit</button>
      <button class="btn btn-secondary" onclick="archiveItem(this)">Archive</button>
    </div>
  </li>
</ul>
```

```css
.list-view {
  list-style: none;
  padding: 0;
  margin: 0;
  background: white;
  border: 1px solid var(--color-border);
  border-radius: var(--radius-lg);
}

.list-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: var(--space-4);
  border-bottom: 1px solid var(--color-border);
}

.list-item:last-child {
  border-bottom: none;
}

.list-item-content {
  display: flex;
  flex-direction: column;
  gap: var(--space-1);
}

.list-item-content strong {
  font-weight: 600;
}

.list-item-content small {
  color: var(--color-text-secondary);
}

.list-item-actions {
  display: flex;
  gap: var(--space-2);
}
```

### List with Status

```html
<ul class="list-view">
  <li class="list-item">
    <div class="list-item-content">
      <strong>John Smith</strong>
      <small>john@example.com</small>
    </div>
    <span class="badge badge-success">Active</span>
    <div class="list-item-actions">
      <button class="btn btn-outline">Edit</button>
    </div>
  </li>
</ul>
```

---

## Toast with Undo (Forgiving Pattern)

The core component for forgiving software. Shows after any destructive action.

### Toast Container

```html
<div class="toast-container" aria-live="polite">
  <!-- Toasts are inserted here by JavaScript -->
</div>
```

```css
.toast-container {
  position: fixed;
  bottom: var(--space-4);
  right: var(--space-4);
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
  z-index: 1000;
}
```

### Toast with Undo Button

```html
<div class="toast" role="status">
  <span class="toast-message">Item archived.</span>
  <button class="toast-undo" onclick="undoArchive()">Undo</button>
  <div class="toast-timer"></div>
</div>
```

```css
.toast {
  display: flex;
  align-items: center;
  gap: var(--space-4);
  padding: var(--space-4) var(--space-5);
  background: white;
  border-radius: var(--radius-lg);
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.15);
  min-width: 280px;
  max-width: 400px;
  animation: slideIn 0.3s ease;
  position: relative;
  overflow: hidden;
}

@keyframes slideIn {
  from {
    transform: translateX(100%);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

.toast-message {
  flex: 1;
  font-size: var(--font-size-md);
}

.toast-undo {
  background: none;
  border: none;
  color: var(--color-primary);
  font-weight: 600;
  cursor: pointer;
  padding: var(--space-1) var(--space-2);
  margin: 0;
  font-size: var(--font-size-md);
}

.toast-undo:hover {
  text-decoration: underline;
}

.toast-timer {
  position: absolute;
  bottom: 0;
  left: 0;
  height: 3px;
  background: var(--color-primary);
  animation: timer 5s linear forwards;
}

@keyframes timer {
  from { width: 100%; }
  to { width: 0%; }
}

.toast.hiding {
  animation: slideOut 0.3s ease forwards;
}

@keyframes slideOut {
  to {
    transform: translateX(100%);
    opacity: 0;
  }
}
```

### Toast Action & Dismiss Spacing

When a toast has both an action button (e.g. "Undo", "Rewind") and a dismiss button (×), ensure sufficient spacing to prevent accidental taps on the wrong target:

- **Dismiss button**: minimum 44×44px touch target (`min-width: 44px; min-height: 44px; display: flex; align-items: center; justify-content: center`)
- **Separation**: add `margin-left: var(--space-2)` (8px) on the dismiss button to visually separate it from the action button
- **Never** rely on gap alone — the dismiss × is visually small, so its tap area must extend beyond the visible glyph

```css
.toast-dismiss {
  color: var(--color-text-muted);
  font-size: 18px;
  min-width: 44px;
  min-height: 44px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-left: var(--space-2);
  line-height: 1;
  background: none;
  border: none;
  cursor: pointer;
}
```

### Toast JavaScript

```javascript
let lastArchivedItem = null;
let toastTimeout = null;

function showToast(message, undoCallback) {
  const container = document.querySelector('.toast-container');

  const existingToast = container.querySelector('.toast');
  if (existingToast) {
    existingToast.remove();
    clearTimeout(toastTimeout);
  }

  const toast = document.createElement('div');
  toast.className = 'toast';
  toast.setAttribute('role', 'status');
  toast.innerHTML = `
    <span class="toast-message">${message}</span>
    <button class="toast-undo">Undo</button>
    <div class="toast-timer"></div>
  `;

  container.appendChild(toast);

  const undoBtn = toast.querySelector('.toast-undo');
  undoBtn.addEventListener('click', () => {
    if (undoCallback) undoCallback();
    removeToast(toast);
  });

  toastTimeout = setTimeout(() => {
    removeToast(toast);
    lastArchivedItem = null;
  }, 5000);
}

function removeToast(toast) {
  toast.classList.add('hiding');
  setTimeout(() => toast.remove(), 300);
  clearTimeout(toastTimeout);
}

function archiveItem(button) {
  const item = button.closest('article') || button.closest('li');
  const itemName = item.querySelector('.card-header, strong')?.textContent || 'Item';

  lastArchivedItem = {
    element: item,
    parent: item.parentNode,
    nextSibling: item.nextSibling
  };

  item.style.display = 'none';

  showToast(`${itemName} archived.`, () => {
    if (lastArchivedItem) {
      lastArchivedItem.element.style.display = '';
      lastArchivedItem = null;
    }
  });
}
```

---

## Archive Page Pattern

Shows all archived items with restore functionality.

```html
<main class="container">
  <h1>Archive</h1>

  <div id="archive-empty" class="empty-state">
    <p>No archived items</p>
    <small>Items you archive will appear here</small>
  </div>

  <ul id="archive-list" class="list-view">
    <li class="list-item">
      <div class="list-item-content">
        <strong>Archived Project</strong>
        <small>Archived on Jan 15, 2025</small>
      </div>
      <div class="list-item-actions">
        <button class="btn btn-primary" onclick="restoreItem(this)">Restore</button>
        <button class="btn btn-danger btn-outline" onclick="permanentDelete(this)">Delete Forever</button>
      </div>
    </li>
  </ul>
</main>
```

```javascript
function restoreItem(button) {
  const item = button.closest('li');
  const itemName = item.querySelector('strong')?.textContent || 'Item';

  item.remove();
  showToast(`${itemName} restored.`, null);
  updateEmptyState();
}

function permanentDelete(button) {
  const item = button.closest('li');
  const itemName = item.querySelector('strong')?.textContent || 'Item';

  item.remove();
  showToast(`${itemName} permanently deleted.`, null);
  updateEmptyState();
}

function updateEmptyState() {
  const list = document.getElementById('archive-list');
  const empty = document.getElementById('archive-empty');

  if (list.children.length === 0) {
    empty.style.display = 'block';
    list.style.display = 'none';
  } else {
    empty.style.display = 'none';
    list.style.display = 'block';
  }
}
```

---

## Empty State

Display when a list or view has no items.

```html
<div class="empty-state">
  <p>No projects yet</p>
  <small>Create your first project to get started</small>
  <button class="btn btn-primary">Create Project</button>
</div>
```

```css
.empty-state {
  text-align: center;
  padding: var(--space-8) var(--space-4);
  color: var(--color-text-secondary);
}

.empty-state p {
  font-size: 18px;
  margin-bottom: var(--space-2);
  color: var(--color-text);
}

.empty-state small {
  display: block;
  margin-bottom: var(--space-6);
}

.empty-state .btn {
  margin: 0 auto;
}
```

---

## Step Indicator

**Important:** No connector lines - steps are separated by whitespace only (gap: 32px).

```html
<div class="steps">
  <div class="step completed">
    <span class="step-number">1</span>
    <span class="step-label">Details</span>
  </div>
  <div class="step active">
    <span class="step-number">2</span>
    <span class="step-label">Review</span>
  </div>
  <div class="step">
    <span class="step-number">3</span>
    <span class="step-label">Confirm</span>
  </div>
</div>
```

```css
.steps {
  display: flex;
  align-items: center;
  gap: var(--space-6);  /* 32px - whitespace separation, no connectors */
  padding: var(--space-5) 0;
}

.step {
  display: flex;
  align-items: center;
  gap: var(--space-2);
}

.step-number {
  width: 24px;
  height: 24px;
  border-radius: 50%;
  background: var(--color-background-subtle);
  color: var(--color-text-muted);
  font-size: 13px;
  font-weight: 600;
  display: flex;
  align-items: center;
  justify-content: center;
}

.step-label {
  font-size: 14px;
  color: var(--color-text-muted);
}

.step.active .step-number {
  background: var(--color-text);
  color: white;
}

.step.active .step-label {
  color: var(--color-text);
  font-weight: 600;
}

.step.completed .step-number {
  background: var(--color-primary);
  color: white;
}
```

---

## Badges / Pills

Non-interactive labels for status and categorization.

### Status Badges

```html
<span class="badge badge-success">Active</span>
<span class="badge badge-warning">Pending</span>
<span class="badge badge-error">Blocked</span>
<span class="badge badge-muted">Inactive</span>
```

```css
.badge {
  display: inline-block;
  padding: var(--space-1) var(--space-3);
  border-radius: var(--radius-full);
  font-size: 12px;
  font-weight: 500;
}

.badge-success {
  background: var(--color-success-bg);
  color: #166534;
}

.badge-warning {
  background: var(--color-warning-bg);
  color: #92400e;
}

.badge-error {
  background: var(--color-danger-bg);
  color: #991b1b;
}

.badge-muted {
  background: var(--color-background-subtle);
  color: var(--color-text-secondary);
}
```

### Category Pills

```html
<div class="pills">
  <span class="pill">Design</span>
  <span class="pill">Development</span>
  <span class="pill">Research</span>
</div>
```

```css
.pills {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-2);
}

.pill {
  display: inline-block;
  padding: var(--space-1) var(--space-3);
  background: var(--color-background-subtle);
  border-radius: var(--radius-full);
  font-size: 14px;
}
```

---

## Error Messages

### Inline Field Error

```html
<label class="form-label">
  <span class="form-label-text">Email</span>
  <input type="email" class="form-input form-input-error" aria-invalid="true" aria-describedby="email-error">
  <small id="email-error" class="form-error">Please check the @ symbol and domain (e.g., name@example.com)</small>
</label>
```

### Error Alert Box

```html
<div class="alert alert-error" role="alert">
  <strong>Something went wrong.</strong> Please try again in a moment.
</div>
```

```css
.alert {
  padding: var(--space-4);
  border-radius: var(--radius-md);
  margin-bottom: var(--space-4);
}

.alert-error {
  background: var(--color-danger-bg);
  border-left: 4px solid var(--color-danger);
  color: var(--color-text);
}

.alert-error strong {
  color: #991b1b;
}

.alert-success {
  background: var(--color-success-bg);
  border-left: 4px solid var(--color-success);
  color: var(--color-text);
}
```

---

## Loading States

### Spinner

```html
<div class="spinner" aria-label="Loading"></div>
```

```css
.spinner {
  width: 24px;
  height: 24px;
  border: 3px solid var(--color-border);
  border-top-color: var(--color-primary);
  border-radius: 50%;
  animation: spin 0.8s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}
```

### Button Loading State

```html
<button class="btn btn-primary" aria-busy="true" disabled>
  <span class="spinner spinner-sm"></span>
  Saving...
</button>
```

```css
.spinner-sm {
  width: 16px;
  height: 16px;
  border-width: 2px;
  margin-right: var(--space-2);
}
```

### Skeleton Loading

```html
<div class="skeleton skeleton-text"></div>
<div class="skeleton skeleton-text short"></div>
```

```css
.skeleton {
  background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
  border-radius: var(--radius-md);
}

.skeleton-text {
  height: 1rem;
  margin-bottom: var(--space-2);
}

.skeleton-text.short {
  width: 60%;
}

@keyframes shimmer {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}
```

---

## Navigation

### Simple Header

```html
<header class="header">
  <nav class="nav container">
    <strong class="nav-brand">App Name</strong>
    <ul class="nav-links">
      <li><a href="#">Overview</a></li>
      <li><a href="#">Projects</a></li>
      <li><a href="#" class="active">Archive</a></li>
    </ul>
  </nav>
</header>
```

```css
.header {
  border-bottom: 1px solid var(--color-border);
  background: white;
}

.nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-top: var(--space-4);
  padding-bottom: var(--space-4);
}

.nav-brand {
  font-size: 18px;
}

.nav-links {
  display: flex;
  gap: var(--space-5);
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-links a {
  color: var(--color-text-secondary);
  text-decoration: none;
}

.nav-links a:hover,
.nav-links a.active {
  color: var(--color-text);
}
```

---

## AI-Assisted Components

Components for AI-powered forms where AI suggests data and users review.

### AI Loading State

```html
<div class="ai-loading">
  <div class="spinner"></div>
  <span>Analyzing...</span>
</div>
```

```css
.ai-loading {
  display: flex;
  align-items: center;
  gap: var(--space-3);
  padding: var(--space-4);
  background: var(--color-background-subtle);
  border-radius: var(--radius-md);
  color: var(--color-text-secondary);
}
```

### AI Suggestion Header

```html
<div class="ai-suggestion-header">
  <span class="ai-badge">AI suggestion</span>
  <small>edit as needed</small>
</div>
```

```css
.ai-suggestion-header {
  display: flex;
  align-items: center;
  gap: var(--space-3);
  margin-bottom: var(--space-4);
}

.ai-badge {
  background: var(--color-info-bg);
  color: #0369a1;
  padding: var(--space-1) var(--space-3);
  border-radius: var(--radius-full);
  font-size: 12px;
  font-weight: 500;
}
```

### AI Suggestion Chips

```html
<div class="ai-chips">
  <label class="ai-chip">
    <input type="checkbox" checked>
    <span>tomatoes (main)</span>
  </label>
  <label class="ai-chip uncertain">
    <input type="checkbox">
    <span>basil</span>
  </label>
</div>
```

```css
.ai-chips {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-2);
}

.ai-chip {
  display: flex;
  align-items: center;
  gap: var(--space-2);
  padding: var(--space-2) var(--space-3);
  background: var(--color-info-bg);
  border-radius: var(--radius-full);
  font-size: 14px;
  cursor: pointer;
}

.ai-chip:hover {
  background: #bae6fd;
}

.ai-chip input[type="checkbox"] {
  width: 16px;
  height: 16px;
  margin: 0;
  accent-color: var(--color-primary);
}

.ai-chip.uncertain {
  background: var(--color-background-subtle);
  border: 1px dashed var(--color-border-strong);
}

.ai-chip.uncertain span {
  color: var(--color-text-secondary);
}
```

---

## 15. Relative Time / Time Ago

Show human-readable relative timestamps instead of absolute dates. Use for "last updated", "created", or any timestamp that benefits from context ("3 days ago" is more useful than "2026-02-11").

### Thresholds

| Elapsed | Display |
|---------|---------|
| < 1 min | "just now" / "právě teď" |
| < 60 min | "X min ago" / "před X min" |
| < 24 hours | "X hours ago" / "před X hod" |
| 1 day | "yesterday" / "včera" |
| 2 days | "day before yesterday" / "předevčírem" |
| < 30 days | "X days ago" / "před X dny" |
| < 12 months | "X months ago" / "před X měsíci" |
| 12+ months | "X years ago" / "před X lety" |

### JavaScript Implementation

```javascript
function formatTimeAgo(isoDateString) {
  if (!isoDateString) return '';
  const diffMs = Date.now() - new Date(isoDateString).getTime();
  const diffMin = Math.floor(diffMs / 60000);
  const diffHour = Math.floor(diffMin / 60);
  const diffDay = Math.floor(diffHour / 24);
  const diffMonth = Math.floor(diffDay / 30);
  const diffYear = Math.floor(diffDay / 365);

  // Adapt strings for your locale
  if (diffMin < 1) return 'just now';
  if (diffMin < 60) return `${diffMin} min ago`;
  if (diffHour < 24) return `${diffHour}h ago`;
  if (diffDay === 1) return 'yesterday';
  if (diffDay < 30) return `${diffDay} days ago`;
  if (diffMonth < 12) return `${diffMonth} months ago`;
  return `${diffYear} years ago`;
}
```

### Live-Updating

For timestamps visible on screen, refresh periodically:

```javascript
setInterval(() => {
  document.querySelectorAll('[data-timestamp]').forEach(el => {
    el.textContent = formatTimeAgo(el.dataset.timestamp);
  });
}, 60000); // Every minute
```

### Clickable Time-Ago (Action Trigger)

Time-ago text can double as an action link. Use `.meta-link` styling — secondary color, accent on hover, no underline. Common pattern: "Updated 3 days ago" triggers a refresh/sync.

```html
<a class="meta-link time-ago" href="#" data-timestamp="2026-02-11T10:00:00Z">
  Updated 3 days ago
</a>
```

```css
.time-ago {
  font-size: var(--font-size-xs);
  color: var(--color-text-secondary);
  cursor: pointer;
  transition: color 150ms ease;
  text-decoration: none;
}

.time-ago:hover,
.time-ago:active {
  color: var(--color-primary);
}
```

---

## 16. Link Visibility

Interactive text (clickable names, filter links, metadata links) must be visually distinct at first sight — users should never have to hover to discover something is clickable.

### Rules

- Use `--color-primary` (#6366f1) as default color for all clickable text elements
- Underline is optional — color alone is sufficient for recognition on interactive elements within app UI (not long-form content)
- Hover/active state darkens to `--color-primary-hover` (#4f46e5) for feedback
- Never use `--color-text-secondary` or `--color-text-muted` as the default for clickable text — these are for non-interactive labels only

### CSS Pattern

```css
.meta-link {
  color: var(--color-primary);
  cursor: pointer;
  transition: color 150ms ease;
}

.meta-link:hover,
.meta-link:active {
  color: var(--color-primary-hover);
}
```

---

## 17. Filter Chip Counts

Tag/filter chips should show how many items they contain. Counts update contextually — they reflect the current view, not global totals.

**Rules:**
- Show count inline after label: `Fantasy 42`
- Count in smaller font, muted opacity (doesn't compete with label)
- Counts update when switching tabs/views (e.g. Favorites shows only favorite counts)
- Zero-count chips can be hidden or dimmed

```css
.filter-chip .chip-count {
  font-size: 10px;
  opacity: 0.6;
  margin-left: 2px;
}
```

---

## 18. Multi-Select OR Filtering

When users select multiple values of the same filter type, use OR (union). Between different types, use AND (intersection).

**Pattern:** Group filters by type → AND between groups, OR within each group.

- Selecting `Fantasy` + `Thriller` → shows all fantasy AND all thriller books (union)
- Selecting `Fantasy` + author `Sapkowski` → shows only Sapkowski's fantasy (intersection)

This matches user mental model: "show me Fantasy OR Thriller" not "show me books that are both Fantasy AND Thriller".

```javascript
const filtersByType = {};
for (const f of activeFilters) {
  if (!filtersByType[f.type]) filtersByType[f.type] = [];
  filtersByType[f.type].push(f);
}

filtered = filtered.filter(item =>
  Object.values(filtersByType).every(group =>   // AND between types
    group.some(f => matchesFilter(item, f))      // OR within same type
  )
);
```
