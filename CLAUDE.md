# AI Rules - Universal

Tool-agnostic engineering rules for this project.

## Working style
- Explore the codebase before editing. Match existing patterns over generic best practices.
- Confirm scope before non-trivial changes. Surface risks and tradeoffs.
- Explain the why behind non-obvious decisions briefly. Skip narration of obvious changes.
- Keep edits focused. No drive-by reformatting or unrelated refactors.
- Do not fabricate APIs, function names, or library behavior. If unsure, say so or check.

## Code quality
- Validate input. Escape output by the rendering context. Never interpolate untrusted data into queries, HTML, or shell commands.
- Return meaningful errors. Keep API behavior consistent across endpoints.
- Reuse existing utilities before adding dependencies. Justify new ones.
- Document non-obvious behavior and public APIs only. Do not write comments that restate the code.

## Output style
- Be concise. Show the change, name the reason, stop.
- Reference code with `file_path:line_number` so it is clickable.
- Default to no trailing summary unless asked.

## Web/WordPress core
- PHP 8.2+ minimum.
- Prefer WordPress wrappers and APIs over raw PHP alternatives.
- Use functional React components and hooks for block editor code.
- Security is mandatory: sanitize input, escape output late, use `$wpdb->prepare()` for dynamic SQL, and require capability plus nonce checks on admin/REST/AJAX actions.
- Server-side validation is required even when client-side validation exists.
- Namespace PHP files outside template hierarchy.
- Register hooks in dedicated methods, not in constructors.
- Avoid singletons; prefer dependency injection or factories.
- Avoid writes during front-end page requests; write in admin, cron, REST, or AJAX contexts.
- Use literal strings in translation functions and keep text domains literal and slug-matched.

## Scoped guidance

Load the relevant file when editing files of that type:
- PHP (`**/*.php`): @.claude/rules/wordpress-php.md
- JS/TS (`**/*.{js,jsx,ts,tsx,mjs,cjs}`): @.claude/rules/wordpress-js.md
- CSS/SCSS (`**/*.{css,scss,sass,pcss}`): @.claude/rules/wordpress-css.md
