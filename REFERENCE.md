# Hermes Prompts — copy-paste reference

Prompts you paste. Not CLI manuals. Setup is in README.md.

## Quick find

| Goal | Where |
| --- | --- |
| Shorten output | PERSONAS.md — Cheapskate, Twelve-Line Cap |
| Speed | PERSONAS.md — Closer, Surgeon |
| Code review | Surgeon + Prove it + Stack-trace |
| Research | Ten-minute, Primary source, Decision memo |
| Daily | Morning repo brief, Meeting brief, Friday digest |
| Debug | Stack-trace, Prove it, Something feels off |
| Adult | PERSONAS.md |

---

## One-shots (`hermes chat -q`)

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

### Lights that lied
```
hermes chat -q "List lights that are on. If any have been on more than 3 hours and presence says empty, turn them off and report what you did."
```

### Something feels off
```
hermes chat -q "Something feels off. One sentence: most likely cause. One command that tests it. Do not list five theories."
```

### Session bloated
```
hermes chat -q "This session is bloated. Compress into: standing facts, open tasks, decisions already made, things we should forget. Then I will /compress."
```

### Skill factory
```
hermes chat -q "Turn the last successful workflow in this session into a skill. lowercase-hyphenated name. Description says WHEN to use it. Numbered steps a tired human can follow at 02:00. Include a failure-mode section."
```

---

## Standing goals

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

### Friday digest
```
/goal "Fridays 18:00. New releases and serious discussion on [topic]. Dedupe against last week. 5 bullets + links. No recap of old news."
```

### Silent repo watch
```
/background "Watch this repo. Stay silent unless CI is red or a new issue is labeled bug. Then one message: failing job or issue title + link. Nothing else."
```

Clear with `/goal clear`. Status with `/goal status`. Kill background with `/stop`.

---

## Steers and queues

### Prove it
```
/steer "Before you finish, run the smallest test that would prove this is wrong. PASSED in one line, or paste the failure and stop."
```

### Config audit
```
/steer "Audit ~/.hermes/config.yaml. Do not rewrite it. List 5 settings leaving speed or money on the table, each with the exact hermes config set line."
```

### Commit + PR
```
/queue "Rewrite the last answer as an 8-line commit message and a 3-bullet PR description. No extra commentary."
```

### Threat note
```
/background "Last 20 commits. Single riskiest file. One-page threat note: what breaks, who notices, how we'd know. No theater."
```

---

## Cleanup

```
/undo
/rollback 1
/stop
/compress here 8
```

## Forks

```
/branch experiment-a
```
Solve [problem] the boring way. Same acceptance tests.

```
/branch experiment-b
```
Solve [problem] the weird way. Same acceptance tests.

```
/agents
/status
/copy 3
```

## Cost

| Mode | Command | When |
| --- | --- | --- |
| Free | `/reasoning none` | rename, list, copy |
| Cheap | `/reasoning low` | routine code |
| Default | `/reasoning medium` | mixed |
| Spend | `/reasoning high` | architecture, incidents |
| Burn | `/reasoning xhigh` | being wrong costs more than tokens |

End of REFERENCE.md
