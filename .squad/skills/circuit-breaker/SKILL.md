# Skill: Circuit Breaker — Model Rate Limit Fallback

## What It Does

When the preferred model hits rate limits, Ralph automatically degrades to free-tier models, then self-heals. Classic circuit breaker pattern (Hystrix / Polly / Resilience4j) applied to model selection.

## Circuit Breaker States

```
┌─────────┐   rate limit error    ┌──────────┐
│ CLOSED  │ ───────────────────►  │   OPEN   │
│ (normal)│                       │(fallback)│
└────┬────┘   ◄──────────────── └────┬─────┘
     │        2 consecutive          │
     │        successes              │ cooldown expires
     │                               ▼
     │                          ┌──────────┐
     └───── success ◄────────  │HALF-OPEN │
             (close)            │ (testing) │
                                └──────────┘
```

## State File

Located at `.squad/ralph-circuit-breaker.json`:

```json
{
  "state": "closed",
  "preferredModel": "claude-sonnet-4.6",
  "fallbackChain": ["gpt-5.4-mini", "gpt-5-mini", "gpt-4.1"],
  "currentFallbackIndex": 0,
  "cooldownMinutes": 10,
  "openedAt": null,
  "halfOpenSuccesses": 0,
  "consecutiveFailures": 0,
  "metrics": {
    "totalFallbacks": 0,
    "totalRecoveries": 0,
    "lastFallbackAt": null,
    "lastRecoveryAt": null
  }
}
```

## Configuration

| Field | Default | Description |
|-------|---------|-------------|
| `preferredModel` | `claude-sonnet-4.6` | Model when circuit is closed |
| `fallbackChain` | `["gpt-5.4-mini", "gpt-5-mini", "gpt-4.1"]` | Ordered fallback models (all free-tier) |
| `cooldownMinutes` | `10` | Wait time before testing recovery |

## Checking Status

```powershell
$cb = Get-Content .squad/ralph-circuit-breaker.json | ConvertFrom-Json
Write-Host "State: $($cb.state) | Fallbacks: $($cb.metrics.totalFallbacks) | Recoveries: $($cb.metrics.totalRecoveries)"
```
