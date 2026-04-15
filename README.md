# Squad Features — Quickstart

> **5-minute hands-on tour** of 10 Squad features. Clone, run, see output.
>
> For the *why* behind each feature, read the blog post: [My Favorite Squad Features](https://dfberry.github.io/blog/my-favorite-squad-features).

## Prerequisites

- [Node.js](https://nodejs.org/) 18+
- [GitHub CLI](https://cli.github.com/) (`gh`)

## Quick Start

```bash
git clone https://github.com/dfberry/squad-features.git
cd squad-features
npx @bradygaster/squad-cli schedule list
```

You should see 4 configured schedules (heartbeat, nightly cleanup, startup sync, weekly report). That means it's working — keep going.

## Try Each Feature

### 1. Generic Scheduler

```bash
npx @bradygaster/squad-cli schedule list      # 4 schedules: interval, cron, startup, workflow
npx @bradygaster/squad-cli schedule status    # Which are due now
```

### 2. Two-Pass Issue Scanning

```bash
cat .squad/skills/ralph-two-pass-scan/SKILL.md
```

Shows Pass 1 (lightweight filter) and Pass 2 (full hydration) — the pattern that cuts API calls by ~72%.

### 3. Tiered Agent Memory

```bash
cat .squad/memory/hot/lead.md       # Hot tier — current session
cat .squad/memory/cold/lead.md      # Cold tier — summarized history
cat .squad/memory/wiki/architecture.md  # Wiki tier — durable reference
```

Three files, three tiers. Agents load only what they need.

### 4. Economy Mode

```bash
npx @bradygaster/squad-cli economy status     # Currently: disabled
npx @bradygaster/squad-cli economy on         # Toggle on — cheaper models
npx @bradygaster/squad-cli economy off        # Toggle off — back to standard
```

### 5. Orchestration Logging

```bash
cat .squad/orchestration-log/2026-04-20T14-30-Lead.md
```

A real log: 4 agents, 11 minutes, auth endpoints built — with dispatch table, timeline, decisions, and cost.

### 6. `nap --deep` (Context Hygiene)

```bash
npx @bradygaster/squad-cli nap --deep --dry-run   # Preview what would be cleaned
cat .squad/decisions.md                            # 8 active decisions
cat .squad/decisions-archive.md                    # 3 archived by previous nap
```

### 7. Personal Squad

```bash
cat .squad/personal-agent-example.md    # Example: "Alex" the code reviewer
```

Personal agents travel with you across repos via Ghost Protocol. See the blog post for setup details.

### 8. Cross-Squad Orchestration

```bash
npx @bradygaster/squad-cli discover               # Searches for peer squads
cat .squad/manifest.json                           # This squad's discovery manifest
```

### 9. Circuit Breaker

```bash
cat .squad/ralph-circuit-breaker.json
```

State machine: CLOSED → OPEN (fallback) → HALF-OPEN (recovery). Currently closed with 3 past recoveries.

### 10. Machine Capability Discovery

```bash
cat .squad/machine-capabilities.json
```

Lists what this machine can do (`browser`, `docker`, `azure-cli`…) and what it can't (`gpu`, `azure-speech`…). Ralph skips issues tagged `needs:gpu` on machines without one.

## What's Next

- **[Blog post](https://dfberry.github.io/blog/my-favorite-squad-features)** — explains *why* each feature matters
- **[Squad on GitHub](https://github.com/bradygaster/squad)** — the framework itself
- **[Squad docs](https://squad.dev)** — full reference

## License

MIT
