# Architecture

## Site Overview

Static Jekyll site hosted on GitHub Pages at `eudaimonialabs.org`. CNAME file points the custom domain correctly.

## Source Code Paths

- **Root**: `c:/Users/t8/Sync/projects/eudaimonia labs/inTensions-app.github.io`
- **App projects** (for reference only, not edited by this site):
  - inTensions: `C:/Users/t8/Sync/projects/intensions`
  - Verbatim: `C:/Users/t8/Sync/projects/verbatim`

## Jekyll Site Structure

```
/
├── _config.yml               # Site-wide config
├── _layouts/
│   ├── landing.html          # Full-screen landing (no header nav)
│   ├── page-with-landing-title.html  # Landing-style title + content body
│   └── simple.html           # Minimal wrapper
├── _includes/
│   └── footer.html           # Shared footer
├── _sass/
│   └── custom-styles.scss    # All custom SCSS
├── assets/
│   └── main.scss             # Entry point (imports minima + custom-styles)
├── index.markdown            # / — Eudaimonia Labs company landing page
├── intensions/
│   ├── index.markdown        # /intensions — inTensions app landing page
│   └── privacy.markdown      # /intensions/privacy — inTensions privacy policy
├── verbatim/
│   ├── index.markdown        # /verbatim — Verbatim app landing page
│   └── privacy.markdown      # /verbatim/privacy — Verbatim privacy policy
├── 404.html
├── CNAME                     # eudaimonialabs.org
└── Gemfile
```

## Planned URL Structure

| URL | Purpose |
|-----|---------|
| `/` | Eudaimonia Labs company landing page |
| `/intensions` | inTensions app landing page |
| `/intensions/privacy` | inTensions privacy policy |
| `/verbatim` | Verbatim app landing page |
| `/verbatim/privacy` | Verbatim privacy policy |
| `/about` | About Eudaimonia Labs (future) |

## Layouts

### `landing.html`
Full-screen no-nav layout. Used for app landing pages. Contains only `<main>` and footer.

### `page-with-landing-title.html`
Used for privacy policy pages. Renders page title as large header, then content in a centered `max-width: 800px` wrapper.

### `simple.html`  
Minimal wrapper with `.wrapper` div.

## Styling System

- Theme: `minima` base, heavily overridden via `_sass/custom-styles.scss`
- Each app section has its own CSS color variables scoped to body class or specific page selectors
- **inTensions palette** (default site palette):
  - Background: `#466365` (dark teal)
  - Primary surface: `#648E90`
  - Text: `#F7FFF7` (mint)
  - Accent: `#F9E1C8` (peach)
  - Error: `#FF6B6B`
- **Verbatim palette** (scoped to Verbatim pages):
  - Background: `#E8E0D2` (Vellum)
  - Surface: `#D8CEB7` (Aged Parchment)
  - Text: `#2B2118` (Iron Gall Ink)
  - Gold: `#D4AF37`
  - Rubric Red: `#C44D34`
  - Azure: `#5D7C89`
- **Eudaimonia Labs home palette**: TBD — to be decided with user

## Key Technical Decisions

1. **Jekyll collections not required** — simple folder structure with `index.markdown` files works for GitHub Pages
2. **Per-page body class injection** — Verbatim pages need their own color palette; this can be done via a `body_class` front matter variable passed to layouts
3. **Privacy policies**: Copied from existing `privacy.markdown` with only app name references changed — never written from scratch
4. **No redirects from old `/privacy/`** — old inTensions app will be updated to point to `/intensions/privacy`

## Component Relationships

```
_config.yml
  ↓ provides site.title, site.email, site.google_play_url, etc.
  
_layouts/landing.html
  ← used by: /index, /intensions/index, /verbatim/index
  → includes: head.html (from minima), footer.html

_layouts/page-with-landing-title.html  
  ← used by: /intensions/privacy, /verbatim/privacy
  → includes: head.html, footer.html

_sass/custom-styles.scss
  ← imported by: assets/main.scss
  → defines: CSS variables, component styles, per-palette overrides
```
