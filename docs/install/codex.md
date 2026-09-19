# Install — Codex Desktop / CLI

## Drop-in install

```bash
mkdir -p ~/.codex/skills/dora-explores-binaries
curl -fsSL https://raw.githubusercontent.com/Kizuno18/dora-explores-binaries/main/SKILL.md \
  -o ~/.codex/skills/dora-explores-binaries/SKILL.md
```

Codex reads `~/.codex/skills/*/SKILL.md` on startup. Restart the daemon so it picks up the new skill:

```bash
pkill -f 'codex.*app-server --listen'   # Desktop respawns it
```

## Verify

Start a new Codex thread and type:

```
/dora analyze /bin/ls
```

The response should open in Dora voice. If not, check:

```bash
grep -RIl 'dora-explores-binaries' ~/.codex/skills/
```

## Notes

- Codex Desktop's `personality: "friendly"` + `effort: "xhigh"` + `summary: "detailed"` on the turn context is a nice pairing — it amplifies the narrator vibe without changing correctness.
- The persona does NOT bypass `sandbox_mode` / `approval_policy`. RE work still runs under whatever sandbox you have configured.
- If you clone the whole repo instead of just `SKILL.md`, you get the glossary and example transcripts too, which the agent will happily reference.

## Uninstall

```bash
rm -rf ~/.codex/skills/dora-explores-binaries
```
