# Site Migration Plan: intensions.app → eudaimonialabs.org

## Overview

Migrate the Jekyll site from a single inTensions app site to a full multi-app company site for Eudaimonia Labs LLC. The domain is already pointed to `eudaimonialabs.org` via the CNAME file.

## Final URL Structure

| URL                   | Content                                                                |
| --------------------- | ---------------------------------------------------------------------- |
| `/`                   | Eudaimonia Labs company landing page                                   |
| `/intensions`         | inTensions app landing page (existing, moved)                          |
| `/intensions/privacy` | inTensions privacy policy (existing, moved)                            |
| `/verbatim`           | Verbatim app landing page (new, parchment theme)                       |
| `/verbatim/privacy`   | Verbatim privacy policy (new, copied from inTensions with name change) |

---

## Phase 1: Restructure Existing Files

### 1.1 Move inTensions content into `/intensions/` subfolder

**Create** `intensions/index.markdown`:
- Copy current `index.markdown` content verbatim
- Update any URLs from site-root variables to app-specific ones
- Update `layout: landing` to include `body_class: intensions` (for palette scoping)

**Create** `intensions/privacy.markdown`:
- Copy current `privacy.markdown` content verbatim
- Change only the `permalink:` front matter from `/privacy/` to `/intensions/privacy/`
- **DO NOT ALTER ANY LEGAL CONTENT**

**Delete** (or replace with Eudaimonia Labs content):
- `index.markdown` → becomes the Eudaimonia Labs company landing page
- `privacy.markdown` → content is now in `intensions/privacy.markdown`

---

## Phase 2: Update `_config.yml`

Change site metadata to be company-wide rather than inTensions-specific:

```yaml
title: Eudaimonia Labs
email: hello@intensions.app
description: >-
  Eudaimonia Labs LLC - In support of human flourishing
baseurl: ""
url: "https://eudaimonialabs.org"
intensions_google_play_url: "https://play.google.com/store/apps/details?id=com.eudaimonialabs.inTensions"
# verbatim_google_play_url: not yet available
```

---

## Phase 3: Update Layouts to Support Per-Page Body Classes

### 3.1 Update `_layouts/landing.html`

Add support for `body_class` front matter variable on the `<body>` tag so Verbatim pages get their own palette scope:

```html
<body class="{{ page.body_class | default: '' }}">
```

### 3.2 Update `_layouts/page-with-landing-title.html`

Same change applied to the privacy policy layout.

---

## Phase 4: Update SCSS for Multi-App Styling

### 4.1 `_sass/custom-styles.scss` changes

**Current state**: All CSS variables in `:root` are inTensions-specific.

**Changes needed**:
- Keep inTensions variables as the `:root` default
- Add a `body.verbatim` scope block with the Verbatim palette:
  ```scss
  body.verbatim {
    --background-dark: #E8E0D2;  // Vellum
    --primary-surface: #D8CEB7;  // Aged Parchment
    --text-light: #2B2118;       // Iron Gall Ink
    --accent-peach: #D4AF37;     // Gold Leaf
    --error-red: #C44D34;        // Rubric Red
    // Additional colors:
    --verbatim-azure: #5D7C89;
    --verbatim-surface-highlight: #F2EBD9;
    --verbatim-text-secondary: #594A3C;
    --verbatim-text-muted: #8B6F69;
    --verbatim-border: #B0A38E;
  }
  ```
- Add Verbatim-specific component styles (journey cards, verse refs, level status tile mock)

### 4.2 Google Fonts

Add Roboto (for Verbatim) alongside Atkinson Hyperlegible, scoped to `body.verbatim`.

---

## Phase 5: Update Footer

### 5.1 `_includes/footer.html` changes

Make privacy link and email context-aware using Jekyll page variables:

```html
<a href="{{ page.privacy_url | default: '/intensions/privacy/' }}">Privacy Policy</a>
```

Each page's front matter sets `privacy_url`:
- `/intensions/index.markdown` → `privacy_url: /intensions/privacy/`
- `/verbatim/index.markdown` → `privacy_url: /verbatim/privacy/`
- etc.

---

## Phase 6: Create New Pages

### 6.1 `verbatim/index.markdown` — Verbatim Landing Page

**Palette**: Verbatim parchment theme (body class `verbatim`)
**Layout**: `landing`
**Key UI Elements to mock** (inspired by actual Verbatim dashboard screen):

1. **Header**: "Verbatim" as large title, tagline "Memorize what matters"
2. **CTA Button**: "Coming Soon" (styled like the app's primary button, no link)
3. **Mock Dashboard UI**:
   - A mock "Level Status Tile" (e.g., "Seeker | Level 1" with a circular progress indicator — styled as parchment card with rounded corners, icon)
   - A "Active Journeys" section header
   - 1–2 journey cards (e.g., "The Sermon on the Mount" — Matthew 5–7, with verse count and progress)
   - A "Daily Walk" section (daily verse review tile)
4. **The key insight** from inTensions comparison: the mock list items (todo items) communicate the app's value proposition through their titles. Do the same for Verbatim — the journey title/content communicates what the app helps you do.

**Sample mock content for journey cards** (to be refined by user):
- Journey: "Romans 8 · 39 verses · 0% memorized"
- Journey: "The Lord's Prayer · Matthew 6:9–13 · 6 verses"
- Daily Walk: "John 3:16 · Due today"

### 6.2 `verbatim/privacy.markdown` — Verbatim Privacy Policy

- Copy `intensions/privacy.markdown` exactly
- Replace all instances of "inTensions" with "Verbatim" (app name only)
- Change `permalink: /intensions/privacy/` to `permalink: /verbatim/privacy/`
- **DO NOT ALTER ANY OTHER LEGAL CONTENT**

### 6.3 Root `index.markdown` — Eudaimonia Labs Company Page

**Palette**: TBD — needs decision from user
**Layout**: `landing`

**Content structure**:
1. **Header**: "Eudaimonia Labs" (or stylized logo/wordmark)
2. **Tagline**: Communicates the company's design philosophy — "Simple, privacy-first tools for a meaningful life" (placeholder — user to finalize)
3. **Design Philosophy Section**: Drawing from inTensions "No ads. No AI. No notifications. No nonsense." + Verbatim consent dialog "We don't participate in surveillance capitalism." — this is the core philosophy
4. **App Cards**: Two cards/sections:
   - inTensions: Brief description, CTA → `/intensions/`
   - Verbatim: Brief description, CTA → `/verbatim/` (Coming Soon badge)
5. **Footer**: Contact info

---

## Phase 7: Update inTensions App

Update the inTensions Flutter app's privacy policy URL from `intensions.app/privacy` to `eudaimonialabs.org/intensions/privacy`.

**File to update**: `C:/Users/t8/Sync/projects/intensions/lib/features/privacy/dialogs/privacy_consent_dialog.dart`

**Change**: Line 86 — `recognizer: createRecognizer('https://intensions.app/privacy')`
→ `'https://eudaimonialabs.org/intensions/privacy'`

---

## Open Questions / Decisions Needed from User

1. **Eudaimonia Labs home page palette**: What color scheme should the company landing page use? Options:
   - A neutral/minimal scheme (white, black, natural tones)
   - A "meta" palette that incorporates both app palettes
   - The user should decide; no implementation should proceed without this decision

2. **Footer behavior**: Should the Eudaimonia Labs root page footer link to a general contact or one of the app privacy policies?

3. **Company tagline**: What is the official Eudaimonia Labs tagline or mission statement for the home page?

---

## File Change Summary

| File                                    | Action  | Notes                                                  |
| --------------------------------------- | ------- | ------------------------------------------------------ |
| `index.markdown`                        | Rewrite | Becomes Eudaimonia Labs home page                      |
| `privacy.markdown`                      | Delete  | Replaced by `intensions/privacy.markdown`              |
| `intensions/index.markdown`             | Create  | Move current root index content                        |
| `intensions/privacy.markdown`           | Create  | Copy privacy.markdown, change permalink only           |
| `verbatim/index.markdown`               | Create  | New Verbatim landing page                              |
| `verbatim/privacy.markdown`             | Create  | Copy intensions/privacy.markdown, change app name only |
| `_config.yml`                           | Update  | Company-wide metadata                                  |
| `_layouts/landing.html`                 | Update  | Add body_class injection                               |
| `_layouts/page-with-landing-title.html` | Update  | Add body_class injection                               |
| `_includes/footer.html`                 | Update  | Dynamic privacy link per page                          |
| `_sass/custom-styles.scss`              | Update  | Add Verbatim palette + component styles                |
| `intensions` Flutter app                | Update  | Privacy policy URL                                     |
