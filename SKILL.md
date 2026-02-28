---
name: ux-design
description: Design-system-agnostic UX principles — forgiving software, interaction patterns, content browsing, copy guidelines, lazy registration. For visual implementation (tokens, CSS, component markup), see the ui-design skill.
---

# UX Design Principles

This skill provides behavioral design principles for building frontend interfaces. It is design-system-agnostic — the interaction patterns, copy guidelines, and philosophy here work with any visual system.

For **visual implementation** (design tokens, CSS, component markup, responsive layout), see the `ui-design` skill at `~/.claude/skills/ui-design/`.

## When to Use This Skill

Use this skill when:
- Making UX decisions (interaction patterns, flows, copy)
- Deciding how users should interact with features
- Writing user-facing text (error messages, labels, buttons)
- Planning form behavior, navigation, or data display
- Designing onboarding, authentication, or content browsing flows

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
- Push footer to bottom using flex layout
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

*For card CSS (flex-direction, flex-grow), see ui-design skill.*

### 3. Form Inputs

- Clear bordered inputs with visible focus states
- Labels above inputs, never inline
- Inline validation with helpful messages
- Input width reflects expected content (see ui-design Input Width Guidelines)

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

- **Primary**: Main action (indigo/purple)
- **Secondary**: Gray outlined
- **Danger**: Only for truly destructive actions (rare)
- **No orange buttons**

*For button color values, see ui-design skill.*

### 6. Minimalist Design

- Clean, simple interfaces with generous whitespace
- No pure colors: use off-white and soft black
- **No borders/lines for separation**: use whitespace only (no grey dividers between sections, items, or cards)
- No icons/emoji unless they have explicit functional meaning

*For specific color values (off-white, soft black), see ui-design design tokens.*

### 7. Heading or Separator, Never Both

Headings and separators both create visual boundaries between content groups. They serve the same purpose — use one or the other, never combine them.

- **Heading** (text label): Creates hierarchy through typography — uppercase, small font, muted color, with whitespace (`margin-top` + `margin-bottom`). Use when groups need a name.
- **Separator** (border/line): Creates a visual break between equal-weight items. Use when items are peers with no named grouping.

**Never add `border-bottom` to a heading.** The heading text itself is the separator — adding a line underneath is redundant double-signaling.

**Quick test:** If you can remove the text and the border still makes sense as a divider, it should be a borderless separator. If you can remove the border and the text still makes sense as a group label, it should be a heading with whitespace only.

*For section header CSS, see ui-design skill.*

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
- List sections (A, B, C...) showing how components appear in context
- Optional: font/spacing comparison table across variants

**Rules:**
- Links to the app's real CSS — components render authentically
- Uses relative CSS path so it works via `file://`
- Disable interactive elements in audit context
- List sections show 2 representative rows each
- **Keep it updated**: when you add/change a component variant, update the audit page in the same commit
- When a candidate variant gets promoted to production, merge it into the main number

**When to create:** At the start of any project with 3+ distinct visual component variants.

**When to update:** Every time a component's markup or styling changes.

*For audit page HTML template, see ui-design skill.*

### 10. No System Popups

**NEVER use browser system popups** — `alert()`, `confirm()`, `prompt()` are banned. They block the UI, look different on every platform, and break the app's visual identity.

- Use inline UI instead: toast notifications, modal sheets, inline forms
- For confirmations: use the forgiving software pattern (action + undo toast)
- For user input: use inline form fields, never `window.prompt()`

### 11. Labels Are Last Resort (Data Display)

**When displaying data, show values only.** Labels add visual noise — most values are self-explanatory from context, format, or position.

This applies to **read-only views** (detail pages, cards, lists, summaries). Forms (§3) still need labels above every input.

**When to skip labels:**
- Dates, times, durations — format is obvious (`14. 2. 2026`, `8 h 3 min`)
- Names, titles — position/typography makes the role clear (bold title, secondary-color author)
- Counts, percentages, ratings — numbers with units speak for themselves
- Status indicators — color/icon/badge is enough (`● Rozposloucháno`)

**When labels help (suggest sparingly):**
- Ambiguous values — e.g., "IČO: 12345678" (without label, just a number)
- Multiple values of same type — e.g., author vs. narrator are both names, so "Čte: Anna Brousková" disambiguates
- Technical or domain-specific data — e.g., "ISBN", "Vzorkovací frekvence"

**Test:** Remove the label. Would a user still know what the value means from context? If yes, skip it.

### 12. Badge the Exception, Not the Default

**When most items share one state, don't badge that state.** Only badge the minority — the exceptions that need attention. Badging the default adds visual noise without information.

**The pattern:**
- Identify the dominant state (the one 70%+ of items have)
- Leave the dominant state unmarked — it's the assumed default
- Badge only the exceptions that differ from the default

**Example — book ownership (90% Klub, 6% purchased, 5% sample):**
```
Klub book:       Zaklínač              12h 30m          ← no badge (default)
Purchased book:  Stopařův průvodce     6h 27m  Koupeno  ← green badge
Sample book:     Jméno růže            5h 52m  Ukázka   ← gray badge + dimmed
```

**Why it works:**
- The eye is drawn to what's different — badges on exceptions pop naturally
- Badging everything (including the default) creates uniform noise where nothing stands out
- Users learn the default quickly ("no badge = normal") and scan for exceptions

**When the dominant state IS worth badging:**
- Legal/compliance requirements (e.g., every item must show its license)
- The majority changes frequently (today 90% are X, tomorrow 60% — unstable default)
- Two states are close to 50/50 split (no clear default)

**Test:** If you badge everything, does the badge still draw attention? If no — you're adding noise, not information.

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
- **Naming**: Brief (max 2 words), clear actions or content
- **No connector lines**: Steps separated by whitespace only

*For step indicator sizing (24x24px, 13px, 32px gap), see ui-design skill.*

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

*For CSS implementation, see ui-design skill.*

### Drop Zone (exception to "no icons/emoji")

File upload areas use a dashed border to visually communicate "drop target". This is a functional pattern, not decoration.

- On mobile: `capture="environment"` on file input opens camera directly
- Always show preview thumbnail after file selection with remove option
- Hidden file input overlays the drop zone for click-to-browse

*For CSS implementation, see ui-design skill.*

### Filter Pills with Dual Meaning (exception to uniform pill styling)

When the same UI has both "include" and "exclude" pills, they need different active colors to signal different behavior:

- **Include pills** (active): primary color — "show recipes WITH this"
- **Exclude pills** (active): dark color — "hide recipes WITH this"

Add `data-exclude` attribute to exclude pills so CSS can differentiate.

**Separation pattern:** When exclusion is a rare "set and forget" preference (e.g., hiding entire categories), move it to a **settings modal** instead of inline pills. The main UI stays positive (inclusion only), and a subtle "Hidden (N)" chip opens the settings when needed. This avoids cognitive load of mixing "tap to show" and "tap to hide" in the same row.

*For CSS implementation, see ui-design skill.*

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

*For ARIA attribute examples and `.sr-only` CSS, see ui-design skill.*

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

**Examples**: Tap author name → see all their works. Tap narrator → see everything they performed. Tap genre tag → filter to that genre.

*For `.meta-link` CSS, see ui-design skill.*

### 3. Series & Sequence Awareness

Items that belong to a series or ordered sequence **must show their position**. Users need to know: Is this item 1 of 5 or 3 of 12? Can I start here?

**Pattern**: Show inline with metadata — "Díl 3 z 7" or "Part 3 / 7". Series name itself is a tappable meta-link (same pattern as principle 2).

### 4. Content Preview — Describe What It's About

Every content item should have a **short preview/description accessible without navigating away**:
- 1-2 line truncated description in the list item itself (preferred)
- Expandable inline description (tap "více" to reveal)
- At minimum: visible in the detail view

Use secondary text color for descriptions. Truncate with line clamping.

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

Clearing all chips returns to the full unfiltered view.

*For filter chip CSS and HTML, see ui-design skill.*

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

Horizontal scroll on mobile, wrap on desktop. Pills use category-specific colors when active.

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

---

*For visual implementation of all patterns above (design tokens, CSS, component markup, responsive layout, accessibility markup), see the `ui-design` skill at `~/.claude/skills/ui-design/`.*
