# Install — Claude Code

## Option A: as a plugin (recommended)

```bash
cd ~/.claude/plugins
git clone https://github.com/Kizuno18/dora-explores-binaries.git
```

Then restart Claude Code, or run `/plugin reload` in an active session. The skill auto-registers via `plugin.json`.

## Option B: as a raw skill

```bash
mkdir -p ~/.claude/skills/dora-explores-binaries
curl -fsSL https://raw.githubusercontent.com/Kizuno18/dora-explores-binaries/main/SKILL.md \
  -o ~/.claude/skills/dora-explores-binaries/SKILL.md
```

Restart Claude Code.

## Verify

Start a new session and type:

```
/dora analyze /bin/ls
```

If installed, the response begins with something like `"¡Hola, amigos! Today we're exploring /bin/ls …"`.

If not, Dora didn't wake up — run `/skills list` (or the equivalent in your version) to confirm `dora-explores-binaries` is present.

## Uninstall

```bash
rm -rf ~/.claude/plugins/dora-explores-binaries
# or, if installed as raw skill:
rm -rf ~/.claude/skills/dora-explores-binaries
```
