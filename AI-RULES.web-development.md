# Web Development Platform Profile

<scope>
Use with `AI-RULES.md` for WordPress projects (plugins, themes, block editor).
</scope>

<platform_profile>
## Stack
- WordPress CMS, PHP, JavaScript, React, HTML, CSS.
- Project types: plugins, themes, and Gutenberg/block-editor work.

## Standards
- Follow WordPress-first architecture (hooks, filters, templates, block metadata, enqueueing).
- Minimum supported PHP version: **8.2+**.
- Prefer WordPress wrappers/helpers over raw PHP equivalents when available (example: `wp_json_encode()` over `json_encode()`).

## Security and Data Handling
- Sanitize all input and escape all output contextually.
- Use capability checks and nonces for admin, REST, and AJAX actions.
- Use prepared SQL; never interpolate dynamic query values directly.

## Frontend and Blocks
- Use functional React components and hooks.
- Keep block editor logic and front-end rendering concerns separated.
- Treat server-side authorization/validation as mandatory even with client-side checks.
- Keep CSS modular, semantic, responsive, and accessible.

## Build and Workflow
- Node/npm + 10up Toolkit for build/lint/format; Composer for PHP dependencies.
- Prefer toolkit defaults; customize webpack/postcss only when required.
- Classify work early (plugin, theme, shared block/editor) and reuse existing project patterns.
- Validate manually across wp-admin/editor and front-end before considering changes complete.

## Formatting and Documentation Preferences
- Add a blank line after the function opening brace.
- In function docblocks, add a blank line between `@param` and `@return` groups.
- Add inline comments only for critical or non-obvious logic.
- Mirror local file formatting first; keep edits focused and avoid unrelated reformatting.
- Use lint/format tooling as final authority when available.

## Testing Policy
- Manual QA is acceptable and expected.
- Automated tests are encouraged for high-risk or reusable logic, but not mandatory for every plugin/theme.

## Common Commands
- npm run build
- npm run start
- npm run lint-js
- npm run lint-style
- npm run format-js
- composer install

## Performance and Delivery
- Optimize and cache expensive WordPress queries.
- Keep bundles lean and split assets by editor/admin/front-end context.
</platform_profile>

<references>
Use team/public guidance as source-of-truth when available:
- WordPress and PHP: https://10up.github.io/Engineering-Best-Practices/php/
- CSS: https://10up.github.io/Engineering-Best-Practices/css/
- JavaScript: https://10up.github.io/Engineering-Best-Practices/javascript/
- Performance: https://10up.github.io/Engineering-Best-Practices/performance/
- HTML Markup: https://10up.github.io/Engineering-Best-Practices/markup/
- 10up Toolkit README: https://raw.githubusercontent.com/10up/10up-toolkit/refs/heads/develop/packages/toolkit/README.md
- WordPress Developer Documentation: https://developer.wordpress.org/
</references>
