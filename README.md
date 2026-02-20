# UX Design System

Opinionated design system for building kind, smart web interfaces. Vanilla CSS, no frameworks, no dependencies.

## Philosophy

Three principles guide every design decision.

### Kind

Error messages with empathy: *"Please check the @ and domain"* not *"Error!"*. Respect the user's time and attention. Professional without corporate bullshit.

### Smart

Modern UX patterns: lazy registration, forgiving software, progressive disclosure. Measure before redesigning, validate after. Know when to break rules — patterns serve users, not the other way around.

### Experienced

Reduction over addition: the best UX is the one users don't remember. Don't interrupt flow, don't demand attention. Show what's needed now, reveal the rest when relevant.

### The Core Question

> **"What to remove?" not "What to add?"**
>
> Every field is an opportunity to abandon. Every step is a friction point. Every duplication is an annoyance.

## Key Patterns

- **Forgiving software**: Undo instead of confirm dialogs. Actions are reversible for ~5 seconds via toast. "Deleted" items go to Archive, not the void.
- **Lazy registration**: Don't block exploration with a login wall. Let users use the app freely — only ask for credentials when they need identity.
- **Progressive disclosure**: Show what's needed now, reveal the rest when relevant.
- **No dropdowns for < 5 options**: Use radio buttons or selectable pills instead.
- **No system popups**: `alert()`, `confirm()`, `prompt()` are banned. Use inline UI.

## What's Inside

| File | Content |
|------|---------|
| **[SKILL.md](SKILL.md)** | Design principles, tokens (colors, spacing, typography), 10 core rules, auth/onboarding patterns, accessibility, responsive guidelines |
| **[components.md](components.md)** | 17+ copy-paste vanilla CSS components — buttons, forms, cards, toasts, pills, empty states, step indicators, content cards, and more |
| **[examples.md](examples.md)** | 8 full-page examples — login, dashboard, registration, address form, company registration, empty states, loading states, content library |
| **[preview.html](preview.html)** | Interactive preview — open in any browser to explore the entire system |

## Design Tokens

### Colors

All text colors meet WCAG AA (4.5:1) contrast on `#fafafa` background.

```
Background        #fafafa          Background Subtle  #f0f0f0

Text              #1f2937  14.1:1  Text Secondary     #4b5563  7.2:1
Text Muted        #6b7280  4.6:1

Primary           #6366f1          Primary Hover      #4f46e5

Border            #e5e7eb          Border Strong      #d1d5db

Success           #22c55e          Success BG         #dcfce7
Warning           #f59e0b          Warning BG         #fef3c7
Danger            #ef4444          Danger BG          #fee2e2
Info              #0ea5e9          Info BG            #e0f2fe
```

### Spacing Scale

```
--space-1:  4px     --space-5: 24px
--space-2:  8px     --space-6: 32px
--space-3: 12px     --space-7: 48px
--space-4: 16px     --space-8: 64px
```

### Typography

```css
--font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;

--font-size-xs: 12px    --font-size-xl:  20px
--font-size-sm: 14px    --font-size-2xl: 24px
--font-size-md: 16px    --font-size-3xl: 30px
--font-size-lg: 18px
```

## Use with Claude Code

This repo works as a [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skill. Claude will follow these design principles when building your UI.

```bash
# Personal (all projects)
git clone https://github.com/abr011/ux-design-skill.git ~/.claude/skills/ux-design

# Project-level
git clone https://github.com/abr011/ux-design-skill.git .claude/skills/ux-design
```

## Inspired By

[GitLab Pajamas](https://design.gitlab.com/) design system, implemented in vanilla CSS. No frameworks, no build tools, no dependencies.

## License

MIT
