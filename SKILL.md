---
name: ux-design
description: UX design system inspired by GitLab Pajamas with forgiving software patterns. Use when building frontend interfaces, creating HTML/CSS components, or implementing user-friendly interactions with undo capabilities.
---

# UX Design System

This skill provides a consistent design system for building frontend interfaces using GitLab Pajamas design principles and forgiving software patterns.

## When to Use This Skill

Use this design system when:
- Creating new HTML pages or components
- Building forms, cards, lists, or other UI elements
- Implementing user actions with undo capability
- Styling buttons, inputs, or navigation

## Design Philosophy

Three principles guide every design decision.

### Kind
- **Error messages with empathy**: "Please check the @ and domain" not "Error!"
- **User-first thinking**: Respect the user's time and attention
- **Friendly, not childish**: Professional without corporate bullshit

### Smart
- **Data-driven decisions**: Measure before redesigning, validate after
- **Modern UX patterns**: Lazy registration, forgiving software, progressive disclosure
- **Know when to break rules**: Patterns serve users, not the other way around

### Experienced
- **Reduction over addition**: The best UX is the one users don't remember
- **Respect user context**: Don't interrupt flow, don't demand attention
- **Progressive disclosure**: Show what's needed now, reveal the rest when relevant

### Core Question

**"What to remove?" not "What to add?"**

- Every field is an opportunity to abandon
- Every step is a friction point
- Every duplication is an annoyance

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

## Core Design Principles

### 1. Forgiving Software Pattern

**No confirmation dialogs.** Instead, use reversible actions with undo:

```
User clicks "Archive" → Item archived → Toast appears:
┌─────────────────────────────────────────┐
│ Item archived.  [Undo]  ────────── 5s   │
└─────────────────────────────────────────┘
```

- Actions are reversible for ~5 seconds via toast
- "Deleted" items go to Archive (not permanently removed)
- Archive page shows all archived items with restore option
- Users can always recover from mistakes

### 2. Data Display Patterns

**Cards** - For browsing/overview (visual scanning):
- Use `display: flex; flex-direction: column` on card
- Use `flex-grow: 1` on card body to push footer to bottom
- No borders between cards - use whitespace (gap) only

```
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│ Card Title   │  │ Card Title   │  │ Card Title   │
│ Key info     │  │ Key info     │  │ Longer info  │
│              │  │              │  │ here...      │
│ [Actions]    │  │ [Actions]    │  │ [Actions]    │
└──────────────┘  └──────────────┘  └──────────────┘
        ↑ Buttons always at bottom, regardless of content height
```

**Lists** - For detailed/searchable views (structured data).

**No tables** - Use cards or lists instead.

### 3. Form Inputs

- Clear bordered inputs with visible focus states
- Labels above inputs, never inline
- Inline validation with helpful messages
- Input width reflects expected content (see Input Width Guidelines)

### 4. Dropdown Avoidance

**Avoid dropdowns when possible.** They hide options and require extra clicks.

**Rules:**
- **< 5 options**: Use radio buttons or selectable pills instead
- **5+ options**: Dropdown is acceptable, but make items rich/informative

**When using dropdowns, show composed information:**
```
┌─────────────────────────────────────┐
│ Select company...                 ▼ │
├─────────────────────────────────────┤
│ Acme Corp                           │
│ ID: 12345 · Prague, Czech Republic  │
├─────────────────────────────────────┤
│ TechStart s.r.o.                    │
│ ID: 67890 · Brno, Czech Republic    │
└─────────────────────────────────────┘
```

- **Header**: Primary identifier (company name)
- **Subtext**: Supporting info (ID, address, etc.)
- This helps users make informed selections without leaving the form

### 5. Buttons

- **Primary**: Indigo/purple (`--color-primary`)
- **Secondary**: Gray outlined
- **Danger**: Red (only for truly destructive actions, rare)
- **No orange buttons**

### 6. Minimalist Design

- Clean, simple interfaces with generous whitespace
- No pure colors: use off-white (#fafafa) and soft black (#1f2937)
- **No borders/lines for separation**: use whitespace only (no grey dividers between sections, items, or cards)
- No icons/emoji unless they have explicit functional meaning

### 7. Heading or Separator, Never Both

Headings and separators both create visual boundaries between content groups. They serve the same purpose — use one or the other, never combine them.

- **Heading** (text label): Creates hierarchy through typography — uppercase, small font, muted color, with whitespace (`margin-top` + `margin-bottom`). Use when groups need a name.
- **Separator** (border/line): Creates a visual break between equal-weight items. Use when items are peers with no named grouping.

**Never add `border-bottom` to a heading.** The heading text itself is the separator — adding a line underneath is redundant double-signaling.

```css
/* CORRECT: heading with whitespace only */
.section-header {
  font-size: var(--font-size-xs);
  font-weight: 600;
  color: var(--color-text-muted);
  text-transform: uppercase;
  letter-spacing: 0.5px;
  margin-top: var(--space-4);
  margin-bottom: var(--space-2);
}

/* WRONG: heading + border = redundant */
.section-header {
  border-bottom: 1px solid var(--color-border); /* NEVER */
}
```

**Quick test:** If you can remove the text and the border still makes sense as a divider, it should be a borderless separator. If you can remove the border and the text still makes sense as a group label, it should be a heading with whitespace only.

### 8. Component Consistency — Audit All Occurrences

When modifying a reusable visual pattern (card, bar, list item, badge), **audit ALL occurrences across the app** and update them to match. A book card in the library, detail view, and player should share the same visual hierarchy.

**Rules:**
- Before changing a component's styling, search the codebase for all places it appears
- Apply the same font sizes, spacing, colors, and layout to every occurrence
- If an occurrence intentionally differs (e.g., compact variant), document why
- If unsure whether to update an occurrence, ask the user explicitly

**Quick test:** Pick any visual element (title, author line, tag badge). Does it look the same everywhere it appears? If not, that's a consistency bug.

### 9. Visual Audit Page — Living Component Reference

Every project with UI should have an **`audit-cards.html`** (or `audit-components.html`) — a standalone HTML page that renders every visual component variant used in the app. This is the single source of truth for visual consistency.

**What it contains:**
- Every card/component variant, numbered (1, 2, 2b, 3, 4...) with:
  - **Label**: short name (e.g., "Book Card — s play")
  - **Description**: what it shows and when
  - **Where**: function name, container, which view it appears in
  - **Live HTML**: exact production markup using the app's real CSS
- List sections (A, B, C...) showing how components appear in context (e.g., "Library list with mix of cards")
- Optional: font/spacing comparison table across variants

**Structure:**
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

**Rules:**
- Links to the app's real `css/styles.css` — components render authentically
- Uses relative CSS path (`css/styles.css`, not `/css/styles.css`) so it works via `file://`
- Disable interactive elements in audit context (`pointer-events: none` on buttons, `cursor: default` on cards)
- List sections show 2 representative rows each — enough to see the pattern, not more
- **Keep it updated**: when you add/change a component variant, update the audit page in the same commit
- When a candidate variant (e.g., 4b) gets promoted to production, merge it into the main number and remove the candidate section

**When to create:**
- At the start of any project that has 3+ distinct visual component variants
- When visual inconsistency bugs start appearing (retroactive audit)

**When to update:**
- Every time a component's markup or styling changes
- When adding a new component variant
- When changing which variant is used in production

### 10. No System Popups

**NEVER use browser system popups** — `alert()`, `confirm()`, `prompt()` are banned. They block the UI, look different on every platform, and break the app's visual identity.

- Use inline UI instead: toast notifications, modal sheets, inline forms
- For confirmations: use the forgiving software pattern (action + undo toast)
- For user input: use inline form fields, never `window.prompt()`

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

## Component Library

See `components.md` for copy-paste ready HTML/CSS for:
- Buttons (primary, secondary, outline)
- Form inputs (text, email, password, textarea)
- Input width utilities
- Cards and Card grids
- List views with actions
- Toast with undo
- Archive page pattern
- Empty states
- Step indicators
- Error messages
- Pills/Tags
- Loading states

## Examples

See `examples.md` for full page examples showing components in context.

---

## Form Guidelines

- Bordered inputs with clear focus states
- Labels above inputs, never inline
- Always show clear focus states
- Friendly, helpful validation messages
- Input widths match expected content length

## Button Guidelines

- Primary action: Indigo background (`.btn-primary`)
- Secondary action: Gray outline (`.btn-secondary`)
- Avoid red/danger buttons - use archive + undo instead
- Only use danger buttons for truly irreversible actions (rare)

## Error Message Guidelines

### Tone
- Always polite and helpful — use "please", "check", "try"
- Offer solutions, don't blame
- Feel like a helpful tip, not a reprimand

### Structure
- **Short**: Problem + action in one sentence where possible
- **Specific**: Show exactly what needs fixing, with an example of correct format
- **Actionable**: Every error suggests a next step

### Patterns

| Instead of | Write |
|------------|-------|
| "Error! Invalid email" | "Please check the @ symbol and domain (e.g., name@email.com)" |
| "Network error" | "Connection lost. Check your internet and try again." |
| "Authentication failed" | "Wrong email or password. Try again or use a different method." |
| "Quota exceeded" | "Too many attempts. Try again tomorrow." |
| "Technical failure" | "Something went wrong. Try again." |

### Rules
- Never show error codes or technical details to users
- Never use ALL CAPS or exclamation marks in errors
- Break long messages into: problem (short) + suggested action
- For capacity/limit messages in private apps: be informational, not apologetic ("This app is private" not "Sorry, you can't access this")

## Step Indicator Guidelines

- **Style**: Subtle circles with numbers + text, all in one line
- **Active step**: Dark circle with white text, bold name
- **Inactive step**: Gray circle with gray text
- **Size**: Small circles 24x24px, font 13px
- **Naming**: Brief (max 2 words), clear actions or content
- **No connector lines**: Steps separated by whitespace only (gap: 32px)

---

## Exceptions & Allowed Patterns

Cases where we intentionally deviate from the core rules above.

### Inline "or" Divider (exception to "no borders/lines")

When a form offers two alternative input methods (e.g. paste URL **or** upload photo), use a short centered divider with text. This is NOT a section separator — it's a semantic "or" indicator, so short lines are appropriate.

```
                    ─────── nebo ───────
```

- Lines are **fixed 60px** each side, not full-width
- Text is centered, muted color, small font
- Use only between **alternative actions** in the same form, never between sequential sections

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

### Drop Zone (exception to "no icons/emoji")

File upload areas use a dashed border to visually communicate "drop target". This is a functional pattern, not decoration.

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

- On mobile: `capture="environment"` on file input opens camera directly
- Always show preview thumbnail after file selection with remove option
- Hidden file input overlays the drop zone for click-to-browse

### Filter Pills with Dual Meaning (exception to uniform pill styling)

When the same UI has both "include" and "exclude" pills, they need different active colors to signal different behavior:

- **Include pills** (active): `--color-primary` (indigo) — "show recipes WITH this"
- **Exclude pills** (active): `--color-text` (dark) — "hide recipes WITH this"

Add `data-exclude` attribute to exclude pills so CSS can differentiate:

```css
.filter-pill.active { background: var(--color-primary); color: white; }
.filter-pill[data-exclude].active { background: var(--color-text); color: white; }
```

**Separation pattern:** When exclusion is a rare "set and forget" preference (e.g., hiding entire categories), move it to a **settings modal** instead of inline pills. The main UI stays positive (inclusion only), and a subtle "Hidden (N)" chip opens the settings when needed. This avoids cognitive load of mixing "tap to show" and "tap to hide" in the same row.

---

## AI-Assisted UX Principle

**"User does minimum, AI does maximum"**

When building forms or interfaces that can leverage AI:
- Minimize required user inputs (e.g., just upload an image)
- AI extracts/suggests all data, user reviews/confirms
- Progressive disclosure based on AI analysis
- Show confidence levels: pre-checked = high confidence, unchecked = uncertain

### Pattern: AI-Assisted Form
1. User provides minimal input (URL, screenshot, file)
2. Show loading state: "Analyzing..."
3. AI processes and returns structured suggestions
4. Display suggestions with editable fields + checkboxes
5. User reviews, modifies if needed, and confirms

### Implementation Notes
- Pre-fill confident suggestions, leave uncertain items unchecked
- Always allow manual override of any AI suggestion
- Include "AI suggestion" indicator so users know what was auto-filled
- Provide clear loading feedback during AI processing

---

## Authentication & Onboarding Patterns

### Lazy Registration

**Don't block exploration with a login wall.** Let users use the app freely first — only ask for credentials when they need identity (save progress, sync, personal content).

#### 1. Default to Anonymous Access

- App loads into a functional state — no login gate, no picker, no modal
- Guest/anonymous mode is the baseline, not a fallback
- First impression is the product, not a form

#### 2. Auth Only at Natural Friction Points

- Prompt for credentials only when the user hits a capability boundary
- Examples: cross-device sync, saving permanent data, premium features
- Prompts appear inline near the blocked action — not a separate page, not a modal

#### 3. Private App Pattern

- For invitation-only apps: no open registration, no "sign up" flow
- Guest limit message is purely informational ("This app is private") — no email prompt, no upsell
- Sign-in link is small and non-blocking — placed in the header alongside navigation, not as a gate
- After first auth, persistent sessions mean the link is never needed again

#### 4. Guest Data Migration on Upgrade

- When a guest signs in, merge their local state into their authenticated profile
- No data loss during the transition — guest progress carries forward
- Migration runs once, flagged to prevent re-running

#### 5. Auto-Sign-In for Returning Users

- `onAuthStateChanged` (or equivalent) must fire before default view selection
- Authenticated users should never flash the guest/login view
- See **Persistent Sessions** below for implementation details

**Progressive access levels** — each unlocked lazily when the user needs it:

```
Level 0: Guest     → Browse, try features (time-limited or read-only)
Level 1: Email     → Full access, sync, persistence, no limits
Level 2: Linked    → Personal content from external services
```

**Implementation rules:**
- Registration = email only (magic link), never passwords
- After registration, seamlessly continue where the user left off (no state loss, no page reload)
- Guest mode works without any input — user lands directly in the app
- "Sign in" shown as a non-blocking option (not a gate)
- When a guest action requires identity, prompt inline near the blocked action with one-tap email entry

### Persistent Sessions

**Once authenticated, keep users logged in indefinitely.** Re-login is friction — avoid it unless security requires it.

**Rules:**
- Use token refresh to extend sessions silently in the background
- On return visits, recognize the user immediately (show name, resume last state)
- If session expires (rare), make re-auth effortless: one tap to resend magic link
- Store auth state in the most durable storage available (IndexedDB > localStorage > cookies)
- Never show a login screen to a returning user who was previously authenticated

**Implementation:**
- Firebase Auth with `browserLocalPersistence` (IndexedDB-backed, survives browser close)
- `onAuthStateChanged` fires on app start with cached user — no network needed
- Silent token refresh every ~50 minutes (tokens expire in 60 min)
- If token refresh fails (offline), continue with cached data until reconnect

---

## Accessibility Guidelines

### Keyboard Navigation

- All interactive elements must be focusable with Tab
- Use `tabindex="0"` for custom interactive elements
- Maintain visible focus indicators
- Support Escape to close dropdowns and dismiss toasts

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

## Content Browsing UX

Patterns for any app where users browse, discover, and interact with content items (books, articles, products, media, recipes, etc.).

### 1. Rich List Items — Show Enough to Decide

List items must provide enough context to decide (open, skip, act) **without navigating to the detail view**. Ask: "What does the user need to know at a glance?"

**Pattern**: Primary info (title) + secondary info (creator, category) + contextual info (progress, status, series position) + brief description or snippet.

```
[thumbnail]  Title (bold, primary text)
             Creator · Category           ← tappable, see principle 2
             Part 3 of 7 in Series Name   ← if applicable
             "Brief description text..."   ← 1-2 lines, truncated
             35% ━━━━━━╸                  ← contextual (progress, price, date)
```

**Don't** just show title + thumbnail and force the user to tap to learn more. That's lazy UX.

### 2. Interactive Metadata — Names Are Navigation

Every entity displayed in a list (person name, category, tag, series) should be **tappable to filter/browse by that entity**. A name is not just a label — it's a link to more content.

**Implementation**: Use `.meta-link` — visually subtle (secondary color, no underline) but interactive (cursor pointer, active state changes color to accent). On tap, apply as a filter with a visible dismissible chip (see principle 6).

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

**Examples**: Tap author name → see all their works. Tap narrator → see everything they performed. Tap genre tag → filter to that genre.

### 3. Series & Sequence Awareness

Items that belong to a series or ordered sequence **must show their position**. Users need to know: Is this item 1 of 5 or 3 of 12? Can I start here?

**Pattern**: Show inline with metadata — "Díl 3 z 7" or "Part 3 / 7". Series name itself is a tappable meta-link (same pattern as principle 2).

### 4. Content Preview — Describe What It's About

Every content item should have a **short preview/description accessible without navigating away**:
- 1-2 line truncated description in the list item itself (preferred)
- Expandable inline description (tap "více" to reveal)
- At minimum: visible in the detail view

Use `--color-text-secondary` for descriptions. Truncate with `-webkit-line-clamp: 2`.

### 5. Contextual Suggestions — Discovery Through Context

When viewing an item's detail, **surface related items** based on shared attributes:
- Same creator → "Další od autora" (More by this author)
- Same performer → "Čte také" (Also performed by)
- Same series → "V sérii" (In this series)
- Same category → "Podobné" (Similar)

Compute client-side from existing data. Show as a horizontal scrollable row of small cards. Each suggestion card is tappable to navigate to that item.

### 6. Active Filters with Dismissible Chips

When the user activates a filter (by tapping a meta-link or selecting a category), show it as a **visible chip that can be dismissed**. The user must always see what's filtering their view.

**Pattern**: Chips appear between search/filter bar and the content list. Each chip shows the filter type + value + × button.

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

Clearing all chips returns to the full unfiltered view.

### 7. Scroll Position Preservation — Stay Where You Were

When the user interacts with filters, expands/collapses items, or navigates away and back, **restore their scroll position**. Losing context is disorienting — the user should never have to scroll back to find where they were.

**When to preserve scroll:**
- Adding or removing a filter chip
- Expanding/collapsing an inline section
- Navigating to a detail view and back
- Changing tabs or sort order

**Implementation**: Save `scrollTop` before any re-render. Restore with `requestAnimationFrame()` after DOM update. Store position per-view so each view remembers independently.

### 8. Tag Cloud Filtering — Browse by Category

When content has categorical metadata (genres, types, topics), show a **tag cloud** — a row of pill buttons that let users filter by tapping. The tag cloud sits above the content list and provides at-a-glance category distribution.

**Model**: Inclusion (tap to show), not exclusion (tap to hide). Users think "show me Fantasy" not "hide everything except Fantasy".

**Components:**
- **"All" pill** — always first, active when no category selected, clears selection on tap
- **Category pills** — show label + count, active state = accent color, sorted by count descending
- **Exclusion settings** — separate from the cloud (settings modal), for "set once, forget" hiding

**Interaction:**
- Tap category → select it (single-select: clears previous)
- Tap active category → deselect (back to "All")
- Tap "All" → clear selection
- Counts reflect the current universe (post-exclusion), not the filtered subset

**Why single-select (not multi-select OR):**
Multi-select adds complexity (how to show 3 active pills on mobile?) for minimal benefit. Users rarely need "Fantasy OR Sci-fi". If they do, they can scan one genre then the other. Keep it simple.

**Persistence:**
- Category selection: NOT persisted (fresh start on reload avoids confusing state)
- Exclusions: persisted (they're preferences, not browsing state)

**Relationship to Active Filters (§6):**
Tag cloud filters by broad categories (genre). Active filter chips filter by specific entities (author, narrator, series). They compose — tag cloud narrows the category, then active filters narrow within it. Don't mix them into one system.

**Layout:**
```
[Vše] [Sci-fi 47] [Historický 29] [Thriller 23] [Fantasy 13] ...
```

Horizontal scroll on mobile, wrap on desktop. Pills use category-specific colors when active (genre → accent color class).

### 9. Meta Cloud — Top N with Expand

When content has many-valued metadata (authors, narrators, tags), show the **top N as pills** with a "and M more" expand button. Don't show 60 pills — show 5 useful ones.

**Pattern:**
```
Autoři: [F. Niedl 21] [J. Kotouč 14] [F. Kotleta 13] ... [a 32 dalších]
```

- Show top 5 by count (or by relevance/preference order)
- Abbreviate names: "František Niedl" → "F. Niedl"
- "a N dalších" opens a full modal with search + multi-select
- Pills toggle active filters (§6) — same dismissible chip system
- Counts come from the current filtered universe

**Modal pattern:**
- Search input at top (filters the list as you type)
- Each item shows full name + count
- Multi-select: tap to toggle, "Hotovo" to apply batch
- Changes applied as active filter chips on confirm
