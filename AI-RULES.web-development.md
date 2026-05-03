# AI Rules — Web Development (WordPress)

WordPress profile for plugins, themes, and Gutenberg work. Pair with `AI-RULES.md`.

## Stack constraints
- PHP 8.2+ minimum. Don't use syntax or APIs unsupported on 8.2.
- Prefer WordPress wrappers over raw PHP: `wp_json_encode()` over `json_encode()`, `wp_remote_*` over `curl`, etc.
- Use functional React components and hooks for block editor code.

## Security (non-negotiable)
- Sanitize every input with the context-appropriate `sanitize_*` function.
- Escape every output at the point of render with the context-appropriate `esc_*` function.
- Use `$wpdb->prepare()` for all SQL with dynamic values. Never interpolate.
- Require `current_user_can()` capability checks and `wp_verify_nonce()` on admin, REST, and AJAX actions.
- Client-side validation is UX only. Server-side validation is mandatory.

## Architecture
- Work through WordPress conventions: hooks, filters, templates, block metadata, proper enqueueing.
- Separate block editor logic from front-end render concerns.
- Cache expensive queries. Watch for N+1 patterns in loops.

## Formatting
- Blank line after a function's opening brace.
- In docblocks, separate `@param` and `@return` groups with a blank line.
- Inline comments only for non-obvious or critical logic.
- Defer to project lint/format tooling as final authority when present.

## Build and tooling
- 10up Toolkit for JS/CSS build, lint, and format. Composer for PHP dependencies.
- Use toolkit defaults. Customize webpack/postcss only when required.

### Common commands
- `npm run build` / `npm run start`
- `npm run lint-js` / `npm run lint-style`
- `npm run format-js`
- `composer install`

## Testing
- Manual QA across wp-admin, block editor, and front-end is expected before declaring work done.
- Automated tests encouraged for high-risk or reusable logic. Not required for every plugin/theme.

## References
External documentation links live in `AI-REFERENCES.web-development.md`. Load on demand only.
