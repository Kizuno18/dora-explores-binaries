# Install — Generic LLM / API

Any tool that lets you set a system prompt or "custom instructions" can host this skill.

## System-prompt prepend

Fetch the skill:

```bash
curl -fsSL https://raw.githubusercontent.com/Kizuno18/dora-explores-binaries/main/SKILL.md
```

Take everything from the `## When this skill activates` header down to (and including) the `## What this skill is NOT` section. Prepend it to your system prompt.

The YAML frontmatter (`name:`, `description:`, `version:`, etc.) at the very top is metadata for skill loaders; a plain LLM does not need it.

## OpenAI API / Anthropic API / any completion endpoint

Concatenate the skill text into the `system` message (Anthropic) or the first `system` role message (OpenAI-compatible). Example (Anthropic Messages API):

```python
import anthropic, pathlib
skill = pathlib.Path("SKILL.md").read_text()
# strip yaml frontmatter (first --- block)
_, _, body = skill.split("---", 2)

client = anthropic.Anthropic()
msg = client.messages.create(
    model="claude-fable-5-1",
    max_tokens=4096,
    system=body.strip(),
    messages=[{"role": "user", "content": "reverse-engineer /bin/ls"}],
)
print(msg.content[0].text)
```

## ChatGPT Custom GPTs / Claude Projects

Paste the skill body into the "Instructions" / "Custom instructions" field of the GPT or Project. Upload a copy of `SKILL.md` as a project file if the tool supports it, so the model can re-read it on demand.

## Ollama / local LLM harnesses

Add the skill text to the model's system prompt via `Modelfile`:

```
FROM llama3.3:70b
SYSTEM """<paste SKILL.md body here>"""
```

Then `ollama create dora-re -f Modelfile`.

## Verify

Send a prompt like:

```
reverse-engineer /bin/ls dora-style
```

The reply should open with the cold-open pattern: `"¡Hola, amigos! Today we're exploring /bin/ls — …"`.

## Notes

- The skill is prompt-only. It never runs tools by itself; the harness (or you) still runs `strings`, `objdump`, etc. and feeds the output back.
- Smaller models (< 8B) will handle the persona but may drop the discipline (fake cheers, English-only). Bigger models keep the balance better.
- If the model translates every sentence Spanish + English, you have too much persona weight — trim the skill body a bit or lower the effort setting.
