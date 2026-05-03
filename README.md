# AI Playbook

Tool-agnostic engineering rules for AI coding assistants. One source of truth, wired into each tool's expected filename.

## Files
- `AI-RULES.md` — universal rules. Always apply.
- `AI-RULES.web-development.md` — WordPress/web profile. Pair with the universal rules.
- `AI-RULES.web-performance.md` — Core Web Vitals, asset delivery, caching. Load when performance work is in scope.
- `AI-REFERENCES.web-development.md` — external URLs. On-demand only — most AI tools don't fetch URLs at runtime, so loading these by default just burns tokens.

## How to use with each AI tool

No mainstream AI tool auto-loads `AI-RULES.md`. Wire it in via the filename the tool expects. Symlinks keep one source of truth; copies are fine if your tool requires a real file.

| Tool | Expected file | Suggested setup |
|---|---|---|
| Claude Code | `CLAUDE.md` | `ln -s AI-RULES.md CLAUDE.md` |
| Cursor | `.cursor/rules/*.mdc` | Copy into `.cursor/rules/` |
| GitHub Copilot | `.github/copilot-instructions.md` | Copy into `.github/` |

For WordPress projects, also wire in `AI-RULES.web-development.md`. For performance-focused work, layer in `AI-RULES.web-performance.md` as well. Either concatenate the relevant profiles into the tool's main rules file, or place them alongside if the tool supports multiple rule files (e.g. Cursor's `.cursor/rules/`, Cline's per-folder `.clinerules`).

## Design principles
- **Imperative voice, plain markdown** — no XML tags, no tool-specific syntax. Works across Claude, GPT, Gemini, and smaller autocomplete models.
- **Override-only rules** — generic best practices that every modern LLM already follows are left out. Each line earns its tokens by changing default behavior.
- **Stable abstractions** — avoids version pins and project-specific details that go stale, so you rarely need to edit these files.
- **Profiles loaded on demand** — universal rules stay small; stack-specific rules layer in only when relevant.
