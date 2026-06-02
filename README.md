# WoGL Academy — MVP 1.0

Full user journey end-to-end, written from scratch.

**Live preview:** https://wogl-oficial.github.io/wogl-mvp1.0/
**Mirror in staging:** https://wogl-oficial.github.io/staging/wogl-mvp1.0/

---

## What this is

A single self-contained `index.html` that carries the entire MVP 1.0
user experience: open academy, browse lessons, log in, onboard, land
in your world. No patches from prior iterations — every token,
hierarchy and flow decision is auditable here.

## Core design choices

- **Browse language vs account language** — two separate states.
  Browse language lives in the header toggle (default EN), affects
  what the academy displays publicly. Account language is asked at
  first login via a Step 0 picker and drives the chassis (auth,
  onboarding, Your World, settings, emails). A user can browse the
  academy in English but live their account in Spanish, or vice
  versa.
- **Open academy first** — visitors land on lessons, not a marketing
  landing. Login is always available in the header.
- **Cloudflare Turnstile** for signup, login and password reset.
  Localhost falls back to the test sitekey automatically.
- **Supabase** for auth, profile, lesson progress and badges. The
  RPCs `check_name_available`, `init_profile`, `update_theme` are
  the contract; client code stays defensive against transient
  network and RPC failures.

## Status

Built block by block, each one validated end-to-end on **iPhone Safari
AND web desktop** before moving on.

- [x] **B1 — Scaffold + design tokens** ✅
- [x] **B2 — Chassis bilingual with browse vs account split** ✅
- [x] **B3 — Auth + onboarding + welcome confirmations + Turnstile + reset + change password** ✅ validated 2026-06-02 on iPhone Safari with user "Claudita" creating a fresh account, then re-validated on web desktop. Same flow, same result.
- [ ] B4 — Your World — Profile, Settings, Backpack
- [ ] B5 — Academy structure — sidebar drawers, sections
- [ ] B6 — Ten Start Here lessons with sandbox
- [ ] B7 — Progress wiring — record completions, auto-award badges
- [ ] B8 — Smoke test end-to-end

**Chassis = backbone of the product, holds together in both surfaces.**
Everything from B4 onward is content on top of this foundation.

Milestone snapshot of the validated B1–B3 state:
`_iterations/2026-06-02-mvp1.0-chassis-validated-iphone-claudita.html`

## Working tree

```
wogl-mvp1.0/
  index.html          ← the whole product, self-contained
  README.md           ← this file
```

## Local dev

```
cd wogl-mvp1.0
python3 -m http.server 8770
open http://localhost:8770/
```

Turnstile in localhost uses Cloudflare's always-pass test sitekey
(`1x00000000000000000000AA`). Supabase will reject those tokens
server-side, so signup/login itself runs from a hostname that's
whitelisted on the real sitekey — local dev is for UI work.

## Conventions

- Major iterations are new files from scratch, not patches.
- Snapshots of validation milestones live in the staging mirror
  under `_iterations/`.
- Every string lives in the `I18N` catalog in `index.html`; nothing
  is hardcoded in JS.
- Opacity floor is 0.75 unless there's a documented reason.
- Border radius is `var(--radius)` (4px) everywhere unless a
  specific component overrides it intentionally.

---

WoGL — World of GL · wogl.io · hello@wogl.io
