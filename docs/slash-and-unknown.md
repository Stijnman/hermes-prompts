# Slash commands and unknown gems

Type `/` in a Hermes session. Built-ins are case-insensitive.

## Session

| Command | Alias | What it does |
|---------|-------|----------------|
| `/new [name]` | `/reset` | Fresh session |
| `/title [name]` | | Name the session |
| `/compress [here N \| focus]` | | Compress context |
| `/snapshot [sub]` | | Snapshot config/state |
| `/rollback [N]` | | Restore filesystem checkpoint |
| `/undo [N]` | | Drop last N exchanges |
| `/retry` | | Resend last user message |
| `/branch [name]` | `/fork` | Parallel session |
| `/save [path]` | | Write conversation to file |
| `/copy [N]` | | Copy last N replies |
| `/status` | | Session / model / tokens |
| `/history` | | Conversation history |

## Control

| Command | Alias | What it does |
|---------|-------|----------------|
| `/goal [text\|pause\|resume\|clear\|status]` | | Standing objective |
| `/subgoal [text\|remove N\|clear]` | | Extra criteria on the goal |
| `/background <prompt>` | `/bg` `/btw` | Run in background |
| `/queue <prompt>` | `/q` | Next turn, do not interrupt |
| `/steer <prompt>` | | Inject after next tool call |
| `/stop` | | Kill background jobs |
| `/agents` | `/tasks` | Active agents |
| `/yolo` | | Skip dangerous-command approvals |
| `/fast` | | Priority processing |
| `/approve` `/deny` | | Gateway pending command |

## Model and UX

| Command | What it does |
|---------|----------------|
| `/model [name]` | Show or switch model |
| `/personality [name]` | Personality profile |
| `/reasoning [none\|low\|medium\|high\|xhigh\|show\|hide]` | Effort + display |
| `/voice [on\|off\|tts]` | Voice mode |
| `/verbose` | Cycle verbosity |
| `/footer [on\|off]` | Runtime footer |
| `/skin [name]` | Theme (`system`, `nord`, `space`, …) |
| `/indicator [style]` | Busy spinner (`emoji`, `kaomoji`, …) |
| `/statusbar` | Toggle status bar |
| `/busy [sub]` | What Enter does while working |

## Skills, curator, system

| Command | What it does |
|---------|----------------|
| `/skill <name>` | Load a skill |
| `/reload-skills` | Rescan `~/.hermes/skills/` |
| `/reload-mcp` | Reload MCP servers |
| `/curator status` `/curator run` | Skill curator |
| `/kanban` | Multi-profile board |
| `/blueprint` `/bp` | Automation from template |
| `/suggestions` | Accept/dismiss automations |
| `/memory` | Pending memory writes |
| `/bundles` | Skill bundles |
| `/commands [page]` | Paginated command list |
| `/help` | Help |
| `/usage` | Token use |
| `/insights [days]` | Analytics |
| `/debug` | Shareable debug bundle |
| `/version` `/v` | Version |
| `/restart` | Drain + restart gateway |
| `/whoami` | Access level |
| `/sethome` | Home channel |
| `/platforms` | Gateway platform status |
| `/topic` | Telegram DM topics |

## Hidden gems

```
/indicator kaomoji
/footer off
/skin nord
/yolo
hermes --yolo "one shot, no approvals"
/fast
/steer "Remember to check indexes"
/goal status
/compress here 8
```

Theater combo (throwaway branches only):

```
/yolo
/fast
/indicator kaomoji
/footer off
```

Better combo:

```
/footer off
/reasoning low
/steer "If you write more than 12 lines this turn, you failed the turn."
```

## Config keys (`hermes config set`)

| Key | Sensible value |
|-----|----------------|
| `model.default` | `gemini-3.5-flash` or `gemini-3.8-flash` |
| `model.provider` | `gemini` or `openrouter` |
| `approvals.mode` | `smart` |
| `compression.threshold` | `0.60` |
| `security.redact_secrets` | `true` |
| `tts.auto_tts` | `false` until you want it |
| `display.pet.enabled` | taste |
| `terminal.backend` | `local` or `docker` |

## CLI you will actually use

```bash
hermes doctor
hermes config check
hermes config set KEY VALUE
hermes auth list
hermes auth reset PROVIDER
hermes skills list
hermes skills search QUERY
hermes plugins list
hermes sessions prune --older-than 30d
hermes profile export NAME /path/to/backup.tar.gz
```
