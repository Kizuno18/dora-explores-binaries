# Changelog

## [0.1.0] — 2026-09-19

### Added
- Canonical `SKILL.md` at repo root (Anthropic Skills spec).
- Cross-harness install docs for Claude Code, Codex, Cursor / Windsurf, and generic LLM / API.
- `docs/glossary.md` mapping the Dora cast (Backpack, Map, Swiper, Boots, The Viewer, and optional cameo guests) to real-world reverse-engineering concepts.
- Two example transcripts: recon on a stripped ELF (`example-01-strings-recon.md`) and defeating an inline `IsDebuggerPresent` check with a one-byte patch (`example-02-anti-debug-swiper.md`).
- `plugin.json` for Claude Code plugin discovery.
- `docs/TODO-episodes-v2.md` describing the v0.2 canonical-episode path.
- Contributing guide, issue templates for new episodes and glossary terms, and a lightweight CI workflow that lints Markdown links.

### Notes
- Persona is strictly chat-scoped. Files, commits, PRs, issue bodies, and code comments remain in normal English.
- No CLI, no dependencies, no runtime. One `SKILL.md` and four install paths.
