# AI Rules — Web Development (WordPress / 10up profile)

WordPress profile for plugins, themes, and Gutenberg work. Pair with `AI-RULES.md`. Distilled from 10up Engineering Best Practices — only the rules that override default LLM behavior; full guides linked in `AI-REFERENCES.web-development.md`.

## Stack constraints
- PHP 8.2+ minimum. Don't use syntax or APIs unsupported on 8.2.
- Prefer WordPress wrappers over raw PHP: `wp_json_encode()` over `json_encode()`, `wp_remote_*` over `curl`, etc.
- Use functional React components and hooks for block editor code.

## Security (non-negotiable)
- Sanitize every input with the context-appropriate `sanitize_*` function.
- Escape every output at the point of render with the context-appropriate `esc_*` function. Late escaping only — never escape earlier in the flow.
- Use `$wpdb->prepare()` for all SQL with dynamic values. Never interpolate.
- Require `current_user_can()` capability checks and `wp_verify_nonce()` on admin, REST, and AJAX actions.
- Client-side validation is UX only. Server-side validation is mandatory.
- Avoid `innerHTML` for dynamic content; use `textContent` or build with `document.createElement`. If HTML is unavoidable, parse it through `DOMParser` first.

## Queries
- Use `WP_Query` for post queries. Reach for `get_posts()` only when intentionally bypassing filters. Avoid raw `$wpdb` unless necessary.
- Pass `'no_found_rows' => true` whenever pagination isn't needed.
- Never use `'posts_per_page' => -1`. Set a sane cap (e.g. 500) even for "get all" cases.
- Avoid `post__not_in`. Query the broader set and filter in PHP.
- Use `isset()` on associative-keyed arrays rather than `in_array()` for hot-path lookups.

## PHP architecture
- Namespace every PHP file outside the WordPress template hierarchy with a vendor prefix (e.g. `TenUp\ClientName\Feature`).
- `use` declarations at the top of files; don't reference fully qualified names inline.
- Register hooks in dedicated methods, never inside `__construct()`. Decouples instantiation from side effects and keeps classes testable.
- Avoid singletons. Use dependency injection or factories.
- Never write to the database on front-end page requests. Confine writes to admin, cron, REST, or AJAX contexts.
- Pass `'autoload' => false` to `add_option()` for values not needed on every page load. Keep `wp_options` small.
- Define a `*_VERSION` constant per plugin/theme. Use it for asset cache-busting; bump before release.

## i18n
- Use `esc_html__()`, `esc_html_e()`, `esc_attr__()`, `esc_attr_e()` to translate and escape in one call.
- Pass literal strings to translation functions. Use `sprintf()` with `%s`/`%d` for dynamic values — never concatenate variables into the translated string.
- Text domains must be literal strings matching the plugin/theme slug.

## Caching and remote calls
- Cache every external HTTP request via `wp_cache_set()` or transients. Don't depend on uncached third-party calls.
- Prime object caches via scheduled or hook-driven warmers, not via visitor cache misses.

## JavaScript
- Tree-shake imports: `import map from 'lodash/map'`, not the full library.
- Avoid barrel files with wildcard re-exports.
- Cache DOM selections outside event handlers. Use event delegation on a parent for dynamic children.
- Debounce/throttle scroll, resize, and pointer events; use `requestAnimationFrame` for visual updates.
- Wrap code in closures. Don't add to `window`.
- Prefer Fetch over jQuery `$.ajax`. Use a small Fetch wrapper instead of axios unless you need cancellation, timeout, or interceptors.

## CSS
- Use `:where()` for bare element styles to keep specificity at zero.
- Cap selector specificity at 0,2,1.
- Apply margins in a single direction (top), or via parent `gap`. Components carry no outer margin.
- Use logical properties (`margin-inline`, `padding-block`, `text-align: start`) for automatic RTL.
- Set `box-sizing: border-box` globally at project start.
- Reach for media queries last. Prefer `clamp()`, `minmax()`, and intrinsic layouts.
- Avoid shorthand with side effects: `background-color` not `background`, `margin-inline` not `margin`.
- No `@import` in CSS — it serializes network requests.

## Formatting
- Blank line after a function's opening brace.
- In docblocks, separate `@param` and `@return` groups with a blank line.
- Inline comments only for non-obvious or critical logic.
- Defer to project lint/format tooling as final authority when present.

## Testing
Manual QA across wp-admin, editor, and front-end is the baseline. Automated tests encouraged for high-risk or reusable logic, not required for every plugin/theme.

## Related profiles
- `AI-RULES.web-performance.md` — Core Web Vitals, asset delivery, caching headers. Load when performance work is in scope.

## References
Full 10up guides and WordPress docs live in `AI-REFERENCES.web-development.md`. Load on demand only.
