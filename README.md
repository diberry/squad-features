# Squad Features — Sample Repository

> Companion repo for the blog post [My Favorite Squad Features (And Why They Matter)](https://dfberry.github.io/blog/my-favorite-squad-features).

This is a working Squad project you can clone and explore. Each feature from the blog post has real configuration files, skill documents, and sample data you can inspect and try.

## Prerequisites

- **Node.js** 20+ ([download](https://nodejs.org/))
- **GitHub CLI** (`gh`) — [install](https://cli.github.com/)
- **Squad CLI** — `npm install -g @bradygaster/squad-cli` or use `npx @bradygaster/squad-cli`

## Quick Start

```bash
# Clone
git clone https://github.com/dfberry/squad-features.git
cd squad-features

# Explore the squad structure
ls .squad/

# Try Squad commands (if Squad CLI is installed)
npx @bradygaster/squad-cli cast        # See the team roster
npx @bradygaster/squad-cli schedule list  # See scheduled tasks
```

---

## Feature 1: Generic Scheduler

Unifies cron jobs, polling loops, and manual triggers in one file.

**Try it:**
```bash
cat .squad/schedule.json                    # See the schedule config
npx @bradygaster/squad-cli schedule list    # List all schedules
npx @bradygaster/squad-cli schedule status  # Check run times
```

**Key file:** [`.squad/schedule.json`](.squad/schedule.json) — defines a Ralph heartbeat (every 5min), nightly cleanup (cron), startup sync, and weekly report.

---

## Feature 2: Two-Pass Issue Scanning

Cuts GitHub API calls by ~72% by separating lightweight list scanning from full issue hydration.

**Try it:**
```bash
cat .squad/skills/ralph-two-pass-scan/SKILL.md  # See the two-pass config
npx @bradygaster/squad-cli ralph watch --duration 30s --verbose  # Watch it in action
```

**Key file:** [`.squad/skills/ralph-two-pass-scan/SKILL.md`](.squad/skills/ralph-two-pass-scan/SKILL.md) — Pass 1 filters by assignee, labels, and title patterns. Pass 2 hydrates only survivors.

---

## Feature 3: Tiered Agent Memory

Three-tier memory model (hot/cold/wiki) reduces context per spawn by 20–55%.

**Try it:**
```bash
cat .squad/skills/tiered-memory/SKILL.md   # See tier definitions
cat .squad/memory/hot/lead.md              # Hot: current session context
cat .squad/memory/cold/lead.md             # Cold: summarized history
cat .squad/memory/wiki/architecture.md     # Wiki: durable reference
```

**Key files:** [`.squad/skills/tiered-memory/SKILL.md`](.squad/skills/tiered-memory/SKILL.md), [`.squad/memory/`](.squad/memory/)

---

## Feature 4: Economy Mode

Shifts model selection to cost-optimized alternatives without overriding explicit user preferences.

**Try it:**
```bash
cat .squad/config.json                         # See current config (economyMode: false)
cat .squad/skills/economy-mode/SKILL.md        # See the economy model table
```

To enable economy mode, set `"economyMode": true` in `.squad/config.json`, or say "use economy mode" in a Squad session.

**Key files:** [`.squad/config.json`](.squad/config.json), [`.squad/skills/economy-mode/SKILL.md`](.squad/skills/economy-mode/SKILL.md)

---

## Feature 5: Orchestration Logging

Every multi-agent task gets a timestamped log showing dispatch, timeline, decisions, and files changed.

**Try it:**
```bash
cat .squad/orchestration-log/2026-04-20T14-30-Lead.md  # Real orchestration log
```

The log shows a 4-agent fan-out that implemented auth endpoints in 11 minutes: dispatch table, timeline, decisions made, files changed, and cost metrics.

**Key file:** [`.squad/orchestration-log/2026-04-20T14-30-Lead.md`](.squad/orchestration-log/2026-04-20T14-30-Lead.md)

---

## Feature 6: `squad nap --deep`

Context hygiene — compresses histories, prunes logs, archives stale decisions.

**Try it:**
```bash
cat .squad/decisions.md             # Active decisions (8 entries)
cat .squad/decisions-archive.md     # Archived decisions (moved by nap --deep)
cat .squad/skills/nap/SKILL.md      # How nap works

# Run it (if Squad CLI is installed)
npx @bradygaster/squad-cli nap --dry-run   # Preview cleanup
npx @bradygaster/squad-cli nap --deep      # Full cleanup
```

**Key files:** [`.squad/decisions.md`](.squad/decisions.md), [`.squad/decisions-archive.md`](.squad/decisions-archive.md)

---

## Feature 7: Personal Squad

Personal agents that travel with you across projects via Ghost Protocol.

**Try it:**
```bash
cat .squad/skills/personal-squad/SKILL.md     # How personal squads work
cat .squad/personal-agent-example.md          # Example personal agent charter

# Set up your own (if Squad CLI is installed)
npx @bradygaster/squad-cli personal init
npx @bradygaster/squad-cli personal add alex --role "Code Reviewer"
npx @bradygaster/squad-cli cast               # See project + personal agents
```

Personal agents live in `~/.config/squad/personal-squad/` (Linux/macOS) or `%APPDATA%\squad\personal-squad\` (Windows) and are auto-discovered.

**Key files:** [`.squad/skills/personal-squad/SKILL.md`](.squad/skills/personal-squad/SKILL.md), [`.squad/personal-agent-example.md`](.squad/personal-agent-example.md)

---

## Feature 8: Cross-Squad Orchestration

Squads discover each other via manifests and delegate work across repo boundaries.

**Try it:**
```bash
cat .squad/manifest.json                       # This squad's manifest
cat .squad/skills/cross-squad/SKILL.md         # Discovery + delegation patterns

# Discover squads (if Squad CLI is installed)
npx @bradygaster/squad-cli discover
```

The manifest declares capabilities, accepted work types, and contact info. Other squads use it to route work here.

**Key files:** [`.squad/manifest.json`](.squad/manifest.json), [`.squad/skills/cross-squad/SKILL.md`](.squad/skills/cross-squad/SKILL.md)

---

## Feature 9: Circuit Breaker

Classic circuit breaker pattern for model rate limits — automatic fallback to free-tier models with self-healing.

**Try it:**
```bash
cat .squad/ralph-circuit-breaker.json          # State machine file
cat .squad/skills/circuit-breaker/SKILL.md     # How it works
```

States: **CLOSED** (normal) → **OPEN** (fallback to free-tier) → **HALF-OPEN** (testing recovery). Cooldown is configurable.

**Key files:** [`.squad/ralph-circuit-breaker.json`](.squad/ralph-circuit-breaker.json), [`.squad/skills/circuit-breaker/SKILL.md`](.squad/skills/circuit-breaker/SKILL.md)

---

## Feature 10: Machine Capability Discovery

Auto-detects what each machine can do and routes work accordingly. Issues with `needs:*` labels are skipped on machines missing those capabilities.

**Try it:**
```bash
cat .squad/machine-capabilities.json               # This machine's capabilities
cat .squad/skills/capability-discovery/SKILL.md     # How routing works
```

Ralph checks `needs:*` labels against the machine's `capabilities` array. Missing capabilities → issue skipped.

**Key files:** [`.squad/machine-capabilities.json`](.squad/machine-capabilities.json), [`.squad/skills/capability-discovery/SKILL.md`](.squad/skills/capability-discovery/SKILL.md)

---

## Repository Structure

```
.squad/
├── charter.md                    # Team charter
├── config.json                   # Squad config (economy mode, model overrides)
├── decisions.md                  # Active team decisions
├── decisions-archive.md          # Archived decisions (from nap --deep)
├── manifest.json                 # Cross-squad discovery manifest
├── machine-capabilities.json     # Machine capability declaration
├── personal-agent-example.md     # Example personal agent charter
├── ralph-circuit-breaker.json    # Circuit breaker state machine
├── schedule.json                 # Generic scheduler config
├── memory/
│   ├── hot/lead.md               # Hot tier: current session context
│   ├── cold/lead.md              # Cold tier: summarized history
│   └── wiki/architecture.md      # Wiki tier: durable reference
├── orchestration-log/
│   └── 2026-04-20T14-30-Lead.md  # Sample multi-agent orchestration log
└── skills/
    ├── capability-discovery/      # Machine capability routing
    ├── circuit-breaker/           # Rate limit fallback
    ├── cross-squad/               # Cross-squad orchestration
    ├── economy-mode/              # Cost-optimized model selection
    ├── nap/                       # Context hygiene
    ├── personal-squad/            # Personal agent management
    ├── ralph-two-pass-scan/       # Two-pass issue scanning
    └── tiered-memory/             # Three-tier memory model
```

## Learn More

- [Squad on GitHub](https://github.com/bradygaster/squad)
- [Squad documentation](https://squad.dev)
- [Blog post: My Favorite Squad Features](https://dfberry.github.io/blog/my-favorite-squad-features)

## License

MIT
