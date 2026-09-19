<div align="center">

# 🎒🗺️ dora explores binaries

### *"¡Lo hicimos! WE DID IT!"* — your AI agent, after every real breakthrough.

**A reverse-engineering skill that turns any AI coding agent into Dora the Explorer.**
Backpack holds your tools. Map plans the flow. Swiper is the packer. Every finding gets celebrated with the *exact bytes* on the very same line.

[![License: MIT](https://img.shields.io/github/license/Kizuno18/dora-explores-binaries?style=flat-square)](LICENSE)
[![Release](https://img.shields.io/github/v/release/Kizuno18/dora-explores-binaries?style=flat-square&color=purple)](https://github.com/Kizuno18/dora-explores-binaries/releases)
[![Stars](https://img.shields.io/github/stars/Kizuno18/dora-explores-binaries?style=flat-square)](https://github.com/Kizuno18/dora-explores-binaries/stargazers)
[![Skills: Anthropic Spec](https://img.shields.io/badge/skills-Anthropic%20spec-blue?style=flat-square)](SKILL.md)
[![Harness: Any](https://img.shields.io/badge/harness-Claude%20Code%20%7C%20Codex%20%7C%20Cursor%20%7C%20API-purple?style=flat-square)](docs/install/)
[![Languages: EN · ES · pt-BR](https://img.shields.io/badge/languages-EN%20·%20ES%20·%20pt--BR-orange?style=flat-square)](SKILL.md#language-policy--default-english-sprinkle-es-and-pt-br)
[![If you smile, ⭐ the repo](https://img.shields.io/badge/if%20you%20smile-⭐%20the%20repo-yellow?style=flat-square)](https://github.com/Kizuno18/dora-explores-binaries/stargazers)

</div>

---

## 60 seconds — what does it feel like

You ask your agent: *"reverse-engineer this suspicious `.exe` and figure out how it detects debuggers"*.

Without the skill:

> `Sure. I'll start by running strings and objdump.` *(runs 12 tool calls in silence, then dumps a wall of hex.)*

With **dora explores binaries**:

> *"¡Hola, amigos! Today we're going after `sample.exe` — every time we attach a debugger it disappears. **¡Swiper is here!** We need to find him. First we fingerprint! Then we find the check! Then we patch it! Then we prove it! **Fingerprint → Find → Patch → Prove! Say it with me!**"*
>
> *"Backpack, we need `die`!"* *(runs die → reports `PE64 MSVC 2022, no packer`)*
>
> *"¡Mira! No packer — plain MSVC. Swiper is going to be **inline API**. Map! Route confirmed. Backpack, we need `objdump`!"*
>
> *"**¡Swiper, no swiping!** `IsDebuggerPresent` at `0x140012a0`, `test eax,eax` at `0x140012a6`, `je +5` at `0x140012a8`, then jump to `exit_process` at `0x140012aa`. Flip the branch: `74 05` → `eb 05` — one byte, less invasive."*
>
> *"**¡Lo hicimos! WE DID IT! 100% WORKING!** One byte flipped, `RAX=0x00000001` from the API, and the jump still skips the exit — the process now **survives with a debugger attached**. Swiper missed the map."*

Same tool calls. Same bytes. **The pipeline is legible.** A person watching over your shoulder — or reading the transcript six months later — can follow every step.

*[See the full transcript ▸](docs/examples/example-02-anti-debug-swiper.md)*

---

## Table of contents

- [Why](#why)
- [How it works](#how-it-works)
- [Install](#install) · [Claude Code](docs/install/claude-code.md) · [Codex](docs/install/codex.md) · [Cursor / Windsurf](docs/install/cursor.md) · [Generic LLM](docs/install/generic-llm.md)
- [Quick invoke](#quick-invoke)
- [The Cast](#the-cast)
- [Trilingual by design](#trilingual-by-design)
- [Real transcripts](#real-transcripts)
- [Design principles](#design-principles)
- [Roadmap](#roadmap)
- [FAQ](#faq)
- [Contributing](#contributing)
- [Legal](#legal)

---

## Why

Reverse engineering is a fog of tool output, addresses, dead ends, and quiet victories. Even senior engineers lose context after an hour of hopping between `objdump`, `radare2`, `frida`, and a debugger. A junior watching the session usually has no idea what just happened.

**dora explores binaries** fixes the legibility problem with a persona:

- Every step is narrated in the moment: *"Backpack, we need `strings`!"* — the tool call is *announced*, not hidden.
- Every plan pivot is called out: *"Map! New route: **Swiper Watch → patch → retry.**"*
- Every real breakthrough gets a celebration with **the exact evidence right next to it**: `¡Lo hicimos! WE DID IT!` → `NtCreateFile status=0x00000000 out[1]=0x76 (expected 0x76)`.
- Every anti-analysis trick is named by archetype: *inline API check*, *PEB flag read*, *timing check*, *SMBIOS anti-VM*, *TLS callback*, *integrity check*, ***Swiper's Locked Door***, ***SCM race***, *packer*, *obfuscator*.

The result: sessions you can hand to a beginner, transcripts that read like a walkthrough, and a running record of exactly which bytes proved what.

## How it works

The whole product is a single [`SKILL.md`](SKILL.md) in the [Anthropic Skills](https://www.anthropic.com/news/introducing-skills) format. No CLI. No dependencies. No runtime. **The persona only exists during chat.** Files, commits, PRs, issues, and code comments you generate stay in normal, professional English.

The skill teaches the model:

1. **When to activate** — RE tasks only. Not when you're debugging your own app; not for PR descriptions.
2. **The cast** — Backpack, Map, Swiper (with 10 named subtypes), Boots, the Cave, the Viewer, and a handful of recurring guests.
3. **The episode structure** — cold open, Map route, ordered Stops, Cheer with evidence, Closing.
4. **A trilingual voice policy** — English is the spine; Spanish is the primary sprinkle (canonical Dora); Portuguese (BR) activates automatically when you write in pt-BR.
5. **Hard rules** — no fake cheers, no double-translations, no persona bleed into persistent artifacts, hard escape hatch (`/dora off`).

## Install

Pick your harness. One file, one path.

<details>
<summary><b>Claude Code</b> — plugin</summary>

```bash
cd ~/.claude/plugins
git clone https://github.com/Kizuno18/dora-explores-binaries.git
```

Then restart Claude Code or `/plugin reload`. Full guide: [`docs/install/claude-code.md`](docs/install/claude-code.md).
</details>

<details>
<summary><b>Codex Desktop / CLI</b> — drop-in</summary>

```bash
mkdir -p ~/.codex/skills/dora-explores-binaries
curl -fsSL https://raw.githubusercontent.com/Kizuno18/dora-explores-binaries/main/SKILL.md \
  -o ~/.codex/skills/dora-explores-binaries/SKILL.md
```

Restart the daemon. Full guide: [`docs/install/codex.md`](docs/install/codex.md).
</details>

<details>
<summary><b>Cursor / Windsurf</b> — rules file</summary>

```bash
mkdir -p .cursor/rules
curl -fsSL https://raw.githubusercontent.com/Kizuno18/dora-explores-binaries/main/SKILL.md \
  -o .cursor/rules/dora-explores-binaries.mdc
```

Or paste `SKILL.md` into Cursor Settings → Rules for AI. Full guide: [`docs/install/cursor.md`](docs/install/cursor.md).
</details>

<details>
<summary><b>Generic LLM / API</b> — system-prompt prepend</summary>

Fetch `SKILL.md`, strip the YAML frontmatter, prepend to your system prompt. Works with OpenAI, Anthropic, Ollama, ChatGPT Custom GPTs, Claude Projects, and anything with an instructions field. Full guide: [`docs/install/generic-llm.md`](docs/install/generic-llm.md).
</details>

## Quick invoke

Once installed, any RE-flavored prompt activates it automatically:

```
reverse this: /bin/ls
```

Force it explicitly:

```
/dora analyze ./sample.exe
```

```
dora mode: unpack this VMProtect'd binary and find the OEP
```

Exit the persona mid-session (progress preserved):

```
/dora off
```

## The Cast

| Character | Role |
|---|---|
| **The Backpack** | your toolbelt — `strings`, `objdump`, `r2`, `ghidra`, `ida`, `frida`, `binwalk`, `die`, `yara`, `x64dbg`, `windbg`, and every other tool your harness exposes |
| **The Map** | the analysis plan — call graph, control flow, next step |
| **Swiper the Fox** | anti-analysis, in 10 named flavors — *inline API check*, *PEB flag read*, *timing check*, *SMBIOS anti-VM*, *TLS callback*, *integrity check*, ***Swiper's Locked Door*** (env-gated behavior), ***SCM race*** (Wine/Windows service manager quirk), *packer*, *obfuscator* |
| **Boots** | the sidekick subagent doing legwork in parallel |
| **The Cave** | the isolated run environment — container netns, VM guest, wine prefix, `nsenter` namespace; the sandbox where the sample actually executes |
| **The Viewer** | you, the human — Dora addresses you directly when a decision is needed |

Recurring guests (used sparingly, one per episode max): **the Big Red Chicken**, the **Grumpy Old Troll** (checksums / integrity gates), **Isa the Iguana** (reference databases), **Tico the Squirrel** (speed heuristics), **Benny the Bull** (brute force).

Full glossary and voice patterns in [`docs/glossary.md`](docs/glossary.md).

## Trilingual by design

<table><tr><td>

**Base language: English.**
Every sentence is grammatical English on its own. Every technical identifier (`IsDebuggerPresent`, `STATUS_OBJECT_NAME_NOT_FOUND`, `RAX=0x00000001`, section names, offsets) stays verbatim in English.

**Primary sprinkle: Spanish** — the canonical Dora phrases. `¡Vámonos!`, `¡Mira!`, `¡Lo hicimos!`, `¡Perfecto!`, `¡Excelente!`, `¡Cuidado!`, `¡Swiper, no swiping!`, `¿Puedes ayudarnos?`.

**Secondary sprinkle: Portuguese (BR)** — activates automatically when you write in pt-BR. `Conseguimos!`, `Achamos!`, `Bateu certinho!`, `Tá rodando 100%!`, `Beleza!`, `Perfeito!`, `Swiper, não roube!`, `Pode ajudar?`.

</td><td>

**Cheers, three flavors:**

| Situation | EN | ES | pt-BR |
|---|---|---|---|
| primary goal verified | `WE DID IT!` | `¡Lo hicimos!` | `Conseguimos!` |
| target located | `THERE IT IS!` | `¡Ahí está!` | `Achamos!` |
| byte-exact match | `EXACT MATCH!` | `¡Exacto!` | `Bateu certinho!` |
| patched sample works | `100% WORKING!` | `¡Funciona al 100%!` | `Tá rodando 100%!` |
| handoff | `Great exploring today!` | `¡Hasta la próxima!` | `Até a próxima!` |

Full table in [`SKILL.md#cheer-phrase-table`](SKILL.md#cheer-phrase-table).

</td></tr></table>

**Hard mixing rules**: no dubbing (same sentence twice, two languages), no tri-lingual single sentences, never translate technical identifiers, never cheer without exact evidence on the next line.

## Real transcripts

Real sessions. Real bytes. No fake output.

- **[example 01](docs/examples/example-01-strings-recon.md)** — string recon on an unknown stripped ELF. Skill picks between `file`, `strings`, `readelf`, and `objdump` to classify the binary in five minutes.
- **[example 02](docs/examples/example-02-anti-debug-swiper.md)** — Swiper vs `IsDebuggerPresent`. One-byte patch (`74 05 → eb 05`) at `0x140012a8`, proven with `RAX=0x00000001` under an attached debugger.
- **[example 03](docs/examples/example-03-wine-kernel-driver.md)** — installing a Wine kernel driver as a live SCM service, escaping the `STATUS_OBJECT_NAME_NOT_FOUND` locked door with `sc create` instead of `wine reg add`, and proving the IOCTL round-trip with `EXACT MATCH!` + `100% WORKING!`. **Demonstrates the Cave, Locked Door, and SCM race archetypes in a single episode.**

## Design principles

1. **Real evidence, always.** No cheer without an exact byte / status / address / string on the same or next line. The persona amplifies competence; it never fakes finds.
2. **Chat only.** The Dora voice never enters files, commits, PRs, issues, or code comments. Persistent artifacts stay in normal English.
3. **English-default, sprinkled with ES and pt-BR.** English is the spine of every sentence. Spanish is the primary sprinkle; Portuguese (BR) is the secondary sprinkle, activated when you write in pt-BR. Never a literal double-translation.
4. **Exact numbers survive verbatim.** `status=0xc0000034` stays `status=0xc0000034` in every language.
5. **Episodes end.** Each session is bounded; long tasks are chunked into episodes with an on-air *"next time on…"* handoff.
6. **Escape hatch always available.** `/dora off` drops the persona for the rest of the session without losing progress.

## Roadmap

- **v0.1** *(shipped)* — persona-only skill, cross-harness, 3 real transcripts, trilingual policy.
- **v0.2** *(planned — [TODO](docs/TODO-episodes-v2.md))* — canonical RE playbooks as structured episodes (*Backpack Check*, *Map Reading*, *Swiper Watch*, *Unpacker Lane*, *Crypto ID*, *We Did It!* writeup template). Prescriptive command → observation → next step; zero external dependencies.
- **v0.3** *(stretch)* — optional `dora` CLI wrapping common RE tools with Dora-styled output.
- **v0.4** *(if community traction)* — mobile RE additions (Android SafetyNet, iOS Frida detection, `apktool`/`jadx`/`class-dump`) and macOS RE additions (SIP, AMFI, code signing).

## FAQ

**Q: Will this ever end up in a commit message, PR body, or code comment?**
No. The skill is **chat-scoped by design**. Persistent artifacts are always written in normal, professional English. This is enforced by the "What this skill is NOT" section of [`SKILL.md`](SKILL.md).

**Q: Does it slow down real RE work?**
No — same tool calls, same commands, same outputs. What changes is how each step is narrated. Timing is a wash; legibility jumps.

**Q: Will smaller models handle it?**
Yes, imperfectly. Models under ~8B parameters keep the persona but sometimes drop the discipline (double-translation, wall of caps, fake cheers). See [`docs/install/generic-llm.md`](docs/install/generic-llm.md) for tuning notes.

**Q: What about macOS / mobile RE?**
v0.1 covers Windows / Linux / Wine well. macOS SIP + AMFI + code signing, and mobile SafetyNet + Frida detection + `apktool`/`jadx`/`class-dump` land in v0.4. Contributions welcome — see [`CONTRIBUTING.md`](CONTRIBUTING.md).

**Q: Does the skill actually reverse-engineer anything on its own?**
No. It's a persona layer. The tools that do the work (`objdump`, `radare2`, `frida`, `ghidra`, MCP servers) still do the work. The skill teaches the model to narrate that work in a legible, replayable, Dora-styled voice.

**Q: Can I turn it off mid-session?**
Yes. `/dora off` (or say "stop dora" / "sério agora" / "normal mode") drops the persona for the rest of the session.

**Q: How is this different from a "system prompt hack" that just says 'be Dora'?**
It's the difference between *cheerleader* and *narrator*. The skill is 500+ lines of hard rules: named archetypes, exact cheer phrases per language, evidence discipline, when to activate, when NOT to activate, escape hatches, failure modes. Read [`SKILL.md`](SKILL.md).

**Q: Is this legal?**
Yes — see [Legal](#legal) below. No assets, art, music, characters as portrayed, trademarks, or logos from the show are used or distributed. Structural metaphors only.

## Contributing

New glossary term? New example transcript? A canonical episode template for v0.2? A new install target?

- Open an issue with the [`New Episode`](.github/ISSUE_TEMPLATE/new-episode.md) or [`Glossary Term`](.github/ISSUE_TEMPLATE/glossary-term.md) template.
- Or send a PR. See [`CONTRIBUTING.md`](CONTRIBUTING.md).

Contributions must include **real evidence** for any example (real byte offsets, real command output, real cheer moments) and follow the persona rules (no fake cheers, no dubbing, no persona bleed into commits).

## Legal

This project is a **parody / homage** of a widely-known children's television character. It uses **no assets**, art, music, characters as portrayed, trademarks, or logos from the show — only structural metaphors: a backpack for tools, a map for a plan, a fox for a protector. The name plays on the character's *explorer* archetype the same way *Waldo* or *Sherlock* enter common speech.

This project is **not affiliated with, endorsed by, sponsored by, or associated with** Nickelodeon, Viacom, ViacomCBS, Paramount, or the show's creators, producers, distributors, or rights-holders. All trademarks belong to their respective owners.

Reverse engineering is a legitimate discipline used in security research, interoperability, malware analysis, digital preservation, and education. Only use this skill on binaries you are legally authorized to analyze. This project does not endorse or assist unauthorized access, copyright infringement, DRM circumvention where prohibited, or license-violating redistribution.

## License

MIT — see [`LICENSE`](LICENSE).

---

<div align="center">

**If Dora just made an ugly hex dump click for you — ⭐ the repo. It's the shortest, most useful signal you can send.**

<sub>¡Vámonos! · Made with 🎒 and a lot of <code>strings(1)</code></sub>

</div>
