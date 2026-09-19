# v0.2 TODO — Canonical Episodes (playbook path)

`v0.1` ships persona only. `v0.2` adds **canonical episode templates**: prescriptive mini-recipes that structure a full RE task (`recon` → `unpacking` → `crypto ID` → …), each narrated in Dora voice. Zero external dependencies — every episode uses tools already in a standard RE box.

## Design principles for v0.2

- Each episode = one Markdown file under `docs/episodes/`.
- Each episode has: a **Route** (3-5 stops), a **Backpack list** (tools per stop), a **Swiper watch** (protections to expect), a **Cheer condition** (what evidence proves success), a **Handoff** (next episode).
- Episodes never assume more than what a standard RE workstation has installed: `file`, `strings`, `objdump`, `readelf`, `nm`, `binwalk`, `hexdump`/`xxd`, `radare2`, `python3` + `capstone`/`pefile`, `yara`. Tools beyond that (`ghidra`, `ida`, `frida`) are **optional upgrades** listed under a "Backpack upgrade" callout.
- Episodes are prescriptive, not conversational: they read like a recipe, but example dialogue is included at the top so the LLM knows the voice.

## Planned episodes

### 1. `backpack-check.md` — Recon
- **Route**: `file → strings → hexdump header → sections/imports → signatures`.
- **Backpack**: `file`, `strings`, `hexdump`/`xxd`, `objdump -h` (or `readelf -S`), `die`.
- **Swiper watch**: entropy of `.text`/`.rdata` sections; suspicious section names (`.vmp0`, `.themida`, `.upx*`, `.enigma*`); embedded PE-in-PE / ELF-in-ELF via `binwalk`.
- **Cheer condition**: a definitive classification — "this is X compiled with Y, packed by Z (or not)".

### 2. `map-reading.md` — Control flow / call graph
- **Route**: `entry → main → hot-function ID → callgraph export → topology summary`.
- **Backpack**: `radare2` (`r2 -A`, `aaa`, `agC`), `objdump -d`, `python3 + capstone`.
- **Backpack upgrade**: `ghidra` headless, `ida` idalib.
- **Swiper watch**: obfuscated control flow (opaque predicates, flattening); indirect jumps through jump tables; API resolution via GetProcAddress hash.
- **Cheer condition**: named hot-path functions with intents (parser / network / crypto / etc.).

### 3. `swiper-watch.md` — Anti-analysis
- **Route**: `enumerate anti-debug calls → PEB flag reads → timing checks → anti-VM heuristics → patch strategy → prove bypass`.
- **Backpack**: `objdump | grep` for classic API names, `radare2 /re` for byte-pattern searches, one live-attach debugger of choice.
- **Swiper watch**: `IsDebuggerPresent`, `CheckRemoteDebuggerPresent`, `NtQueryInformationProcess`, `NtSetInformationThread(ThreadHideFromDebugger)`, `NtQuerySystemInformation(SystemKernelDebuggerInformation)`, PEB `BeingDebugged` / `NtGlobalFlag`, RDTSC deltas, CPUID leaf `0x40000000`, MAC OUI checks.
- **Cheer condition**: patched sample runs to `main` with a debugger attached; recorded bytes changed.

### 4. `unpacker-lane.md` — Automated unpacking
- **Route**: `packer ID → tail-jump/OEP heuristic → dump memory → rebuild imports → verify`.
- **Backpack**: `die`, `unipacker` (for known packers), a debugger with dumping (`x64dbg` + Scylla), `pe-sieve`.
- **Backpack upgrade**: `frida` for run-time module dumping; `qiling` for headless emulation.
- **Swiper watch**: TLS-callback OEP misdirection, self-integrity checks post-dump, encrypted IAT.
- **Cheer condition**: `sample_unpacked.exe` boots in a sandbox and passes a signature/YARA scan against known clean templates.

### 5. `crypto-id.md` — Crypto identification
- **Route**: `constant scan (S-boxes / round constants) → API imports → block-size fingerprint → mode ID`.
- **Backpack**: `yara` (with the community crypto ruleset), `strings`, targeted `objdump` grep for `CryptAcquireContext`, `BCryptEncrypt`, `AES_encrypt`, `EVP_EncryptInit`, `chacha20`, `sodium_*`.
- **Swiper watch**: custom XOR keyed by CPUID/HWID; homebrew rot-N; obfuscated tables under XOR sheet.
- **Cheer condition**: named algorithm + mode + key location OR a documented "custom, key at 0x...".

### 6. `we-did-it.md` — Writeup template
- **Not an episode**; it's a **closing template** — a Markdown skeleton the agent fills at the end of a full RE task, containing:
  - artifact identity + hashes,
  - route taken,
  - each Cheer with its evidence line,
  - any unresolved Swiper (open questions / needs help),
  - suggested next episode (if handing off).
- The template is written in **normal English** — no Dora voice. The Dora persona is chat-scoped; the final deliverable is a real writeup.

## Implementation strategy for v0.2

1. Write episode files as prose that reads well to both humans and models. Use the exact structure sketched above.
2. Cross-link between episodes so a v0.2 agent can naturally hand off: `swiper-watch.md` → `unpacker-lane.md` → `crypto-id.md` etc.
3. Update the top-level `SKILL.md` to add a **"Canonical episodes"** section that references `docs/episodes/*.md` by name.
4. Add example transcripts for each episode under `docs/examples/`, following the format used in `example-01` / `example-02`.
5. Update the README's roadmap block; bump the version in `plugin.json` to `0.2.0`.

## Non-goals for v0.2

- No CLI (that's v0.3).
- No MCP server bundled (users bring their own tool MCPs; the skill just narrates).
- No stateful "episode tracker" — episodes are self-contained; the model chooses which to enter based on the artifact and the user's mission.
- No "auto-detect" logic that classifies the binary before the skill loads. Detection happens inside the first stop of `backpack-check`.

## Contributing to v0.2

- Open an issue with the `New Episode` template describing the RE task and the proposed Route.
- Or PR a new file under `docs/episodes/` following the shape sketched above.

## Timeline

Not fixed. `v0.2` ships when there are at least three complete, tested episodes with real transcripts and no `TBD`s. Community PRs count.
