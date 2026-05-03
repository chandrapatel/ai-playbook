# AI Playbook

Tool-agnostic engineering rules for AI coding assistants. Source-of-truth rules live in the repo root; tailored entry points for each tool sit in the locations those tools expect.

## Source-of-truth files
- `AI-RULES.md` — universal rules. Always apply.
- `AI-RULES.web-development.md` — WordPress profile. Pair with the universal rules.
- `AI-RULES.web-performance.md` — Core Web Vitals, asset delivery, caching. Load when performance work is in scope.
- `AI-REFERENCES.web-development.md` — external URLs. On-demand only — most AI tools don't fetch URLs at runtime, so loading these by default just burns tokens.

## Tool wiring

Each tool loads rules from a different filename and supports different ways to scope rules to file types. Rather than symlinking (which loses tool-specific frontmatter and import syntax), this repo ships tailored entry points for each tool.

> **Note:** The root `AI-RULES.*.md` files and the tool-tailored files (`CLAUDE.md` + `.claude/rules/`, `.github/copilot-instructions.md` + `.github/instructions/`) are **not strict mirrors**. The root files are the tool-agnostic baseline. The per-tool variants were reviewed and refined separately by each AI to take advantage of native path-scoping and to minimize context / token cost, so wording, ordering, and even rule coverage can intentionally differ.
>
> - **Root `AI-RULES.*.md`** — reference baseline. Developers can adopt them as-is, copy into a new project, or modify to fit a different stack.
> - **Tool-tailored files** — active, working configurations for Claude Code and Copilot in this repo. Edit these to change behavior in those tools; don't expect them to track the root files line-for-line.

### Claude Code
- `CLAUDE.md` — main entry. Universal + WordPress core rules.
- `.claude/rules/wordpress-{php,js,css}.md` — language-scoped rules, pulled in via `@.claude/rules/...` import lines in `CLAUDE.md`.

### GitHub Copilot
- `.github/copilot-instructions.md` — main entry.
- `.github/instructions/wordpress-{php,js,css}.instructions.md` — language-scoped rules. Each file has `applyTo: "**/*.{ext}"` frontmatter so Copilot loads the right one automatically based on the file being edited.

### Cursor
Not yet wired up. Equivalent layout would be `.cursor/rules/*.mdc` with `globs:` frontmatter mirroring the Copilot `applyTo` patterns.

## Why path-scoped rules

Both Claude Code's `@`-imports and Copilot's `applyTo` frontmatter let the assistant load only the rules relevant to the file under edit. Editing PHP loads the PHP rules; editing CSS loads the CSS rules. The universal and WordPress-core rules in the main entry file are always present; the per-language sets layer in on demand. This keeps prompt tokens low without giving up depth.

## Design principles
- **Imperative voice, plain markdown** — no XML tags. The source-of-truth files stay tool-agnostic so they work in any AI assistant.
- **Override-only rules** — generic best practices every modern LLM already follows are left out. Each line earns its tokens by changing default behavior.
- **Stable abstractions** — avoids version pins and project-specific details that go stale, so you rarely need to edit these files.
- **Profiles loaded on demand** — universal rules stay small; stack-specific rules layer in only when relevant.
