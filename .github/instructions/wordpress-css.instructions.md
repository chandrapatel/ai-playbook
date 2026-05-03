---
description: "WordPress CSS guidance for scalable styling, RTL-friendly properties, and rendering performance. Use when editing CSS/SCSS for themes, blocks, and admin UI."
applyTo: "**/*.{css,scss,sass,pcss}"
---

# WordPress CSS Instructions

## Scalable styling
- Prefer low-specificity selectors.
- Use `:where()` for base element styling where it helps keep specificity low.
- Avoid shorthand properties with side effects in shared styles.
- Keep component outer spacing controlled by parent layout (`gap` or one-direction margins).

## Internationalization and layout
- Prefer logical properties (for example, `margin-inline`, `padding-block`, `text-align: start`) for RTL support.
- Use intrinsic layouts first (`clamp()`, `minmax()`) and media queries second.

## Performance and stability
- Keep `box-sizing: border-box` globally.
- Avoid `@import` in CSS.
- Favor transform/opacity animations over layout-triggering properties.
