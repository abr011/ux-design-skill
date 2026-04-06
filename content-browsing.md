# Content Browsing UX

Patterns for apps where users browse, discover, and interact with content items (books, articles, products, media, recipes, etc.).

Referenced from the main `ux-design` SKILL.md. For CSS implementations, see `ui-design` skill.

---

## 1. Rich List Items — Show Enough to Decide

List items must provide enough context to decide (open, skip, act) **without navigating to the detail view**.

```
[thumbnail]  Title (bold, primary text)
             Creator · Category           ← tappable, see §2
             Part 3 of 7 in Series Name   ← if applicable
             "Brief description text..."   ← 1-2 lines, truncated
             35% ━━━━━━╸                  ← contextual (progress, price, date)
```

**Don't** just show title + thumbnail and force tap-to-learn-more.

## 2. Interactive Metadata — Names Are Navigation

Every entity (person, category, tag, series) should be **tappable to filter/browse by that entity**. A name is not just a label — it's a link.

Use `.meta-link` — visually subtle (secondary color, no underline) but interactive (cursor pointer, active = accent color). On tap, apply as a dismissible filter chip (§6).

## 3. Series & Sequence Awareness

Items in a series **must show position**: "Díl 3 z 7" or "Part 3 / 7". Series name itself is a tappable meta-link.

## 4. Content Preview

Every item should have a **short description accessible without navigating away**:
- 1-2 line truncated description inline (preferred)
- Expandable "více" to reveal full text
- At minimum: visible in detail view

## 5. Contextual Suggestions — Discovery Through Context

On item detail, **surface related items** by shared attributes:
- Same creator → "Další od autora"
- Same performer → "Čte také"
- Same series → "V sérii"
- Same category → "Podobné"

Compute client-side from existing data. Horizontal scrollable row of small cards.

## 6. Active Filters with Dismissible Chips

When user activates a filter (meta-link tap, category select), show as a **visible chip with × dismiss button**. User must always see what's filtering their view.

Chips appear between search bar and content list. Clearing all returns to unfiltered view.

*For filter chip CSS/HTML, see ui-design skill.*

## 7. Scroll Position Preservation

When user filters, expands/collapses, or navigates away and back, **restore scroll position**.

**When to preserve:**
- Adding/removing filter chips
- Expanding/collapsing inline sections
- Navigating to detail and back
- Changing tabs or sort order

**Implementation**: Save `scrollTop` before re-render. Restore with `requestAnimationFrame()` after DOM update. Store per-view.

## 8. Tag Cloud Filtering — Browse by Category

When content has categories (genres, types), show a **pill row** above content for filtering:

```
[Vše] [Sci-fi 47] [Historický 29] [Thriller 23] [Fantasy 13] ...
```

**Model**: Inclusion (tap to show), not exclusion.

**Components:**
- **"All" pill** — always first, active when nothing selected
- **Category pills** — label + count, sorted by count descending

**Interaction:**
- Tap category → select (single-select, clears previous)
- Tap active → deselect (back to All)
- Counts reflect current universe (post-exclusion)

**Why single-select:** Multi-select adds complexity for minimal benefit. Users rarely need "Fantasy OR Sci-fi".

**Persistence:** Category selection NOT persisted (fresh on reload). Exclusions ARE persisted (preferences).

## 9. Meta Cloud — Top N with Expand

For many-valued metadata (authors, narrators), show **top 5 as pills** with expand:

```
Autoři: [F. Niedl 21] [J. Kotouč 14] [F. Kotleta 13] ... [a 32 dalších]
```

- Abbreviate names: "František Niedl" → "F. Niedl"
- "a N dalších" opens full modal with search + multi-select
- Pills toggle active filters (§6)
- Counts from current filtered universe

**Modal pattern:** Search at top, full name + count per item, multi-select with "Hotovo" to apply batch.
