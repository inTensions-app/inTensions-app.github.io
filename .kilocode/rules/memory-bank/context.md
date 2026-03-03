# Context

## Current Work Focus

The site migration from `intensions.app` → `eudaimonialabs.org` multi-app site is **complete**. All pages and infrastructure changes have been implemented.

## Recent Changes (2026-03-03)

### Files Created
- `intensions/index.markdown` — inTensions app landing page at `/intensions/`; uses `body_class: intensions`, `privacy_url: /intensions/privacy/`, and `site.intensions_google_play_url`
- `intensions/privacy.markdown` — inTensions privacy policy at `/intensions/privacy/`; exact copy of old root `privacy.markdown` with only front matter changed
- `verbatim/index.markdown` — Verbatim app landing page at `/verbatim/`; uses `body_class: verbatim`, medieval manuscript UI mock (level status tile, journey cards, daily walk tile)
- `verbatim/privacy.markdown` — Verbatim privacy policy at `/verbatim/privacy/`; copy of inTensions policy with app name changed to "Verbatim" and front matter updated

### Files Modified
- `index.markdown` — Completely rewritten as Eudaimonia Labs company landing page; `body_class: eudaimonia`, two app cards (inTensions + Verbatim)
- `_config.yml` — `title` → `Eudaimonia Labs`, `description` → company-wide description, `url` → `https://eudaimonialabs.org`, `google_play_url` → `intensions_google_play_url`
- `_layouts/landing.html` — `<body>` → `<body class="{{ page.body_class | default: '' }}">`
- `_layouts/page-with-landing-title.html` — Same `body_class` injection as landing.html
- `_includes/footer.html` — Privacy link now uses `{{ page.privacy_url | default: '/intensions/privacy/' }}`
- `_sass/custom-styles.scss` — Added Roboto to Google Fonts import; added `body.verbatim` palette + all Verbatim component styles; added `body.eudaimonia` palette + company page card styles

### Files Deleted
- `privacy.markdown` (root) — now lives at `intensions/privacy.markdown`

## Next Steps

1. **Update inTensions Flutter app** — Change privacy policy URL from `https://intensions.app/privacy` to `https://eudaimonialabs.org/intensions/privacy` in `C:/Users/t8/Sync/projects/intensions/lib/features/privacy/dialogs/privacy_consent_dialog.dart` line 86
2. **Test the site locally** — Run `bundle exec jekyll serve` and verify all pages render correctly with correct palettes
3. **Verify `/verbatim/privacy/` redirects** — Verbatim app will eventually need to link to this URL when launched
4. **Eudaimonia Labs home page palette** — A dark forest green (`#2D3B35`) is implemented; user may want to adjust

## Known Issues / Decisions Pending

- **Eudaimonia Labs home page palette**: Implemented with dark forest green (`#2D3B35`) bridging teal and warm parchment. User should confirm this feels right.
- **inTensions app update**: The Flutter app's privacy URL still points to old domain — needs to be changed (see Next Steps above)
- **Verbatim not yet on Play Store**: `verbatim_google_play_url` not in `_config.yml` yet — add when app launches

## CSS Architecture

- `:root` (no body class) — inTensions palette (default) — `#466365` background
- `body.intensions` — explicitly sets same as :root (falls through, front matter sets class for clarity)
- `body.verbatim` — Vellum/parchment palette, Roboto font, full dashboard component styles
- `body.eudaimonia` — Dark forest palette, Atkinson Hyperlegible, app card styles
- All pages set `body_class` in front matter + `privacy_url` for dynamic footer
