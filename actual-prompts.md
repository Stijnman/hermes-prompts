# Hermes Agent — Actual Use Prompts
# Copy-paste these directly into your Hermes CLI or gateway sessions

---

## 🔧 One-Shot Queries (hermes -c or hermes chat -q)

### Model & Configuration
```bash
# Check current config
hermes config

# Switch to OpenRouter with gemma
hermes config set model.provider openrouter
hermes config set model.default google/gemma-4-31b-it:free

# Enable TTS auto-speaking
hermes config set tts.auto_tts true
hermes config set voice.default true

# Disable pet (set false) or scale (1.5)
hermes config set display.pet.enabled false
hermes config set display.pet.scale 1.5
```

### Web Search
```bash
# Search with Exa (content extraction)
hermes -c "terminal(command='hermes chat -q \"What is the capital of France?\"')"

# Search with Tavily (targeted)
hermes chat -q "Find recent articles about Belgian lottery results"

# Privacy search (no API key needed)
hermes chat -q "SearXNG query: best places to visit in Brussels"

# OpenRouter model fallback test
hermes chat -q "List 5 free OpenRouter models with context length > 100k"
```

### Home Assistant
```bash
# List all entities
hermes tools enable homeassistant  # (then next session)
hermes chat -q "List all lights in the living room"

# Turn on a light
hermes chat -q "Turn on light.living_room"

# Set thermostat temperature
hermes chat -q "Set climate.thermostat to 22°C in heat mode"

# Check entity state
hermes chat -q "What is the state of sensor.temperature?"
```

### Skills & Tools
```bash
# List installed skills
hermes skills list

# Search for a skill
hermes skills search "homeassistant"

# Install a skill from hub
hermes skills install homeassistant-control

# Load a skill into current session
/hermes skills inspect homeassistant-control
# or: /skill homeassistant-control

# Curator status
hermes curator status

# Run manual curator review
hermes curator run
```

### TTS & Voice
```bash
# Test TTS generation
hermes -c "text_to_speech(text='Hello, this is a test')"

# Check TTS provider
hermes config show | grep -A2 "tts:"

# Enable/disable TTS
hermes config set tts.enabled true

# Set voice provider
hermes config set tts.provider edge

# Voice mode commands (in-session)
/voice on     # voice-to-voice mode
/voice tts    # always voice responses
/voice off    # disable voice
```

### Session Management
```bash
# Fresh session
/hermes reset     # or: /new

# Name a session
/hermes title work-project

# Resume session
hermes --continue           # most recent
hermes --resume 20260910_1430_gra7   # specific session

# Compress context (free tokens)
/compress

# Snapshot state
/hermes snapshot
/hermes snapshot restore

# Goal tracking
/hermes goal research "GRPO papers"
/hermes goal status
/hermes goal clear

# Queue for next turn
/hermes queue "Build a REST API"

# Steer without interrupting
/hermes steer "Remember to check DB indexes"
```

### Gateway / Platform
```bash
# Approve/deny pending command
/approve
/deny

# Restart gateway
/hermes gateway restart

# Set home channel
/sethome

# Telegram topic sessions
/topic general

# Platform status
/hermes platforms

# Insights/analytics
/hermes insights 30
/hermes usage

# Dashboard
/hermes dashboard          # launch web dashboard
/herms dashboard --port 9119  # custom port
```

### Plugin Management
```bash
# List plugins
hermes plugins list

# Enable plugins
hermes plugins enable homeassistant
hermes plugins enable web-exa
hermes plugins enable web-tavily
hermes plugins enable web-searxng
hermes plugins enable spotify
hermes plugins enable evey-goals
hermes plugins enable evey-status

# Check specific plugin
hermes plugins enable homeassistant  # takes effect next session
```

### Configuration Deep Dive
```bash
# Show full config
hermes config edit  # opens $EDITOR

# Set specific keys
hermes config set compression.threshold 0.60
hermes config set approvals.mode smart
hermes config set stt.provider groq
hermes config set terminal.backend docker

# Check doctor
hermes doctor

# Check env path
hermes config env-path

# Migrate config
hermes config migrate
```

### Debug & Troubleshooting
```bash
# Upload debug report
/hermes debug

# Check for security advisories
hermes doctor --fix

# Reset exhaustion status
hermes auth reset openrouter

# List stored credentials
hermes auth list

# Reset a provider's status
hermes auth reset gemini

# Config validity check
hermes config check
```

### Batch / Background Tasks
```bash
# Background long task (returns immediately)
terminal(command="hermes chat -q 'Build a FastAPI auth service'", background=true)

# One-shot with timeout
hermes -c "terminal(command='python script.py --arg value', timeout=60)"

# tmux session for interactive work
terminal(command="tmux new-session -d -s agent1 -x 120 -y 40 'hermes'", timeout=10)
terminal(command="sleep 8 && tmux send-keys -t agent1 'Build REST API' Enter", timeout=15)
terminal(command="tmux capture-pane -t agent1 -p", timeout=5)

# Branch/fork session for A/B testing
/hermes branch /fork

# Fast priority toggle
/fast
```

### Model Prompts
```bash
# Test specific model
hermes chat -q "Say 'hello from gemma'"

# Compare model capabilities
hermes chat -q "What can you do? List your top 5 capabilities."

# Context length test
hermes chat -q "Write a 2000-word essay on AI governance and include specific references to at least 3 research papers with author names and year."

# Reasoning level test
/hermes reasoning none
hermes chat -q "Simple math: what is 15 * 27?"
/hermes reasoning high
hermes chat -q "Explain the trade-offs between LoRA and QLoRA for fine-tuning LLMs."
```

---

## 🚀 Quick Start Prompts (Copy & Paste)

### "I want to test my setup"
```bash
hermes doctor
hermes config check
hermes -c "terminal(command='echo Setup OK')"
```

### "Search the web"
```bash
hermes chat -q "Search for latest AI news and summarize 3 key stories"
```

### "Home assistant control"
```bash
hermes plugins enable homeassistant  # first time
hermes chat -q "List all entities"
hermes chat -q "Turn on all lights"
```

### "Enable voice/TTS"
```bash
hermes config set tts.auto_tts true
hermes config set voice.default true
/hermes voice on
```

### "Enable plugins"
```bash
hermes plugins enable homeassistant
hermes plugins enable web-exa
hermes plugins enable spotify
# (restart gateway)
hermes gateway restart
```

### "Check skills and curator"
```bash
hermes skills list
hermes curator status
hermes curator run
```

### "Change model/provider"
```bash
hermes config set model.provider openrouter
hermes config set model.default google/gemma-4-31b-it:free
hermes gateway restart
```

### "Backup / export session"
```bash
hermes sessions export ~/my-session.jsonl
hermes profile export work /path/to/backup.tar.gz
hermes profile import /path/to/backup.tar.gz
```

### "Fork session for testing"
```bash
/hermes branch /fork    # creates branch for A/B testing
# Or use tmux:
terminal(command="tmux new-session -d -s agent2 -x 120 -y 40 'hermes'", timeout=10)
```

### "Cost monitoring"
```bash
/hermes usage          # current session tokens
/hermes insights 7     # last 7 days analytics
/hermes gquota         # Google quota
```

---

## ⚡ Power-User Combinations

| Goal | Prompt Sequence |
|------|----------------|
| "Set up for HA control" | `hermes plugins enable homeassistant && hermes gateway restart && hermes chat -q "List lights"` |
| "Enable voice + search" | `hermes config set tts.auto_tts true && hermes config set voice.default true && hermes chat -q "Search for pizza places"` |
| "Debug model issues" | `hermes doctor && hermes config check && hermes -c "terminal(command='curl -s http://localhost:11434/api/tags')"` |
| "Fork and test" | `/branch /fork` then try different prompts in each session |
| "Save and resume" | `/save ~/session.jsonl` then later `/new` or `hermes --resume session-name` |
| "Plugin switcheroo" | `hermes plugins enable web-exa && hermes chat -q "Search this topic"` vs `hermes plugins enable web-tavily && hermes chat -q "Search this topic"` |
| "Model swap" | `hermes config set model.provider anthropic && hermes gateway restart && hermes chat -q "Same prompt, different model"` |

---

## 📋 Prompt Library (save these)

```bash
# Create prompt directory
mkdir -p ~/.hermes/prompts/

# Save frequently-used prompts
cat > ~/.hermes/prompts/ha-lights.md <<'EOF'
hermes chat -q "Turn on all lights"
EOF

cat > ~/.hermes/prompts/search-ai.md <<'EOF'
hermes chat -q "Latest AI news, 3 key stories, summary"
EOF

cat > ~/.hermes/prompts/model-test.md <<'EOF'
hermes chat -q "What is your context length? List supported modalities."
EOF

# Use: source ~/.hermes/prompts/ha-lights.md
# Or just: hermes chat -q "$(cat ~/.hermes/prompts/ha-lights.md | head -1 | cut -d'"' -f2)"
```

---

## ⚠️ Quick Safety Reminders

| Action | Command | Note |
|--------|---------|------|
| "Reset all security" | `/config set security.redact_secrets false` | Only for debugging — re-enable after |
| "Bypass all approvals" | `hermes --yolo "prompt"` | Redaction still active independently |
| "Disable TTS" | `/config set tts.enabled false` | Overrides `auto_tts` |
| "Smart approvals" | `/config set approvals.mode smart` | Recommended default |
| "Privacy mode" | `/config set privacy.redact_pii true` | Hashes user IDs, strips phone numbers |
| "Full reset to defaults" | `hermes config migrate && hermes gateway restart` | Restores config version v42 schema |

---

**Repository:** `https://github.com/Stijnman/hermes-prompts`

**Last updated:** 2026-09-10

**Test these now:** Start with `hermes doctor` → `hermes config check` → then try the one-shot queries above.