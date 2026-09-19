<div align="center">

# 🎒🗺️ dora explores binaries

**A reverse-engineering skill that turns your AI coding agent into Dora the Explorer.**

<sub>Backpack has your tools. Map plans the flow. Swiper is the packer. And every real breakthrough gets a `¡Lo hicimos!`</sub>

[![License: MIT](https://img.shields.io/badge/License-MIT-brightgreen.svg)](LICENSE)
[![Skills: Anthropic Spec](https://img.shields.io/badge/skills-Anthropic%20spec-blue)](SKILL.md)
[![Harness: Any](https://img.shields.io/badge/harness-Claude%20Code%20%7C%20Codex%20%7C%20Cursor%20%7C%20API-purple)](docs/install/)
[![Persona: Dora](https://img.shields.io/badge/persona-Dora-ff69b4)](SKILL.md)
[![Stars welcome](https://img.shields.io/badge/⭐-stars%20welcome-yellow)](#)

</div>

---

## What is this

It's a single [`SKILL.md`](SKILL.md) that hijacks your AI agent's voice during reverse-engineering tasks.

Ask it to unpack an `.exe`, dissect a firmware image, or decompile a `.dll`, and instead of dry monotone tool output you get:

> *"¡Hola, amigos! Today we're exploring `sample.exe` — a Windows PE that's hiding something. First we go through the imports! Then across the packed section! Then to the OEP! **Imports → packed section → OEP! Say it with me!**"*
>
> *"Backpack, we need `radare2`! (`r2 -A ./sample.exe`)"*
>
> *"¡Mira! `.vmp0` section. **¡Swiper, no swiping!** VMProtect 3.x is on the map. New route: **anti-VM check first, then dump handlers.**"*
>
> *"`IsDebuggerPresent` inline at `0x140012a4` → patch `xor eax, eax; ret`. Try again."*
>
> *"**¡Lo hicimos! WE DID IT!** OEP at `0x141002000` recovered, imports rebuilt with `Scylla`. `sample_unpacked.exe` boots clean in a sandbox."*

The persona is scoped to RE turns. It never leaks into your code, commits, PRs, or docs — those still sound like *you*.

## Why

- **Legibility.** RE work is a fog of tool output, addresses, and dead ends. A cast narrating each step (Backpack = which tool, Map = which plan, Swiper = which protection) makes the pipeline readable to anyone watching.
- **Onboarding.** Beginners can follow a Dora RE session and *see* what an expert would do next, because Dora explains it out loud.
- **Fun.** Reverse engineering is often lonely. A persona that celebrates *actual* breakthroughs with *actual* evidence makes long sessions less painful.
- **Portable.** One `SKILL.md` — no runtime, no CLI, no dependencies. Works in every AI coding harness you already have.

## Install

Pick your harness:

| Harness | Install path |
|---|---|
| [Claude Code](docs/install/claude-code.md) | plugin |
| [Codex Desktop](docs/install/codex.md) | `~/.codex/skills/` drop-in |
| [Cursor / Windsurf](docs/install/cursor.md) | rules file append |
| [Generic API / other LLM](docs/install/generic-llm.md) | system-prompt prepend |

Universal fallback for any tool that reads Markdown skills: copy [`SKILL.md`](SKILL.md) into that tool's skill directory.

## Quick invoke

Once installed, any RE-flavored prompt activates it automatically. To force it explicitly:

```
/dora analyze ./sample.exe
```
or
```
dora mode: unpack this VMProtect'd binary and find the OEP
```

To exit the persona mid-session (without losing progress):

```
/dora off
```

## The Cast

| Character | Role |
|---|---|
| **The Backpack** | your toolbelt (`strings`, `objdump`, `r2`, `ghidra`, `frida`, `binwalk`, `die`, `yara`, …) |
| **The Map** | the analysis plan / call graph / route |
| **Swiper the Fox** | anti-debug, anti-VM, packers, protectors, obfuscation — named subtypes: *inline API check*, *PEB flag read*, *timing check*, *SMBIOS anti-VM*, *TLS callback*, *integrity check*, ***Swiper's Locked Door*** (env-gated behavior), ***SCM race*** (Wine/Windows service manager cache), *packer*, *obfuscator* |
| **Boots** | the sidekick subagent doing legwork in parallel |
| **The Cave** | the isolated run environment: container netns, VM guest, wine prefix, `nsenter` namespace — the sandbox where the sample actually executes |
| **The Viewer** | you, the human — Dora addresses you directly when a decision is needed |

Full glossary: [`docs/glossary.md`](docs/glossary.md)

## Show me a real transcript

- [example 01 — string recon on an unknown ELF](docs/examples/example-01-strings-recon.md)
- [example 02 — Swiper vs `IsDebuggerPresent` (one-byte patch)](docs/examples/example-02-anti-debug-swiper.md)
- [example 03 — Wine kernel driver, SCM race, IOCTL smoke](docs/examples/example-03-wine-kernel-driver.md) — the *Cave*, the *Locked Door*, and the *SCM race* archetypes in one episode

## Design principles

1. **Real evidence, always.** No `¡Lo hicimos!` without an exact byte/status/string right after it. The persona amplifies competence; it does not fake finds.
2. **Chat only.** The Dora voice never enters files, commits, PRs, or issues. Persistent artifacts are written in normal English.
3. **Bilingual sprinkle.** Spanish and Portuguese phrases dot the flow (*¡Vámonos!*, *¡Mira!*, *¿Puedes ayudarnos?*). Never a literal double-translation.
4. **Exact numbers survive verbatim.** `status=0xc0000034` stays `status=0xc0000034`.
5. **Episodes end.** Each session is bounded; long tasks are chunked into episodes with an on-air "next time on…" handoff.

## Roadmap

- **v0.1** (this release): persona-only skill, cross-harness, install docs, example transcripts.
- **v0.2** (TODO — see [`docs/TODO-episodes-v2.md`](docs/TODO-episodes-v2.md)): canonical RE playbooks structured as episodes (*Backpack Check* / *Map Reading* / *Swiper Watch* / *We Did It!*). Each is a prescriptive mini-recipe (command → observation → next step) narrated in Dora voice. Zero external dependencies.
- **v0.3** (stretch): optional `dora` CLI wrapping common RE tools with Dora-styled output.

## Contributing

New glossary term? New example transcript? New episode template for v0.2?

- Open an issue with the [`New Episode`](.github/ISSUE_TEMPLATE/new-episode.md) or [`Glossary Term`](.github/ISSUE_TEMPLATE/glossary-term.md) template.
- Or send a PR. See [`CONTRIBUTING.md`](CONTRIBUTING.md).

## Ethical & legal notes

This project is a **parody / homage** of a widely-known children's television character. It uses no assets, art, music, characters as portrayed, trademarks, or logos from the show — only structural metaphors (a backpack for tools, a map for a plan, a fox for a protector). The name plays on the character's "explorer" archetype in the same way "Waldo" or "Sherlock" enter common speech.

Reverse engineering is a legitimate discipline used in security research, interoperability, malware analysis, digital preservation, and education. Only use this skill on binaries you are legally authorized to analyze. This project does not endorse or assist unauthorized access, copyright infringement, DRM circumvention where prohibited, or license-violating redistribution.

## License

MIT — see [`LICENSE`](LICENSE).

---

<div align="center">
<sub>¡Vámonos! · Made with 🎒 and a lot of <code>strings(1)</code></sub>
</div>
