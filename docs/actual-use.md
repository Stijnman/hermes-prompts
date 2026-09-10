# Actual-use one-shots

Copy-paste. Restart the gateway after plugin or provider changes.

## Setup

```bash
hermes doctor
hermes config check
hermes -c "terminal(command='echo Setup OK')"
```

## Model

```bash
hermes config set model.provider gemini
hermes config set model.default gemini-3.5-flash
# or
hermes config set model.provider openrouter
hermes config set model.default google/gemma-4-31b-it:free
hermes gateway restart
```

Current Flash IDs as of 2026-09: `gemini-3.8-flash`, `gemini-3.7-flash`, `gemini-3.6-flash`, `gemini-3.5-flash`, `gemini-3.5-flash-lite`.

Native Gemini URL (preferred):

```yaml
base_url: https://generativelanguage.googleapis.com/v1beta
provider: gemini
```

## Search

```bash
hermes chat -q "Search for latest AI news and summarize 3 key stories"
hermes chat -q "Find recent articles about Belgian lottery results"
hermes chat -q "List 5 free OpenRouter models with context length > 100k"
```

## Home Assistant

```bash
hermes plugins enable homeassistant
hermes gateway restart
hermes chat -q "List all lights in the living room"
hermes chat -q "Turn on light.living_room"
hermes chat -q "Set climate.thermostat to 22\u00b0C in heat mode"
```

## Voice

```bash
hermes config set tts.enabled true
hermes config set tts.provider edge
hermes config set tts.auto_tts true
hermes config set voice.default true
```

In session: `/voice on` · `/voice tts` · `/voice off`

## Skills

```bash
hermes skills list
hermes skills search homeassistant
hermes curator status
hermes curator run
```

In session: `/skill hermes-agent`

## Sessions

```bash
/new
/title work-project
hermes --continue
/compress
/snapshot
/goal research "GRPO papers"
/queue "Build a REST API"
/steer "Remember to check DB indexes"
```

## Cost

```
/usage
/insights 1
/insights 7
/reasoning none
/reasoning high
```

## Debug

```bash
hermes doctor --fix
hermes auth list
hermes auth reset openrouter
hermes auth reset gemini
hermes config check
/debug
```

## Power sequences

| Goal | Sequence |
|------|----------|
| HA control | `hermes plugins enable homeassistant && hermes gateway restart && hermes chat -q "List lights"` |
| Voice + search | `hermes config set tts.auto_tts true && hermes chat -q "Search for pizza places"` |
| Fork and test | `/branch` then different prompts per branch |
| Save and resume | `/save ~/session.jsonl` then `hermes --continue` |

## OpenRouter 404

If fallbacks die with `0 endpoints … guardrail restrictions and data policy`:

1. Privacy: allow free endpoints that train and that publish.
2. Turn **Non-frontier ZDR** off if you need free models.
3. Workspaces → Guardrails: `enable_free_model_training` and `enable_free_model_publication` must not be false.
4. Regenerate the key after policy changes.
5. Hermes wants tools; many `:free` endpoints do not support tools. Use a cheap paid model as fallback if chat-only free models keep dying.
