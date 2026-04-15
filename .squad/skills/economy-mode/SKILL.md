---
name: "economy-mode"
description: "Shifts Layer 3 model selection to cost-optimized alternatives when economy mode is active."
domain: "model-selection"
confidence: "low"
source: "manual"
---

# Skill: Economy Mode

## What It Does

Economy mode shifts Layer 3 (Task-Aware Auto-Selection) to lower-cost model alternatives. It does NOT override user-configured models — those always take priority.

## Activation Methods

| Method | How |
|--------|-----|
| Session phrase | "use economy mode", "save costs", "go cheap" |
| Persistent config | `"economyMode": true` in `.squad/config.json` |
| CLI flag | `squad --economy` |

**Deactivation:** "turn off economy mode" or remove `economyMode` from config.json.

## Economy Model Selection Table

| Task Output | Normal Mode | Economy Mode |
|-------------|-------------|--------------|
| Writing code | `claude-sonnet-4.5` | `gpt-4.1` or `gpt-5-mini` |
| Docs, planning, triage | `claude-haiku-4.5` | `gpt-4.1` or `gpt-5-mini` |
| Architecture, security audits | `claude-opus-4.5` | `claude-sonnet-4.5` |
| Scribe / mechanical ops | `claude-haiku-4.5` | `gpt-4.1` |

## Config Examples

### Economy mode ON:
```json
{
  "version": 1,
  "defaultModel": "claude-sonnet-4.6",
  "economyMode": true
}
```

### Economy mode OFF (default):
```json
{
  "version": 1,
  "defaultModel": "claude-sonnet-4.6",
  "economyMode": false
}
```

### With agent-level overrides (Layer 0 always wins):
```json
{
  "version": 1,
  "defaultModel": "claude-sonnet-4.6",
  "economyMode": true,
  "agentModelOverrides": {
    "security-lead": "claude-opus-4.5"
  }
}
```

## Anti-Patterns

- **Don't override Layer 0 in economy mode.** If the user set a specific model, respect it.
- **Don't silently apply economy mode.** Always acknowledge activation.
- **Don't bump premium tasks down too far.** Security reviews go from opus→sonnet, never to fast/cheap.
