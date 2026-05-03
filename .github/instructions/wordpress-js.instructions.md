---
description: "WordPress JavaScript and block editor rules for safety, performance, and architecture. Use when editing JS/TS for frontend behavior or Gutenberg blocks."
applyTo: "**/*.{js,jsx,ts,tsx,mjs,cjs}"
---

# WordPress JavaScript Instructions

## Security and DOM safety
- Avoid injecting untrusted HTML via `innerHTML`.
- Prefer `textContent` or explicit element creation.
- If HTML is unavoidable, sanitize or parse safely before insertion.

## Architecture
- Use functional React components and hooks for block editor code.
- Avoid adding globals to `window`.
- Wrap standalone scripts in closures/modules.
- Avoid barrel files with wildcard re-exports.

## Networking and performance
- Prefer Fetch wrappers over jQuery `$.ajax` unless legacy code requires it.
- Tree-shake imports (for example, `lodash/map` over full-package imports).
- Cache DOM selections outside hot event loops.
- Use delegation for dynamic children when appropriate.
- Debounce or throttle resize/scroll/pointer handlers.
- Use `requestAnimationFrame` for visual update work.
