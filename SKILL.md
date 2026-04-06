---
name: ux-design
description: Use when making UX decisions — interaction patterns, flows, copy, form behavior, navigation, data display, onboarding. For visual implementation (tokens, CSS, markup), see ui-design skill.
---

# UX Design Principles

Behavioral design principles for frontend interfaces. Design-system-agnostic — works with any visual system.

**Core question: "What to remove?" not "What to add?"** Every field is an opportunity to abandon. Every step is friction. Every duplication is noise.

## When to Use

- Deciding how users interact with features (flows, patterns, copy)
- Writing user-facing text (errors, labels, buttons)
- Planning forms, navigation, data display, onboarding
- Designing content browsing or authentication flows

For **CSS, tokens, component markup**: see `ui-design` skill.

**MUST READ sub-files when relevant:**
- Building a content browsing UI (lists, filters, tags, series)? → Read `~/.claude/skills/ux-design/content-browsing.md` first.
- Building auth, login, onboarding, or session handling? → Read `~/.claude/skills/ux-design/auth-patterns.md` first.

---

## Quick Reference

| Decision | Pattern |
|----------|---------|
| Server action (save, archive, send)? | Optimistic UI — update screen instantly, revert on failure |
| Delete/remove action? | No confirmation dialog — reversible action + undo toast (5s) |
| Multiple toasts firing? | Stack max 3, merge same-type ("3 archived [Undo all]") |
| Display a collection? | Cards for browsing/scanning, lists for structured data. No tables. |
| How many options? | <5 → radio/pills. 5+ → dropdown with rich items |
| Separate sections? | Heading OR separator, never both |
| Need a label? | Skip if value is self-evident from format/position/context |
| Badge an item? | Badge the exception (minority state), not the default |
| Status indicator? | Passive/read-only, not interactive (see ui-design) |
| Interactive element? | Default to passive. Only add interaction if user must act. |
| Empty view (no data yet)? | Onboarding: explain what goes here + action button. Never blank. |
| Too many form fields? | Progressive disclosure: show essential fields, hide rest behind "More" |
| Error message? | Polite + specific + actionable. No codes, no caps, no blame. |
| Loading state? | Skeleton screen for layout, spinner for actions. Never blank. |
| Offline state? | Show cached content + subtle offline indicator. Never block. |
| Multi-step flow? | Step indicator (subtle circles), allow back navigation, preserve state |
| Mobile nav? | Bottom nav for 3-5 primary actions. Hamburger only for secondary. |
| User providing data manually? | App should extract/pre-fill it. User confirms, not types. |
| Feature needs multiple capability levels? | Build in tiers: manual → assisted → automatic → predictive |

---

## Core Principles

### 1. Forgiving Software

**No confirmation dialogs.** Use reversible actions with undo:

```
User clicks "Archive" → Item archived → Toast:
┌─────────────────────────────────────────┐
│ Item archived.  [Undo]  ────────── 5s   │
└─────────────────────────────────────────┘
```

- "Deleted" items go to Archive, not permanent removal
- Archive page shows all archived items with restore option

### 2. Optimistic UI

**Update the screen instantly. Don't wait for the server.**

When the user clicks save, archive, send, or any server action:
1. Update the UI immediately (remove the item, show the change)
2. Send the request to the server in the background
3. If the server confirms — done, nothing to do
4. If connection fails — queue the action, retry silently until it succeeds (like Instagram)
5. If the server explicitly rejects — revert the UI change and show an error toast

The user never sees a spinner for common actions. Everything feels instant. Failed actions retry automatically — the user doesn't need to know about network hiccups.

**When NOT to use:** Irreversible actions with real consequences (sending money, deleting permanently). Those should wait for server confirmation before updating UI.

### 3. Toast Stacking

When multiple toasts fire (batch actions, background jobs completing), manage them:
- **Max 3 visible** at a time — new ones push oldest out
- **Merge same-type actions**: "3 invoices archived" with [Undo all], not 3 separate toasts
- **Auto-dismiss** after 5 seconds each (toasts with undo get the full 5s)
- **Position**: bottom-left or bottom-center, never covering primary content or navigation

### 4. Data Display

- **Cards**: browsing/overview (visual scanning). No borders between cards — whitespace only.
- **Lists**: detailed/searchable views (structured data)
- **No tables**: use cards or lists instead

### 3. Forms

- Labels above inputs, never inline
- Input width reflects expected content length (see ui-design Input Width Guidelines)
- Inline validation with helpful messages
- Clear focus states

### 4. Dropdown Avoidance

- **< 5 options**: radio buttons or selectable pills
- **5+ options**: dropdown with rich items (header + subtext with supporting info)

### 5. Minimalist Design

- Generous whitespace, no clutter
- No pure colors — off-white backgrounds, soft black text
- **No borders/lines for separation** — use whitespace only
- No icons/emoji unless they have explicit functional meaning

### 6. Heading or Separator, Never Both

Both create visual boundaries. Use one:
- **Heading**: creates hierarchy via typography (uppercase, small, muted). Use when groups need a name.
- **Separator**: creates a visual break between equal-weight items.
- **Never add `border-bottom` to a heading** — the text IS the separator.

### 7. Component Consistency

When modifying a reusable pattern, **audit ALL occurrences** and update to match. A component should look the same everywhere it appears.

### 8. Labels Are Last Resort

Skip labels when format/position/context makes the value obvious:
- Dates, names, counts, percentages — self-evident
- Add labels only for: ambiguous values (IČO: 12345678), same-type values needing disambiguation, technical data

### 9. Badge the Exception

When most items share one state, don't badge that state. Badge only the minority:
```
Default (90%):  Zaklínač           12h 30m          ← no badge
Exception:      Stopařův průvodce  6h 27m  Koupeno  ← badge
```

### 10. No System Popups

`alert()`, `confirm()`, `prompt()` are banned. Use inline UI: toasts, modal sheets, inline forms.

### 11. Empty State as Onboarding

Empty screens are not dead ends — they're the first impression. When a view has no data yet, show **what to do first**:

- Short explanation of what will appear here
- Primary action button to create the first item or connect a data source
- No sad icons, no "nothing here" — be helpful, not apologetic

```
┌─────────────────────────────────────┐
│                                     │
│   Zatím žádné faktury               │
│                                     │
│   Vytvořte první fakturu nebo       │
│   připojte Gmail pro automatický    │
│   import.                           │
│                                     │
│   [Vytvořit fakturu]                │
│                                     │
└─────────────────────────────────────┘
```

Every list, dashboard section, and collection view must have a designed empty state. Never show a blank area or just a technical "0 results".

### 12. Progressive Disclosure

Show the simple version first. Hide advanced options behind "More" or expandable sections.

- **Forms**: show 3-5 essential fields. Put optional/advanced fields behind "Další možnosti" toggle.
- **Settings**: show common settings. Group advanced ones in a collapsible section.
- **Detail views**: show key info at a glance. Expandable sections for full history, technical details, metadata.

**Rule of thumb**: if fewer than 30% of users need it, hide it by default.

### 13. Visual Audit Page

Every UI project with 3+ component variants needs an `audit-cards.html` — renders every variant with real CSS. Keep updated with every component change. See ui-design for template.

---

## Loading & Skeleton States

Never show a blank screen. Users need feedback that something is happening.

**Action loading** (button click, form submit): inline spinner replacing the button text. Disable the button.

**Content loading** (page load, data fetch): skeleton screen matching the layout shape:
```
┌──────────────────────────────────────┐
│ ████████████████                     │  ← title placeholder
│ ████████ ██████████████              │  ← metadata
│ ████████████████████████████████████ │  ← description line 1
│ ████████████████████████████         │  ← description line 2
└──────────────────────────────────────┘
```

- Skeleton shapes match actual content dimensions
- Subtle pulse animation (opacity 0.6 → 1.0)
- Transition smoothly from skeleton to real content (no flash/jump)
- Show skeleton for minimum 200ms to avoid flicker on fast loads

**Partial loading**: show available content immediately, skeleton only for pending parts.

---

## Offline & PWA UX

For apps with service workers or offline capability:

- **Show cached content immediately** — never block the UI waiting for network
- **Subtle offline indicator** — small banner or icon, not a full-screen blocker
- **Queue actions offline** — let users act, sync when back online
- **Distinguish stale data** — muted timestamp "Last updated: 2h ago" when showing cached content
- **Reconnection**: auto-sync silently, brief toast "Synced" on success

**Anti-patterns:**
- Full-screen "You're offline" blocking cached content
- Hiding features that work offline
- Losing user input when connection drops

---

## Multi-Step Flows (Wizards)

For processes with 3+ distinct steps:

- **Step indicator**: subtle numbered circles in a row (see ui-design for sizing)
- **Allow back navigation**: never trap users. Previous steps preserve their input.
- **Preserve state**: if user leaves mid-flow and returns, resume where they left off
- **Validate per step**: don't wait until the end to show errors
- **Show progress**: "Step 2 of 4" is clearer than just step names

**Anti-patterns:**
- Resetting form state on back navigation
- Validating all steps only at final submit
- No way to review previous steps before confirming

---

## Responsive Navigation

**Bottom navigation** (mobile, 3-5 items):
- Primary actions always visible as bottom tabs
- Active tab highlighted, others muted
- Labels under icons (icons alone are ambiguous)

**Hamburger menu** (secondary/overflow items only):
- Never hide primary navigation behind hamburger
- Acceptable for: settings, account, help, rarely-used pages

**Desktop → Mobile adaptation:**
- Horizontal nav → bottom tabs (primary) + hamburger (secondary)
- Sidebar → slides in from left as overlay on mobile
- Multi-column → single column, cards stack vertically

---

## Error Recovery

Beyond error message copy (see Error Messages below), handle recovery:

- **Form errors**: highlight the specific field, scroll to it, focus it. Don't just show a toast.
- **Network errors**: retry automatically (with backoff), show retry button after 3 failures
- **Lost input**: autosave form state to localStorage every 5s. Restore on reload.
- **Partial failures**: complete what succeeded, report what failed, offer retry for failures only
- **Session expiry**: preserve current state, re-auth inline, resume without data loss

---

## Error Messages

### Tone
- Polite and helpful — "please", "check", "try"
- Offer solutions, don't blame

### Patterns

| Instead of | Write |
|------------|-------|
| "Error! Invalid email" | "Please check the @ symbol and domain (e.g., name@email.com)" |
| "Network error" | "Connection lost. Check your internet and try again." |
| "Authentication failed" | "Wrong email or password. Try again or use a different method." |

### Rules
- Never show error codes or technical details
- Never use ALL CAPS or exclamation marks
- Break long messages into: problem (short) + suggested action

---

## The App Does the Work (core philosophy)

**The user expresses intent. The app does everything else.**

The user should never be a middleman between systems, never manually transfer data, never manage technical processes. Their only job is to say what they want.

### Examples of right vs wrong

| User intent | Wrong (user is middleman) | Right (app does the work) |
|---|---|---|
| "I want this recipe from Instagram" | Open form, user rewrites recipe from post | User pastes link or screenshot → app extracts recipe from video/description/comments automatically |
| "I want to listen offline" | User manually downloads each book | App silently caches what they're listening to, explicit download for guaranteed offline |
| "I need this invoice paid" | User copies bank details, opens banking app | App generates ABO payment file ready for bank import |
| "Add this contact" | User types name, phone, email from a business card | User takes photo → app extracts all fields |

### Progressive capability tiers

For features that can work at multiple levels, build in tiers — each one does more for the user:

```
Tier 1: Manual        → user does it themselves (baseline, always available)
Tier 2: Assisted      → app pre-fills/suggests, user confirms
Tier 3: Automatic     → app does it silently, user can override
Tier 4: Predictive    → app does it before user asks
```

**Example — offline audio (prehravac):**
```
Tier 1: Stream only           → play from CDN, needs connection
Tier 2: Smart cache           → auto-cache what user listens to
Tier 3: Explicit download     → user taps download for guaranteed offline
Tier 4: Full offline          → app works entirely without connection, syncs later
```

**Example — invoice creation (kancelar):**
```
Tier 1: Manual form           → user fills all fields
Tier 2: Pattern suggestions   → app suggests amount, client, frequency from history
Tier 3: Auto-create           → app creates recurring invoices automatically at 7 AM
Tier 4: Predictive            → app anticipates new clients based on email patterns
```

### AI-assisted input (specific pattern)

When AI can extract data from user input:
1. User provides minimal input (URL, screenshot, photo, file)
2. Show loading: "Analyzing..."
3. AI returns structured suggestions
4. Display with editable fields + checkboxes (pre-checked = high confidence)
5. User reviews, modifies, confirms

- Always allow manual override
- Show "AI suggestion" indicator on auto-filled fields
- Never show an empty form when the app could pre-fill it

---

## Exceptions & Allowed Patterns

### Inline "or" Divider
Short centered divider between alternative input methods (paste URL **or** upload photo). Fixed 60px lines, not full-width. Only between alternative actions, never between sequential sections.

### Drop Zone
Dashed border file upload areas. On mobile: `capture="environment"` opens camera. Show preview thumbnail after selection.

### Filter Pills with Dual Meaning
Include pills (active = primary color) vs exclude pills (active = dark color). When exclusion is rare, move to settings modal instead.

---

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Making status indicators clickable buttons | Default to passive/read-only display |
| Confirmation dialogs for reversible actions | Forgiving software: action + undo toast |
| Full-screen offline blocker over cached content | Subtle indicator + show cached data |
| Guessing at Safari audio/autoplay behavior | Check existing working code first (see CLAUDE.md Safari rules) |
| Blank screen during data loading | Skeleton screen matching layout shape |
| Hiding primary nav in hamburger on mobile | Use bottom tabs for 3-5 primary actions |
| Heading with border-bottom underneath | Heading OR separator, never both |
| Badging every item's state | Badge exceptions only, leave default unmarked |
| Building interactive UI when passive would do | Ask: "Does the user need to ACT on this?" |

---

*For visual implementation: see `ui-design` skill.*
*For content browsing patterns: see `content-browsing.md`.*
*For auth & onboarding: see `auth-patterns.md`.*
