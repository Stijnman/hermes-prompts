# Hermes Invented Prompt Library

Original prompts. Drop in `~/.hermes/prompts/` or paste.

Last updated: 2026-09-10

## Quick find

| Goal | Where |
| --- | --- |
| Voices | [PERSONAS.md](PERSONAS.md) |
| One-shots and goals | [REFERENCE.md](REFERENCE.md) |
| Code / debug | § 3 below + Prove it |
| Research | § 4 + REFERENCE.md |
| Chaos | § 6 |

## How to use

| Intent | Command |
| --- | --- |
| One-shot | `hermes chat -q "..."` |
| In-session | paste the block |
| Standing | `/goal "..."` |
| Nudge | `/steer "..."` |
| Next turn | `/queue "..."` |
| Background | `/background "..."` |
| Voice | paste after `/personality` |

Golden rule: one voice, one goal, one steer.

## 1. Operator voices

Canonical text: [PERSONAS.md](PERSONAS.md)

Closer · Surgeon · Cheapskate · Historian · Night Watch · Receipt · Twelve-Line Cap · Staff Pair · On-Call

## 2. Work that compounds

Canonical text: [REFERENCE.md](REFERENCE.md)

Morning repo brief · Meeting brief · Stack-trace mode · Silent repo watch · Friday digest

## 3. Code and repo

### Prove it
```
/steer "Before you finish, run the smallest test that would prove this is wrong. PASSED in one line, or paste the failure and stop."
```

### Stack-trace mode
```
/goal "When I paste a stack trace: do not explain. Reproduce the smallest failing case, name file and line, propose a one-hunk patch, then wait."
```

### Cold-start
```
hermes chat -q "Don't search the internet. Inspect this repo as-is. 5 bullets: entrypoint, data flow, biggest smell, safest first PR, test command after the PR."
```

### Smallest script
```
hermes chat -q "Write the smallest script that would have saved me from repeating this task. No framework. No extra files. --help must work."
```

### Three approaches, then 20 minutes
```
hermes chat -q "Three approaches for [problem]. Table: approach · time-to-first-win · failure mode · when to abandon. Pick one. Implement only the first 20 minutes of work."
```

### Threat note
```
/background "Last 20 commits. Single riskiest file. One-page threat note: what breaks, who notices, how we'd know. No theater."
```

### Commit + PR
```
/queue "Rewrite the last answer as an 8-line commit message and a 3-bullet PR description. No extra commentary."
```

### Skill factory
```
hermes chat -q "Turn the last successful workflow in this session into a skill. lowercase-hyphenated name. Description says WHEN to use it. Numbered steps a tired human can follow at 02:00. Include a failure-mode section."
```

## 4. Research

See [REFERENCE.md](REFERENCE.md): ten-minute research, primary source, decision memo, memory clean.

## 5. Home, calendar, people

See [REFERENCE.md](REFERENCE.md): morning one-pager, decline, hard conversation, lights that lied.

## 6. Chaos control

```
/undo
/rollback 1
/stop
/compress here 8
```

```
hermes chat -q "This session is bloated. Compress into: standing facts, open tasks, decisions already made, things we should forget. Then I will /compress."
```

```
hermes chat -q "Something feels off. One sentence: most likely cause. One command that tests it. Do not list five theories."
```

## 7. Forks

```
/branch experiment-a
```
boring way, same tests

```
/branch experiment-b
```
weird way, same tests

```
/agents
/status
/copy 3
```

## 8. Cost knobs

| Mode | Command |
| --- | --- |
| Free | `/reasoning none` |
| Cheap | `/reasoning low` |
| Default | `/reasoning medium` |
| Spend | `/reasoning high` |
| Burn | `/reasoning xhigh` |

## 9. Personas and safety

[PERSONAS.md](PERSONAS.md) — work-safe + adult + combos.

No `/yolo` with adult voices. No GODMODE in this repo.

## 10. Setup

```bash
hermes doctor
hermes config check
hermes config set approvals.mode smart
hermes config set compression.threshold 0.60
hermes config set security.redact_secrets true
mkdir -p ~/.hermes/prompts
cp LIBRARY.md PERSONAS.md REFERENCE.md ~/.hermes/prompts/
```

Quick commands: [examples/quick-commands.yaml](examples/quick-commands.yaml)

End of LIBRARY.md
