---
name: tiered-memory
description: Three-tier agent memory model (hot/cold/wiki) for 20-55% context reduction per spawn
domain: memory-management, performance
confidence: high
source: earned (production measurements, 34-74KB baseline payloads)
---

# Skill: Tiered Agent Memory

## Overview

Squad agents load their full context history on every spawn, resulting in 34–74KB payloads per agent. The Tiered Memory skill introduces a three-tier model that cuts this bloat by 20–55%.

## Memory Tiers

### 🔥 Hot Tier — Current Session Context
- **Size target:** ~2–4KB
- **Load policy:** Always loaded. Every spawn includes hot memory.
- **Contents:** Current task, active decisions, immediate blockers, last 3–5 actions.
- **Lifetime:** Current session only. Scribe promotes relevant parts to Cold.

### ❄️ Cold Tier — Summarized Cross-Session History
- **Size target:** ~8–12KB
- **Load policy:** Load on demand (`--include-cold`).
- **Contents:** Summarized past sessions, cross-session decisions, recurring patterns.
- **Lifetime:** 30 days rolling window. After 30 days, Scribe promotes to Wiki.

### 📚 Wiki Tier — Durable Structured Knowledge
- **Size target:** variable
- **Load policy:** Load on demand (`--include-wiki`).
- **Contents:** Architecture decisions, agent charters, routing rules, API contracts.
- **Lifetime:** Permanent until explicitly deprecated.

## When to Load Each Tier

| Situation | Hot | Cold | Wiki |
|-----------|-----|------|------|
| New task, no prior context needed | ✅ | ❌ | ❌ |
| Resuming interrupted work | ✅ | ✅ | ❌ |
| Debugging a recurring issue | ✅ | ✅ | ❌ |
| Implementing against a spec/ADR | ✅ | ❌ | ✅ |
| Post-incident review | ✅ | ✅ | ✅ |

## File Locations

```
.squad/memory/
├── hot/
│   ├── lead.md         # Current session context for Lead agent
│   └── scribe.md       # Current session context for Scribe
├── cold/
│   ├── lead.md         # 30-day summarized history
│   └── scribe.md
└── wiki/
    ├── architecture.md  # Durable reference docs
    └── api-contracts.md
```
