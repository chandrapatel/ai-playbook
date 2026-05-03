---
description: "WordPress PHP rules for security, queries, architecture, i18n, caching, formatting, and testing. Use when editing PHP in plugins, themes, admin, REST, AJAX, or Gutenberg server-side code."
applyTo: "**/*.php"
---

# WordPress PHP Instructions

## Security
- Sanitize every input with the context-appropriate `sanitize_*` function.
- Escape every output at render time with the context-appropriate `esc_*` function.
- Use `$wpdb->prepare()` for all SQL with dynamic values. Never interpolate.
- Require `current_user_can()` and `wp_verify_nonce()` on admin, REST, and AJAX actions.
- Client-side validation is UX only; server-side validation is mandatory.

## Queries
- Use `WP_Query` for post queries.
- Use `get_posts()` only when intentionally bypassing filters.
- Avoid raw `$wpdb` unless needed.
- Set `'no_found_rows' => true` when pagination is not needed.
- Avoid `'posts_per_page' => -1`; set a sane cap.
- Avoid `post__not_in`; query a broader set and filter in PHP.
- Prefer `isset()` on associative keyed lookups for hot paths.

## Architecture
- Namespace PHP files outside WordPress template hierarchy with a vendor prefix.
- Keep `use` declarations at the top of files.
- Register hooks in dedicated methods, not in `__construct()`.
- Avoid singletons; prefer dependency injection or factories.
- Do not write to the database on front-end page requests.
- Pass `'autoload' => false` to `add_option()` for values not needed on every request.
- Define and use a `*_VERSION` constant for asset cache busting.

## i18n
- Prefer escaped translation helpers like `esc_html__()`, `esc_html_e()`, `esc_attr__()`, `esc_attr_e()`.
- Pass literal strings to translation functions.
- Use `sprintf()` for dynamic placeholders.
- Keep text domains literal and matched to plugin or theme slug.

## Caching and remote calls
- Cache external HTTP requests with transients or object cache.
- Prime caches through scheduled or hook-driven warmers.

## Formatting and testing
- Keep comments for non-obvious logic only.
- Follow project lint and formatting tooling when present.
- Manual QA across wp-admin, editor, and front-end is baseline.
- Add automated tests for high-risk or reusable logic where practical.
