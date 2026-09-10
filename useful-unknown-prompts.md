# Useful and Unknown Hermes Agent Prompts

A curated collection of Hermes Agent prompts, commands, and tricks — categorized for easy discovery. Some are hidden slash commands, some are configuration tips, and others are power-user workflows.

---

## 📡 Slash Commands (Type `/` in-session)

| Command | Description | Example |
|---------|-------------|---------|
| `/new` / `reset` | Fresh session, clears context | `/new` |
| `/title [name]` | Name the session for later resume | `/title work-project` |
| `/compress` | Manually compress context to free tokens | `/compress` |
| `/snapshot [sub]` | Create/restore state snapshots of Hermes config/state | `/snapshot` |
| `/goal [text|sub]` | Set a standing goal Hermes works on across turns | `/goal research grpo papers`<br>`/goal status` — shows progress<br>`/goal clear` — clears standing goal |
| `/background <prompt>` | Run prompt in background (non-interactive) | `/background Research GRPO papers` |
| `/queue <prompt>` | Queue for next turn | `/queue Build a FastAPI service` |
| `/steer <prompt>` | Inject a message after the next tool call without interrupting | `/steer Remember to check the DB indexes` |
| `/stop` | Kill background processes | `/stop` |
| `/rollback [N]` | Restore filesystem checkpoint (N = snapshot number) | `/rollback 3` |
| `/undo` | Remove last exchange | `/undo` |
| `/help` | Show all commands | `/help` |
| `/commands [page]` | Browse all commands (gateway) | `/commands` |
| `/usage` | Token usage summary | `/usage` |
| `/insights [days]` | Usage analytics | `/insights 30` |
| `/profile` | Active profile info | `/profile` |
| `/status` | Session info | `/status` |
| `/debug` | Upload debug report and get shareable links | `/debug` |

---

## ⚙️ Configuration Commands (In-session)

| Command | Description | Usage |
|---------|-------------|-------|
| `/config` | Show current config | `/config` |
| `/model [name]` | Show or change model | `/model gemini-3.5-flash` |
| `/personality [name]` | Set personality | `/personality helpful` |
| `/reasoning [level]` | Set reasoning level (none|minimal|low|medium|high|xhigh|show|hide) | `/reasoning low` |
| `/verbose` | Cycle: off → new → all → verbose | `/verbose` |
| `/voice [on|off|tts]` | Voice mode | `/voice on` / `/voice tts` / `/voice off` |
| `/yolo` | Toggle approval bypass | `/yolo` |
| `/busy [sub]` | Control what Enter does while Hermes is working | `/busy queue` |
| `/indicator [style]` | Pick TUI busy-indicator style | `/indicator emoji` |
| `/footer [on|off]` | Toggle footer on final replies | `/footer off` |
| `/skin [name]` | Change theme | `/skin dark` |
| `/statusbar` | Toggle status bar | `/statusbar` |

---

## 🛠️ Tool & Skill Management

| Prompt/Action | Description |
|---------------|-------------|
| `hermes tools list` | Show all tools and status |
| `hermes tools enable NAME` | Enable a toolset | `hermes tools enable web` |
| `hermes tools disable NAME` | Disable a toolset | `hermes tools disable browser` |
| `hermes skills list` | List installed skills |
| `hermes skills search QUERY` | Search the skills hub | `hermes skills search "homeassistant"` |
| `hermes skills install ID` | Install a skill (hub ID or URL) | `hermes skills install agentskill-id` |
| `hermes skills inspect ID` | Preview without installing | `hermes skills inspect some-skill` |
| `hermes skills config` | Enable/disable skills per platform |
| `hermes skills check` | Check for updates |
| `hermes skills update` | Update outdated skills |
| `hermes skills uninstall N` | Remove a hub skill |
| `/skill <name>` | Load a skill into session | `/skill hermes-agent` |
| `/reload-skills` | Re-scan `~/.hermes/skills/` for added/removed skills |
| `/curator status` | Curator skill lifecycle status |
| `/curator run` | Run manual curator review |

---

## 🔧 Handy Config Settings (via `hermes config set`)

| Key | Default | Example |
|-----|---------|-------|
| `model.default` | gemini-3.5-flash | `hermes config set model.default google/gemma-4-31b-it:free` |
| `model.provider` | openrouter | `hermes config set model.provider openrouter` |
| `voice.default` | false | `hermes config set voice.default true` — TTS on by default |
| `tts.auto_tts` | false | `hermes config set tts.auto_tts true` — auto-speak responses |
| `display.pet.enabled` | true | `hermes config set display.pet.enabled false` / `true` |
| `display.pet.scale` | 0.5 | `hermes config set display.pet.scale 1.5` — 150% pet |
| `compression.threshold` | 0.70 | `hermes config set compression.threshold 0.60` |
| `approvals.mode` | manual | `hermes config set approvals.mode smart` |
| `security.redact_secrets` | true | `hermes config set security.redact_secrets false` (debug only) |
| `stt.provider` | local | `hermes config set stt.provider groq` |
| `tts.provider` | edge | `hermes config set tts.provider elevenlabs` |
| `terminal.backend` | local | `hermes config set terminal.backend docker` |
| `cron.provider` | built-in | `hermes config set cron.provider chronos` |

---

## 💡 Power-User Workflows

### **One-shot batch tasks:**
```bash
# Research multiple topics in one query
hermes chat -q "Research GRPO, LoRA, and QLoRA. Compare trade-offs and write a 3-paragraph summary."

# Run a single query and exit (no PTY needed)
hermes -c "terminal(command='echo hello')"

# Background long task (returns immediately)
terminal(command="hermes chat -q 'Build a REST API for user management'", background=true)
```

### **Session management:**
```bash
# Resume most recent session
terminal(command="tmux new-session -d -s resumed 'hermes --continue'", timeout=10)

# Resume specific session by ID
terminal(command="tmux new-session -d -s resumed 'hermes --resume 20260225_143052_a1b2c3'", timeout=10)

# Rename a session
hermes sessions rename ID T R

# Delete old sessions
hermes sessions prune --older-than 30d
```

### **Profile switching:**
```bash
# List profiles
hermes profile list

# Create a new profile (clone current)
hermes profile create my-work-profile --clone

# Switch to a different profile
hermes profile use my-work-profile

# Export/import profile for backup
hermes profile export NAME /path/to/backup.tar.gz
hermes profile import /path/to/backup.tar.gz
```

---

## 🔍 Unknown / Hidden Gems

| Prompt | What It Does |
|--------|-------------|
| `/indicator kaomoji` | Changes the busy indicator to Japanese emoticons (¯\\_(ツ)_/¯) |
| `/footer off` | Removes the runtime-metadata footer from final replies — cleaner output |
| `/skin system` / `/skin nord` / `/space` | Theme switchers (if available on your skin set) |
| `/yolo` + `hermes --yolo "prompt"` | Skip ALL approval prompts for that invocation only |
| `/save` | Save conversation to file (CLI) — `/save ~/my-session.jsonl` |
| `/copy [N]` | Copy the last assistant response to clipboard (CLI) — `/copy 3` copies last 3 |
| `/branch /fork` | Branch the current session for parallel experimentation |
| `/fast` | Toggle priority/fast processing (may speed up response at higher cost) |
| `/branch` | Fork the current session — useful for A/B testing different prompts |
| `/redirect` | Redirect future outputs to a different channel (gateway) |
| `/approve` / `/deny` | Approve/deny a pending gateway command (when in gateway mode) |
| `/pairing` / `/approve` / `/revoke` | DM authorization for gateway platforms (Telegram, Discord) |

---

## 📊 Token & Cost Monitoring

| Prompt | What It Shows |
|--------|---------------|
| `/usage` | Current session token usage (input + output) |
| `/insights [days]` | Analytics: tokens used, models, costs, top tools |
| `/gquota` | Google Gemini Code Assist quota (CLI) |
| `/curator insights` | Curator-side skill usage stats |

**Pro tip:** Set `/reasoning none` for simple tasks — reduces cost and latency. Use `/reasoning high` or `/reasoning show` only when you need to see the model's thought process.

---

## 🌐 Gateway-Specific (messaging platforms)

| Prompt | Platform | What It Does |
|--------|----------|-------------|
| `/approve` | gateway | Approve a pending command |
| `/deny` | gateway | Deny a pending command |
| `/restart` | gateway | Restart the gateway service |
| `/sethome` | gateway | Set current chat as home channel |
| `/topic [sub]` | Telegram | Enable/disable DM topic sessions |
| `/platforms` | gateway | Show platform connection status |
| `/gquota` | gateway | Google Gemini Code Assist quota |

---

## 📦 Skill Authoring (for advanced users)

If you want to create your own reusable Hermes skills:

```bash
# Create a new skill directory
mkdir -p ~/.hermes/skills/my-cool-skill/

# Create SKILL.md with frontmatter
cat > ~/.hermes/skills/my-cool-skill/SKILL.md <<'EOF'
---
name: my-cool-skill
description: Use when I need to do something cool. One-line behavior.
version: 1.0.0
author: Me
license: MIT
metadata:
  hermes:
    tags: [productivity, automation]
    related_skills: []
---
# My Cool Skill

## Overview
One or two paragraphs: what and why.

## When to Use
- Trigger 1
- Trigger 2

## Common Pitfalls
1. Don't do X
2. Watch out for Y

## Verification Checklist
- [ ] Checklist item 1
- [ ] Checklist item 2

EOF

# Now load it into the session
/hermes skills inspect my-cool-skill
# or just: /skill my-cool-skill
```

---

## 🛡️ Security & Privacy Prompts

| Prompt | Effect |
|--------|--------|
| `/config set security.redact_secrets true` | On by default — redacts API keys from tool output |
| `/config set privacy.redact_pii true` | Hashes user IDs, strips phone numbers from session context |
| `/config set approvals.mode smart` | Smart auto-approve low-risk, prompt on high-risk |
| `/config set tts.enabled false` | Disable TTS entirely |
| `/config set tts.auto_tts false` | Don't auto-speak responses |
| `/yolo` | Bypass all approvals for one invocation |

---

## 🔐 Secrets & Credential Management

| Prompt / Command | What It Does |
|------------------|-------------|
| `hermes auth list` | List all stored API keys and credentials per provider |
| `hermes auth add PROVIDER` | Add a new API key for a provider interactively | `hermes auth add openrouter` |
| `hermes auth remove PROVIDER` | Remove a stored credential | `hermes auth remove openrouter` |
| `hermes auth reset PROVIDER` | Clear exhaustion/status for a provider | `hermes auth reset openrouter` |
| `hermes auth` | Interactive credential manager (gateway `/auth` menu) | Full OAuth and API key setup flow |
| `hermes config set <provider>.key_env <VAR>` | Set which env var holds the API key | `hermes config set providers.gemini.key_env GOOGLE_API_KEY` |
| `hermes config env-path` | Print path to `.env` file | Use to manually edit API keys |
| `HERMES_API_KEY` / `OPENROUTER_API_KEY` / `GOOGLE_API_KEY` | Env vars placed in `~/.hermes/.env` | Never commit these to git — keep in `.env` (chmod 600) |
| `hermes config set security.redact_secrets true` | On by default — redacts credential-like strings from tool output before they enter context | ✅ Recommended keep enabled |
| `/config set privacy.redact_pii true` | Hashes user IDs, strips phone numbers from session context before model sees them | 🔒 Privacy protection |
| `/yolo` | Bypass ALL approvals AND secret redaction for one invocation only | 🚨 Use only for debugging — never with sensitive data |
| `hermes doctor` | Checks for missing/outdated config, validates API key presence | 🏥 Run regularly to verify your setup |
| `hermes config check` | Quick config validity scan | ⚡ Fast status check |

### **Rotating / Refreshing Keys:**

```bash
# 1. Get new key from provider dashboard
# 2. Edit .env directly (recommended):
nano ~/.hermes/.env
# 3. Update the specific key line
# 4. Restart Hermes so new key loads:
hermes gateway restart
# 5. Or reset exhaustion status:
hermes auth reset openrouter
```

### **Best Practices:**

| Practice | Command / Note |
|----------|---------------|
| **Keep redaction on** | `/config set security.redact_secrets true` — never disable unless debugging |
| **Use `.env` not config.yaml** | API keys → `~/.hermes/.env` (chmod 600), never in git |
| **Rotate regularly** | `hermes auth reset <provider>` clears exhaustion state |
| **Never use `--yolo` with real keys** | Bypass disables secret redaction too |
| **Check doctor after changes** | `hermes doctor` validates all keys are present and valid |
| **Use `hermes config env-path`** | Find `.env` path quickly for manual edits |
| **Credential pools** | Multiple keys per provider rotate automatically; `hermes auth list` shows order |

---

## 🔍 Quick Secrets Checklist

Before running sensitive tasks, verify:

- [ ] `hermes doctor` passes with no warnings
- [ ] `.env` file has correct keys (not checked into git)
- [ ] `security.redact_secrets: true` in config
- [ ] `privacy.redact_pii: true` in config (recommended)
- [ ] Provider keys have not expired
- [ ] `--yolo` is NOT used with real data
- [ ] `hermes auth list` shows expected providers
- [ ] `hermes config check` returns no errors

---

## 🛡️ Security & Privacy Prompts (recap)

| Prompt | Effect |
|--------|--------|
| `/config set security.redact_secrets true` | On by default — redacts API keys from tool output |
| `/config set privacy.redact_pii true` | Hashes user IDs, strips phone numbers from session context |
| `/config set approvals.mode smart` | Smart auto-approve low-risk, prompt on high-risk |
| `/config set tts.enabled false` | Disable TTS entirely |
| `/config set tts.auto_tts false` | Don't auto-speak responses |
| `/yolo` | Bypass all approvals for one invocation |

---

**Last updated:** 2026-09-10

**Repository:** `https://github.com/Stijnman/hermes-prompts`

**Feel free to:**
- Fork this repo and add your own prompts
- Open issues with prompts you've discovered
- Submit PRs with new categories or workflows
- Use `hermes curator status` to see which skills are most active
- Use `hermes auth list` to view stored credentials
- Use `hermes auth add/remove/reset` to manage API keys