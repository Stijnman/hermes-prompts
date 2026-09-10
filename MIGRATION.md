# Migration guide

## Where things went

| Old | New |
| --- | --- |
| `actual-prompts.md` | [REFERENCE.md](REFERENCE.md) + [PERSONAS.md](PERSONAS.md) |
| `useful-unknown-prompts.md` | [REFERENCE.md](REFERENCE.md) + [LIBRARY.md](LIBRARY.md) |
| `docs/actual-use.md` | [REFERENCE.md](REFERENCE.md) |
| `docs/slash-and-unknown.md` | `/help` in Hermes. Note in `docs/SLASH_COMMANDS_MOVED.md` |
| `docs/uncensored-personas.md` | [PERSONAS.md](PERSONAS.md) adult section |

## Update a local install

```bash
git pull origin main
mkdir -p ~/.hermes/prompts
cp LIBRARY.md PERSONAS.md REFERENCE.md ~/.hermes/prompts/
```

Config templates did not move.

Prompts themselves are still paste-compatible. Only the file names changed.
