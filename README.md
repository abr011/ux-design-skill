# UX/UI Design Skills for Claude Code

Two independent skills for building kind, smart web interfaces. **UX** handles behavioral principles. **UI** handles visual implementation. Swap the visual system without losing your UX foundations.

## Architecture

```
ux-design-skill/
├── SKILL.md              ← UX skill: behavioral principles (design-system-agnostic)
└── ui-design/
    ├── SKILL.md           ← UI skill: Pajamas-inspired tokens, CSS patterns
    ├── components.md      ← 17+ copy-paste vanilla CSS components
    ├── examples.md        ← 8 full-page examples
    └── preview.html       ← Interactive preview (open in browser)
```

### UX Skill (SKILL.md)

Design-system-agnostic behavioral principles:

- **Forgiving software**: Undo instead of confirm dialogs
- **Lazy registration**: Don't block exploration with a login wall
- **Progressive disclosure**: Show what's needed now, reveal the rest when relevant
- **Content browsing UX**: Rich list items, interactive metadata, series awareness, tag clouds
- **Error messages**: Empathetic copy guidelines
- **Form behavior**: Dropdown avoidance, input width hinting
- **Accessibility**: Keyboard navigation, ARIA patterns
- **AI-assisted UX**: "User does minimum, AI does maximum"

### UI Skill (ui-design/)

GitLab Pajamas-inspired visual implementation in vanilla CSS:

- **Design tokens**: Colors (WCAG AA), spacing scale, typography, border radius
- **Component CSS**: Buttons, forms, cards, toasts, pills, navigation, content cards
- **Responsive layout**: Mobile-first breakpoints, touch targets
- **Full examples**: Login, dashboard, registration, content library

## Philosophy

Three principles guide every design decision:

- **Kind** — Error messages with empathy. Professional without corporate bullshit.
- **Smart** — Modern UX patterns. Measure before redesigning, validate after.
- **Experienced** — Reduction over addition. The best UX is the one users don't remember.

> **"What to remove?" not "What to add?"**

## Use with Claude Code

This repo works as a [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skill.

```bash
# Clone to your skills directory (creates both ux-design/ and ui-design/)
git clone https://github.com/abr011/ux-design-skill.git ~/.claude/skills/ux-design

# Then add to your CLAUDE.md:
# - Invoke `ux-design` skill before making UX decisions
# - Invoke `ui-design` skill before writing CSS/HTML components
```

Claude will follow UX principles when designing interactions and UI tokens when writing CSS.

## Inspired By

[GitLab Pajamas](https://design.gitlab.com/) design system, implemented in vanilla CSS. No frameworks, no build tools, no dependencies.

## License

MIT
