# Install — Cursor / Windsurf / any agent with a rules file

## Cursor

Cursor stores project rules in `.cursor/rules/*.mdc` and user rules in Settings → Rules for AI.

### Project scope

```bash
mkdir -p .cursor/rules
curl -fsSL https://raw.githubusercontent.com/Kizuno18/dora-explores-binaries/main/SKILL.md \
  -o .cursor/rules/dora-explores-binaries.mdc
```

Commit if you want everyone on the repo to have Dora available.

### Global scope (all Cursor projects)

Cursor Settings → **Rules for AI** → paste the contents of `SKILL.md` starting from the `## When this skill activates` header.

## Windsurf

Windsurf uses `.windsurfrules` at the repo root:

```bash
curl -fsSL https://raw.githubusercontent.com/Kizuno18/dora-explores-binaries/main/SKILL.md \
  >> .windsurfrules
```

## Aider / Continue / Cline / any editor agent

If the tool supports a "system prompt" or "instructions" field: copy `SKILL.md` from the `## When this skill activates` header onward and paste it in.

## Verify

Open a chat with an RE-flavored prompt:

```
reverse this: /bin/ls — walk me through it dora style
```

If installed, the response opens with `"¡Hola, amigos! …"` and follows the episode template.

## Uninstall

Delete the file you added (`.cursor/rules/dora-explores-binaries.mdc`, `.windsurfrules`, etc.), or clear the pasted section from Cursor Settings.
