# Kayloo brand assets (agency sign-up flow)

Extracted from the local staging site at http://kayloo.local:8000 with Playwright (Chrome channel, headless, viewport 1440x810, device scale factor 2). No application code, template, database or .env was modified.

## Logos

| File | Source | Natural size | Rendered on page |
|---|---|---|---|
| `kayloo-logo.svg` | `/static/kayloo/images/logos/kayloo-main.svg` (file: `app/static/kayloo/images/logos/kayloo-main.svg`), the logo displayed in the public header and on the sign-up page | 2304 x 684 px | 176 x 52 px in the home header (`base.html` line 49), 101 x 30 px on `/inscription` |
| `kayloo-logo-white.svg` | `/static/kayloo/logo.svg` | 2245 x 643 px | white version served for dark backgrounds |
| `kayloo-logo-admin.svg` | `/static/kayloo/logo.svg`, used by the admin header (`app/templates/admin/login.html` line 21) and the admin panel switcher (`app/templates/admin/layout.html` line 280) | 2245 x 643 px | 182 x 52 px on `/admin/login` |

Note on the logo choice. `/static/kayloo/logo.svg` is a white-only cut of the logo (`fill="white"`, 13 paths). On a white page it is invisible. The logo the site actually displays in the header of the home page and of the sign-up page is `/static/kayloo/images/logos/kayloo-main.svg` (2304 x 684, dark `#0E0F21` plus red `#DB0000`). That is `kayloo-logo.svg`. The white variant is kept as `kayloo-logo-white.svg` and is byte-identical to `kayloo-logo-admin.svg`.

The dashboard is behind login and was not visited. The admin header logo was read from the public `/admin/login` page and the admin layout template.

## Icons

One file per distinct inline `<svg>` found on the home page, the auth modal and the sign-up page. Every icon keeps its original path data; colors are the computed values at capture time (resolved from `currentColor`), and all use `viewBox="0 0 24 24"`.

| File | Size | Stroke/fill | Where it appears | Template source |
|---|---|---|---|---|
| `arrow-left.svg` | 14 x 14 | `#D60000` | sign-up page, "Retour" pill | `app/templates/kayloo/public/pages/inscription.html` line 21 |
| `arrow-right.svg` | 15 x 15 | `#FFFFFF` | home page, "Voir tous les bons plans" CTA on the red section | `app/templates/kayloo/public/index.html` (bons plans block) |
| `home.svg` | 9 x 9 | `#FFFFFF` | home page, bon plan card: property type | `app/templates/kayloo/public/index.html` |
| `bed.svg` | 9 x 9 | `#FFFFFF` | home page, bon plan card: bedrooms | `app/templates/kayloo/public/index.html` |
| `expand.svg` | 9 x 9 | `#FFFFFF` | home page, bon plan card: land area | `app/templates/kayloo/public/index.html` |
| `bath.svg` | 9 x 9 | `#FFFFFF` | home page, bon plan card: bathrooms | `app/templates/kayloo/public/index.html` |
| `pin.svg` | 12 x 12 | `#D60000` | home page, bon plan card: city | `app/templates/kayloo/public/index.html` |
| `check.svg` | 9 x 9 | `#15803D` | home page, bon plan card: availability confirmed | `app/templates/kayloo/public/index.html` |
| `close.svg` | 14 x 14 | `#55555F` | auth modal close button | `app/templates/components/web_auth.html` (panel macro) |
| `check-circle.svg` | 52 x 52 | `#16A34A` with white tick | auth modal and sign-up success screen | `app/templates/components/web_auth.html` (`check_icon` macro) |

White icons are white because they sit on the red bons-plans section or on photo thumbnails. They are invisible on a white background, so put them on the matching background in the video or swap the stroke color if needed.

Not extracted, deliberately:

- The header and nav use Font Awesome webfont icons (`<i class="fas fa-angle-down">`, `fa-bullhorn`, `fa-bars`), not inline SVG, so there is no SVG markup to copy. Redrawing them by hand is outside the brief.
- The hero has no inline SVG icon.
- The dashboard/sidebar needs login, so it was skipped. The admin layout template (`app/templates/admin/layout.html`) does contain 9 inline SVGs if they are needed later.

## Documents

`documents/` already contained the three dummy PDFs. Nothing was copied, each file was checked in place.

| File | Size | Header | Trailer |
|---|---|---|---|
| `documents/CNI.pdf` | 33758 bytes | `%PDF` | `%%EOF` |
| `documents/NINEA.pdf` | 39611 bytes | `%PDF` | `%%EOF` |
| `documents/RCCM.pdf` | 41289 bytes | `%PDF` | `%%EOF` |

## Validation

- XML parse with `xml.etree.ElementTree`: 13 of 13 SVG files pass (3 logos, 10 icons).
- Render check in Chrome: 13 of 13 load with the expected intrinsic size (icons at 9 to 52 px, logos at 2304 x 684 and 2245 x 643).
- PDFs: 3 of 3 have the `%PDF` magic bytes and the `%%EOF` trailer.

Reproduction scripts and raw capture data live in `.agents/scripts/assets-scout/` (`extract.py`, `build.py`, `verify_render.py`, `icons.json`, `render-check.json`).
