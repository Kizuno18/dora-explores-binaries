# Changelog

## [0.1.1] — 2026-09-19

### Added
- **Cave** cast member — the isolated execution environment (docker netns, VM guest, wine prefix, `nsenter` namespace) that modern RE increasingly happens inside. Added to `SKILL.md` cast table and `docs/glossary.md`.
- **Swiper subtype table** in `SKILL.md`: named archetypes for inline API check, PEB flag read, timing check, SMBIOS anti-VM, TLS callback, integrity check, ***Swiper's Locked Door*** (env-gated protection), ***SCM race*** (Wine/Windows service manager cache), packer, obfuscator.
- **Cheer phrase table**: rotate between `¡Lo hicimos! WE DID IT!`, `LOOK AT THAT!`, `THERE IT IS!`, `EXACT MATCH!`, `100% WORKING!`, `GOT IT!`, `¡Excelente!`, `¡Perfecto!`, `¡Mira!` — never chain two full cheers, never cheer without evidence.
- **Wine / Linux RE section** in glossary: winedevice, SCM, Xvfb / `DISPLAY :99`, virtual desktop `BadWindow` gotchas.
- Rule that STATUS_OBJECT_NAME_NOT_FOUND / STATUS_BLOCK / STATUS_INVALID_PARAMETER and similar NT statuses should be quoted verbatim then reasoned about as *which door is locked*.
- Rule that remote-lab chains (ssh → docker exec → nsenter → wine → target) are named as a Cave with N doors, not as individual stops.
- `docs/examples/example-03-wine-kernel-driver.md` — anonymized transcript demonstrating the Cave, Locked Door, SCM race, and the `LOOK AT THAT!` / `EXACT MATCH!` / `100% WORKING!` cheer variants in one episode.

### Changed
- Duplicate cheer/closing sections in `docs/glossary.md` folded into the new cheer phrase table.
- README cast table now names the new archetypes and the Cave.

### Rationale
- Mined a real 6-hour reverse-engineering session (Wine kernel driver install, SCM race, IOCTL smoke test) to find gaps in v0.1's persona vocabulary. Every addition in this release maps to a concrete pattern that showed up in that session.

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
