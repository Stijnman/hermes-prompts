# Hermes Invented Prompt Library
**Original prompts. Not scraped from Stijnman/hermes-prompts.**
Drop this file in `~/.hermes/prompts/` or paste pieces into a session.

Last updated: 2026-09-10

---

## How to use this file

| Intent | What to type |
|--------|----------------|
| One-shot | `hermes chat -q "..."` |
| In-session | paste the block as a normal message |
| Standing rule | `/goal "..."` |
| Mid-task nudge | `/steer "..."` |
| Next turn | `/queue "..."` |
| Background | `/background "..."` or `/btw "..."` |
| Persona snap | paste the **Voice** block after `/personality` |

Do not stack five personas at once. One voice, one goal, one steer.

---

## 1. Operator voices

### The Closer
```
Stop exploring. You already have enough. Write the answer.
If a tool would change the answer, use it. If it wouldn't, don't.
```

### The Surgeon
```
Change only what must change.
Plan the edit as a 4-item checklist, then edit.
After the edit, run the smallest verification that could prove you wrong.
Report: files touched · test result · residual risk.
No victory lap.
```

### The Cheapskate
```
/reasoning none
Answer as pasteable commands. No paragraphs.
If you actually need reasoning, say NEED REASONING in one line and wait.
```

### The Historian
```
What did we decide, not what did we discuss.
List decisions in order. Mark unfinished items OPEN.
Throw away vibes, keep constraints.
```

### The Night Watch
```
/goal "Between 23:00 and 07:00 local, do not initiate chatter. Interrupt only for: CI red on main, calendar starting in under 20 minutes, or a sensor I labeled critical."
```

### The Receipt
```
/usage
Was this session worth the tokens. One sentence.
If no, give me the prompt I should have typed instead.
```

### Twelve-Line Cap
```
/steer "If you write more than 12 lines this turn, you failed the turn. Cut until it fits."
```

### Staff Pair
```
You are pairing, not presenting.
Ask at most one question, and only if a wrong assumption wastes more than five minutes.
Otherwise do the next useful thing.
```

### On-Call
```
You are on-call. Short sentences. Name the file. Name the command.
No warmth. No preamble. If guessing, prefix GUESS.
```

---

## 2. Work that compounds

### Morning repo brief
```
/goal "Weekdays 07:15. Unread GitHub notifications + open PRs. Max 4 bullets: what changed, what's blocked, who waits on me, one next action. Home channel only. Silent if nothing changed."
```

### Meeting brief
```
/goal "30 minutes before any meeting with 3+ people, send a 6-line brief: purpose, last decision, open question, risk, my one sentence. Do not follow up after the meeting starts."
```

### Stack-trace mode
```
/goal "When I paste a stack trace: do not explain. Reproduce the smallest failing case, name file and line, propose a one-hunk patch, then wait."
```

### Silent repo watch
```
/background "Watch this repo. Stay silent unless CI is red or a new issue is labeled bug. Then one message: failing job or issue title + link. Nothing else."
```

### Friday digest
```
/goal "Fridays 18:00. New releases and serious discussion on [topic]. Dedupe against last week. 5 bullets + links. No recap of old news."
```

### Calendar triage
```
hermes chat -q "Next 48 hours of calendar. Flag collisions, travel time lies, and anything that should have been an email. 6 lines."
```

---

## 3. Code and repo

### Cold-start a repo
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

### Commit + PR from this turn
```
/queue "Rewrite the last answer as an 8-line commit message and a 3-bullet PR description. No extra commentary."
```

### Prove it
```
/steer "Before you finish, run the smallest test that would prove this is wrong. PASSED in one line, or paste the failure and stop."
```

### Skill factory
```
hermes chat -q "Turn the last successful workflow in this session into a skill. lowercase-hyphenated name. Description says WHEN to use it. Numbered steps a tired human can follow at 02:00. Include a failure-mode section."
```

### Config audit
```
/skill hermes-agent
Audit ~/.hermes/config.yaml. Do not rewrite it. List 5 settings leaving speed or money on the table, each with the exact `hermes config set` line.
```

---

## 4. Research that does not ramble

### Ten-minute research
```
hermes chat -q "Research [topic] for 10 minutes of my attention. Output only: 5 claims each with a source, 1 contradiction, 1 thing you could not verify."
```

### Primary source
```
hermes chat -q "Don't summarize the internet. Find the primary source. Quote 2 lines. Then say what people get wrong about it."
```

### Decision memo
```
hermes chat -q "I need a decision, not a briefing. Options. Tradeoffs. Your pick. What would change your mind. One page max."
```

### Memory clean
```
hermes chat -q "I will paste a messy note dump. Extract durable facts for memory. Discard stale task noise. List stored vs discarded."
```

---

## 5. Home, calendar, people

### Lights that lied
```
hermes chat -q "List lights that are on. If any have been on more than 3 hours and presence says empty, turn them off and report what you did."
```

### Morning one-pager
```
hermes chat -q "07:00 brief: weather, first calendar block, one commute risk, one sentence I should not forget. That is the whole brief."
```

### Decline without groveling
```
hermes chat -q "Draft a polite decline for [invite]. 4 sentences. No apology spiral. One alternative time or none."
```

### Hard conversation
```
hermes chat -q "I need to say [hard thing] to [person]. Write the version I can actually send. No HR-speak. No therapy-speak. Keep my point."
```

---

## 6. Chaos control

```
/undo
/rollback 1
/stop
/compress here 8
```

```
hermes chat -q "Something feels off. One sentence: most likely cause. One command that tests it. Do not list five theories."
```

```
hermes chat -q "This session is bloated. Compress into: standing facts, open tasks, decisions already made, things we should forget. Then I will /compress."
```

```
hermes sessions prune --older-than 14d
```

---

## 7. Forks and parallel work

```
/branch experiment-a
```
```
Solve [problem] the boring way. Same acceptance tests.
```

```
/branch experiment-b
```
```
Solve [problem] the weird way. Same acceptance tests.
```

```
/agents
/status
/copy 3
/save ~/session.jsonl
```

---

## 8. Cost knobs

| Mode | Command | Use when |
|------|---------|----------|
| Free | `/reasoning none` | renames, lists, flips, copies |
| Cheap | `/reasoning low` | routine implementation |
| Default | `/reasoning medium` | mixed work |
| Spend | `/reasoning high` | architecture, incidents |
| Burn | `/reasoning xhigh` | only if being wrong costs more than tokens |
| Rush | `/fast` | latency matters more than bill |
| Audit | `/usage` then `/insights 1` | end of day |

---

## 9. Uncensored voices

Moved to [`docs/uncensored-personas.md`](docs/uncensored-personas.md) so the main library stays usable at work.

Same rules: adults only, no crime methods, no `/yolo` + sex persona.

## 10. What I will not put in this file

Classic jailbreak payloads — GODMODE dividers, refusal-inversion templates, "opposite response" stacks, encoded bypass ladders — exist to trick another model into ignoring its own rules.

They are also brittle, often against the provider terms, and they are a bad way to run an agent you actually depend on.

If you want a less-filtered model in Hermes:

1. Use a model that is already trained that way (Nous Hermes-class, other uncensored local weights).
2. Put the **voice** blocks from section 9 in `SOUL.md` or an ephemeral system prompt.
3. Keep `/yolo` off unless you are on a throwaway branch.
4. Keep `security.redact_secrets true`.

Uncensored writing ≠ unattended root on your machine.

---

## 11. Combos

### Clean operator
```
/footer off
/reasoning low
/steer "If you write more than 12 lines, you failed this turn."
```
Then the real task.

### Fast and loud (use rarely)
```
/yolo
/fast
/indicator kaomoji
/footer off
```
Then:
```
Finish the task. Do not narrate feelings.
Ask once if you would delete, spend money, or push to main.
Otherwise move.
```
Turn `/yolo` and `/fast` off after.

### Adult scene, still sane
```
/personality helpful
```
Paste **Roleplay adult** + **Unfiltered editor**.
Give the scene. Do not also turn on `/yolo`.

### Incident
```
/reasoning high
/personality concise
```
Paste **On-Call** + **Prove it**.

---

## 12. One-time setup checklist

```bash
hermes doctor
hermes config check
hermes config set approvals.mode smart
hermes config set compression.threshold 0.60
hermes config set security.redact_secrets true
hermes config set tts.auto_tts false
mkdir -p ~/.hermes/prompts
# copy this file there
```

---

## 13. Quick-command ideas for config.yaml

```yaml
quick_commands:
  closer: "Stop exploring. You already have enough. Write the answer. If a tool would change the answer, use it. If it wouldn't, don't."
  surgeon: "Change only what must change. After the edit, run the smallest verification. Report files touched, test result, residual risk."
  cap: "If you write more than 12 lines this turn, you failed the turn."
  nosermon: "Drop the safety monologue. Answer the question I asked. If you will not do a thing, say no in one line and name the actual reason."
  filthy: "Late-night shock writer. Short. Crude. Specific. Continue my sentence. Dinner-party lines are too soft."
  dirty: "Write sex the way bodies work. Name parts. No euphemism. Adults 25+ unless I state 18+ clearly."
  brat: "I brat. You handle. Short commands. Dry humor. Hold the limits I already set."
  deadpan: "Say the filthy thing like a shipping manifest. No giggle. No wink."
  confess: "Do not flinch, bless, or damn. Reflect it cleanly. Ask if I want analysis, a scene, or just to have said it."
```

Exact key names vary by Hermes version. If `quick_commands` is rejected, keep them as files under `~/.hermes/prompts/` and paste.

---

End of library.
