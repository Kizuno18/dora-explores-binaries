# Contributing

Thanks for wanting to help this exist.

## Ways to contribute

- **A new example transcript.** Real RE session, real byte-level evidence, narrated in Dora voice per [`SKILL.md`](SKILL.md). Drop it under `docs/examples/`.
- **A new glossary term.** Add to `docs/glossary.md`, following the format there. Character + real-world RE meaning + voice pattern.
- **A canonical episode for v0.2.** See [`docs/TODO-episodes-v2.md`](docs/TODO-episodes-v2.md). Open an issue with the `New Episode` template first so we can align on the Route.
- **A bug or a persona misfire.** If Dora is cheering without evidence, translating literally, or bleeding into files: open an issue with the reproduction.
- **A new install target.** Add a file under `docs/install/` following the shape of the existing ones.

## Style rules

- English for all committed files (`SKILL.md`, docs, examples, code, commit messages, PR bodies, issue text). The Dora voice is **chat-only** — it never enters persistent artifacts.
- Real evidence in examples. Made-up bytes, addresses, or outputs get PRs rejected.
- LF line endings, UTF-8, final newline. `.editorconfig` and `.gitattributes` enforce this.
- Markdown: keep lines readable; no arbitrary hard wraps at 80.

## Commit messages

Conventional Commits:

```
feat(skill): add "Grumpy Old Troll" character for checksum gates
docs(examples): add example-03 uPX unpacking transcript
fix(skill): tighten activation to exclude source-code review
```

No AI attribution lines. No `Co-authored-by: Claude`.

## PR flow

1. Fork.
2. Feature branch: `feat/<topic>`, `fix/<topic>`, `docs/<topic>`.
3. One coherent change per PR.
4. Fill the PR body with what changed and why.
5. If a new example transcript, paste the exact command outputs.
6. If a new episode for v0.2, include at least one worked example.

## Licensing

MIT. By contributing you agree your work ships under MIT.

## Etiquette

This project makes light of a beloved children's character. Contributions must stay affectionate — no crude riffs, no political adjacent stuff, no character defamation. If in doubt, keep it fun-and-nerdy.
