# Authentication & Onboarding Patterns

Referenced from the main `ux-design` SKILL.md.

---

## Lazy Registration

**Don't block exploration with a login wall.** Let users use the app first — only ask for credentials when they need identity.

### 1. Default to Anonymous Access

- App loads into a functional state — no login gate, no picker, no modal
- Guest/anonymous mode is the baseline, not a fallback
- First impression is the product, not a form

### 2. Auth Only at Natural Friction Points

- Prompt only when user hits a capability boundary (sync, save, premium)
- Prompts appear inline near the blocked action — not a separate page

### 3. Private App Pattern

- Invitation-only: no open registration, no "sign up" flow
- Guest limit message is informational ("This app is private") — no upsell
- Sign-in link is small, non-blocking — in header alongside navigation, not as a gate
- After first auth, persistent session means the link is never needed again

### 4. Guest Data Migration

- When guest signs in, merge local state into authenticated profile
- No data loss — guest progress carries forward
- Migration runs once, flagged to prevent re-running

### 5. Auto-Sign-In for Returning Users

- `onAuthStateChanged` must fire before default view selection
- Authenticated users should never flash the guest/login view

---

## Progressive Access Levels

Each unlocked lazily when needed:

```
Level 0: Guest     → Browse, try features (time-limited or read-only)
Level 1: Email     → Full access, sync, persistence, no limits
Level 2: Linked    → Personal content from external services
```

**Rules:**
- Registration = email only (magic link), never passwords
- After registration, continue seamlessly (no state loss, no reload)
- "Sign in" shown as non-blocking option (not a gate)
- When guest action requires identity, prompt inline with one-tap email entry

---

## Persistent Sessions

**Once authenticated, keep logged in indefinitely.** Re-login is friction.

**Rules:**
- Token refresh extends sessions silently in background
- On return, recognize user immediately (show name, resume last state)
- If session expires: one tap to resend magic link
- Store auth state in most durable storage (IndexedDB > localStorage > cookies)
- Never show login screen to a previously authenticated returning user

**Firebase implementation:**
- `browserLocalPersistence` (IndexedDB-backed, survives browser close)
- `onAuthStateChanged` fires on start with cached user — no network needed
- Silent token refresh every ~50 minutes (tokens expire in 60 min)
- If refresh fails (offline), continue with cached data until reconnect
