# Tech

## Technologies Used

| Technology   | Version                   | Purpose                                |
| ------------ | ------------------------- | -------------------------------------- |
| Jekyll       | via github-pages gem ~232 | Static site generator                  |
| GitHub Pages | —                         | Hosting at eudaimonialabs.org          |
| Minima       | ~2.5                      | Base Jekyll theme (heavily overridden) |
| SCSS         | —                         | Styling (compiled by Jekyll)           |
| jekyll-feed  | ~0.12                     | RSS feed plugin                        |

## Development Setup

Local development:
```
bundle exec jekyll serve
```

Deployment: Push to GitHub — GitHub Actions / Pages auto-builds.

## Technical Constraints

- **GitHub Pages gem** is pinned to `gem "github-pages", "~> 232"` — limits available Jekyll plugins to the whitelist
- **No custom plugins** beyond the allowlist (jekyll-feed is allowed)
- **No server-side logic** — everything must be static
- **Jekyll `_config.yml`** is not hot-reloaded in dev; requires server restart after changes

## Custom Variables in `_config.yml`

The site uses custom variables accessible in templates via `{{ site.variable_name }}`:
- `site.title` — site/app name
- `site.email` — contact email
- `site.google_play_url` — Play Store link for the primary app
- Need to expand for multi-app architecture (see Context for planned approach)

## File Organization Conventions

- All pages use `index.markdown` inside named folders to get clean URLs (e.g., `/intensions/index.markdown` → `/intensions/`)
- Privacy policy pages use `privacy.markdown` inside app folders for `/app/privacy`
- Custom SCSS goes in `_sass/custom-styles.scss`, imported from `assets/main.scss`
- Layouts in `_layouts/`, partials in `_includes/`

## Styling Approach

- CSS custom properties (variables) defined in `:root` for the default inTensions palette
- Verbatim pages override palette via CSS scoped to body class (e.g., `body.verbatim`)
- The `landing.html` layout supports a `body_class` front matter variable injection pattern
- Google Fonts (Atkinson Hyperlegible) loaded via `@import` in SCSS

## Privacy Policy Rules (CRITICAL)

**NEVER write or generate new privacy policy content.** Privacy policies are legal documents prepared by the user's legal team.

The ONLY permitted modification to privacy policies is:
- Changing the **app name** where it is referenced (e.g., replacing "inTensions" with "Verbatim")
- Changing the **permalink** front matter to match the correct URL path

All other content, legal language, and structure must remain exactly as-is from the source `privacy.markdown`.
