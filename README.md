# Hermes Prompts

Useful, unknown, and invented prompts for [Hermes Agent](https://github.com/NousResearch/hermes-agent).

Copy-paste into the CLI or gateway. No API keys live in this repo.

## Start in 60 seconds

```bash
git clone https://github.com/Stijnman/hermes-prompts.git
mkdir -p ~/.hermes/prompts
cp hermes-prompts/LIBRARY.md ~/.hermes/prompts/library.md
cp hermes-prompts/PERSONAS.md ~/.hermes/prompts/personas.md
cp hermes-prompts/REFERENCE.md ~/.hermes/prompts/reference.md
```

Then in a session:

```
/steer "If you write more than 12 lines this turn, you failed the turn."
```

## Find a prompt

| I want to… | File |
| --- | --- |
| Operator voices (Closer, Surgeon, …) | [PERSONAS.md](PERSONAS.md) |
| One-shots (research, code, personal) | [REFERENCE.md](REFERENCE.md) |
| Standing goals / background | [REFERENCE.md](REFERENCE.md) |
| Adult / unfiltered voices | [PERSONAS.md](PERSONAS.md) |
| Full invented library | [LIBRARY.md](LIBRARY.md) |
| Config snippets | [examples/quick-commands.yaml](examples/quick-commands.yaml) |
| Migrating from old files | [MIGRATION.md](MIGRATION.md) |

## Files

| File | What it is |
| --- | --- |
| `LIBRARY.md` | Core invented prompts + indexes |
| `PERSONAS.md` | Work-safe + adult voices, combos, safety |
| `REFERENCE.md` | Copy-paste one-shots and in-session blocks |
| `config/config.example.yaml` | Example config, no secrets |
| `config/env.template` | Blank `.env` shape |
| `archive/` | Pointers to deprecated originals |

## Rules

- Secrets stay in `~/.hermes/.env`. Never in YAML. Never in git.
- Do not pair `/yolo` with an adult persona.
- Uncensored voice ≠ jailbreak. No GODMODE payloads here.
- Adults only in unfiltered personas. If an age could be misread as under 18, stop.

## License

MIT. Fork freely. Do not commit keys.
