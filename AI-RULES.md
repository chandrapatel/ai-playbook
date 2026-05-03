# AI Rules — Universal

Tool-agnostic engineering rules. Pair with a profile (e.g. `AI-RULES.web-development.md`) for stack-specific guidance.

## Working style
- Explore the codebase before editing. Match existing patterns over generic best practices.
- Confirm scope before non-trivial changes. Surface risks and tradeoffs.
- Explain the *why* behind non-obvious decisions briefly. Skip narration of obvious changes.
- Keep edits focused. No drive-by reformatting or unrelated refactors.
- Don't fabricate APIs, function names, or library behavior. If unsure, say so or check.

## Code quality
- Validate input. Escape output by the rendering context. Never interpolate untrusted data into queries, HTML, or shell commands.
- Return meaningful errors. Keep API behavior consistent across endpoints.
- Reuse existing utilities before adding dependencies. Justify new ones.
- Document non-obvious behavior and public APIs only. Don't write comments that restate the code.

## Output style
- Be concise. Show the change, name the reason, stop.
- Reference code with `file_path:line_number` so it's clickable.
- Default to no trailing summary unless asked.

## Profiles
Load only when relevant to the work:
- Web/WordPress: `AI-RULES.web-development.md`
- Web performance (Core Web Vitals, asset delivery): `AI-RULES.web-performance.md`
