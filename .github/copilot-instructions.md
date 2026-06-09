# AI Coding Agent Instructions — Radio Bahrain

Purpose: Make agents immediately productive in this static site + broadcast overlay repo. Keep changes minimal, respect RTL Arabic design, and avoid adding JS unless explicitly requested.

## Big Picture
- Two primary artifacts:
  - Landing page: [index.html](../index.html) — Arabic-first, animated, responsive.
  - Studio overlay: [OVERLAY_01.html](../OVERLAY_01.html) — programmatic banner states for live/break/ended.
- Pure HTML/CSS architecture; no build system, no JS frameworks. Deployment via GitHub Pages.
- Arabic-first and RTL: `lang="ar"`, `dir="rtl"`, Tajawal font, right-aligned layout.

## Key Conventions
- Design tokens: CSS variables define brand/colors, spacing, transitions.
  - Landing: `--primary-gradient`, `--secondary-gradient`, `--border-radius`, `--spacing-*` in `:root` (see [index.html](../index.html)).
  - Overlay brand: `--brand-red`, `--brand-red-ink`, `--banner-bg`, `--banner-ink` (see [OVERLAY_01.html](../OVERLAY_01.html)).
- Accessibility: ARIA roles/labels on visuals and nav, focus-visible styling, reduced motion support via `prefers-reduced-motion`.
- Responsiveness: heavy use of `clamp()`, media queries for 1024/768/480 widths; grid for features.
- Typography:
  - Landing loads Google Fonts Tajawal via `<link>`; fallbacks are system sans.
  - Overlay uses Arabic-centric font stack; keep `Tajawal`/`Cairo` where applicable.

## Developer Workflows
- Local preview: open [index.html](../index.html) or [OVERLAY_01.html](../OVERLAY_01.html) directly in a browser. Optional: use VS Code Live Server.
- Overlay state control: switch banner text via body attribute.
  - Programmatic: `document.body.setAttribute('data-state', 'soon'|'break'|'ended')`.
  - CSS selectors: `body[data-state="soon"|"break"|"ended"] .banner .<state>` control visibility.
- Deployment: GitHub Pages serves from this repo. Commit to main to update [README.md](../README.md) preview link.

## File/Folder Pointers
- HTML roots: [index.html](../index.html), [OVERLAY_01.html](../OVERLAY_01.html)
- Fonts/images: [assets/fonts](../assets/fonts), [screenshots](../screenshots)
- Project intro: [README.md](../README.md)

## Patterns To Follow
- Components on landing (examples in [index.html](../index.html)):
  - `.logo` with ripple/pulse and `.radio-waves` elements.
  - `.features` grid of `.feature-card` with hover top bar animation.
  - `.cta-button` with gradient hover and accessible role.
  - `.social-links` as circular, blurred cards.
- Overlay structure (in [OVERLAY_01.html](../OVERLAY_01.html)):
  - `.logo-circle` white disc with inline SVG mic + `.wordmark`.
  - `.socials` row with inline SVG icons (X, Instagram, YouTube, TikTok).
  - `.banner` fixed bottom block showing one of three `<h1>` messages.

## Integration Points
- External: Google Fonts (Tajawal). No JS/CDN libs.
- Inline SVG for icons; prefer editing the paths directly over adding external assets.

## Safe Changes & Examples
- Add a new overlay state:
  1. Add `<h1 class="text my_state">…</h1>` inside `.banner`.
  2. Add selector `body[data-state="my_state"] .banner .my_state{display:block}`.
- Adjust brand color: update `--brand-red`/`--brand-red-ink` in `:root`.
- Add a feature card to landing: duplicate `.feature-card` markup and keep ARIA labels.
- New social icon: add a `.social` span with inline SVG sized `22px` and stroke `white`.

## Quality Checks
- RTL correctness: verify alignment and `dir="rtl"` remains.
- Motion accessibility: confirm `prefers-reduced-motion` disables animations.
- Print styles: landing hides decoration and converts colors; leave overlay minimal.
- Performance: keep animations lightweight, avoid heavy shadows on mobile.

## Guardrails
- Do not introduce JS/frameworks unless explicitly requested.
- Preserve ARIA labels, roles, and focus-visible styles.
- Keep typography consistent with Tajawal/Cairo stacks.
- Use existing CSS variables and patterns; avoid inline styles.
