# Hermes Prompts

Useful, unknown, and invented prompts for [Hermes Agent](https://github.com/NousResearch/hermes-agent).

Copy-paste into the CLI or gateway. No API keys live in this repo.

```
hermes-prompts/
├── README.md
├── LICENSE
├── .gitignore
├── LIBRARY.md                 # one-file library (start here)
├── ALL-IN-ONE.md              # concatenated offline read
├── docs/
│   ├── slash-and-unknown.md   # slash commands + hidden gems
│   ├── actual-use.md          # copy-paste one-shots
│   └── uncensored-personas.md # adult / no-sermon voices
├── config/
│   ├── config.example.yaml    # safe example config
│   └── env.template           # ~/.hermes/.env shape, keys blank
└── examples/
    └── quick-commands.yaml    # optional quick_commands snippet
```

## Start in 60 seconds

```bash
git clone https://github.com/Stijnman/hermes-prompts.git
mkdir -p ~/.hermes/prompts
cp hermes-prompts/LIBRARY.md ~/.hermes/prompts/library.md
```

Then in a Hermes session:

```
/steer "If you write more than 12 lines this turn, you failed the turn."
```

Or paste any block from `LIBRARY.md`.

## What is in here

| File | What it is |
|------|------------|
| `LIBRARY.md` | Operator voices, standing goals, research, recovery, combos |
| `ALL-IN-ONE.md` | Entire library concatenated |
| `docs/slash-and-unknown.md` | Slash commands, config keys, hidden gems |
| `docs/actual-use.md` | One-shot `hermes chat -q` and setup sequences |
| `docs/uncensored-personas.md` | Adult / filthy / no-sermon personas |
| `config/config.example.yaml` | Example `~/.hermes/config.yaml` (no secrets) |
| `config/env.template` | Example `~/.hermes/.env` (blank keys) |
| `actual-prompts.md` | Original one-shot list |
| `useful-unknown-prompts.md` | Original unknown-gems list |

## Rules of the road

- Secrets stay in `~/.hermes/.env`. Never in `config.yaml`. Never in git.
- `/yolo` skips approvals. Do not pair it with a sex persona. Do not leave it on.
- Uncensored **voice** ≠ jailbreak exploit. This repo does not ship GODMODE payloads.
- Adults only in the persona file. If an age could be misread as under 18, stop.

## Suggested first config

```bash
hermes doctor
hermes config check
hermes config set approvals.mode smart
hermes config set compression.threshold 0.60
hermes config set security.redact_secrets true
```

Primary model IDs that existed in September 2026:

- `gemini-3.8-flash` (newest Flash)
- `gemini-3.5-flash` (safe default)
- Native Gemini base URL: `https://generativelanguage.googleapis.com/v1beta`

OpenRouter `:free` models often 404 if workspace guardrails or ZDR block free endpoints that train or publish. That is an account setting, not a dead slug.

## License

MIT. Prompts are yours to fork. Do not commit keys.
