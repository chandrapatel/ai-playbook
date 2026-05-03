# AI Rules — Web Performance

Performance overrides for the web. Pair with `AI-RULES.md` (and `AI-RULES.web-development.md` for WordPress). Load on demand for projects where Core Web Vitals or asset budgets matter.

## Layout stability (CLS)
- Set `width` and `height` on every `<img>` and `<iframe>` so the browser can reserve space.
- Reserve space for late-loading content (ads, embeds) with `min-height` or `aspect-ratio`.
- Animate `transform` and `opacity` only — never `width`, `height`, `margin`, `padding`, or `top`/`left`.

## Largest Contentful Paint (LCP)
- LCP image: `fetchpriority="high"`, `loading="eager"`, `decoding="async"`. Use `<picture>` / `srcset` / `sizes`; serve AVIF, then WebP, then a JPEG/PNG fallback.
- Inline critical CSS in `<head>`. Load the rest async via `rel="preload"` + `onload="this.rel='stylesheet'"`.
- Preconnect only to origins required for LCP (CDN, font host). Skip nice-to-have third parties — connection budget is finite.
- Use `dns-prefetch` for third parties used later in the page; reserve `preconnect` for above-the-fold critical origins.

## Interaction (INP) and main thread
- Defer non-critical scripts. Prefer `defer` over `async` when DOM order matters.
- Break long tasks (>50 ms) with `await` boundaries, `setTimeout(0)`, or `scheduler.postTask()`.
- Use Intersection Observer to load below-fold widgets only when they enter the viewport.
- Apply debounce / throttle / `requestAnimationFrame` to scroll, resize, and pointer handlers.
- Read DOM measurements before writes inside the same frame to avoid layout thrashing.
- Move heavy computation to a Web Worker.

## Embeds and below-fold assets
- `loading="lazy"` on below-fold images and iframes.
- Facade pattern for heavy embeds (YouTube, maps, social widgets): render a static preview, swap to the real asset on user interaction.
- Don't inject scripts dynamically with `createElement` for ad/analytics tags; place them statically with `defer`/`async`.

## Fonts
- Max two web fonts. Prefer variable fonts when multiple weights or styles are needed.
- `font-display: swap` on every `@font-face`.
- Subset with `unicode-range` to skip glyph ranges you don't render.

## CSS delivery
- No `@import` in CSS — it serializes network requests.
- Minimize render-blocking CSS: inline critical, defer the rest.

## Caching headers
- Long-lived `Cache-Control: public, max-age=31536000, immutable` for fingerprinted assets (JS, CSS, images, fonts with hashed filenames).
- Short or revalidated caching for HTML; never serve HTML with `immutable`.

## WordPress specifics
- Defer non-critical scripts via the `script_loader_tag` filter; add `defer`/`async` selectively.
- Dequeue plugin assets not used on the current page with `wp_dequeue_script` / `wp_dequeue_style`.
- Enable a persistent object cache (Redis or Memcached). Use page caching for anonymous traffic.
- Disable `wp-cron` on front-end requests (`DISABLE_WP_CRON`); trigger via system cron instead.
- Cache slow queries via transients or the object cache. Cap `WP_Query` results; never `'posts_per_page' => -1`.
