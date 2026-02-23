# Changelog

## 2026-02-23 — UX/UI Skill Split

**What changed:** The single `ux-design` skill was split into two independent skills.

**Why:** The original skill mixed behavioral UX principles (forgiving software, lazy registration, content browsing patterns) with visual implementation details (CSS tokens, component markup, Pajamas colors). This made it impossible to swap the visual system without rewriting the entire skill.

**The two skills:**

| Skill | Scope | Files |
|-------|-------|-------|
| **ux-design** (`SKILL.md`) | Interaction patterns, copy guidelines, form behavior, auth flows, content browsing UX, accessibility rules | 1 file |
| **ui-design** (`ui-design/`) | Pajamas-inspired design tokens, CSS component patterns, responsive layout, ARIA markup, full-page examples | 4 files |

**Migration:** Update your `CLAUDE.md` to invoke both skills:

```markdown
- Invoke `ux-design` skill before making UX decisions (interaction patterns, flows, copy)
- Invoke `ui-design` skill before writing CSS/HTML components (tokens, styling, markup)
```

Cross-references between skills use relative paths (e.g., "see ui-design skill" / "see ux-design skill").
