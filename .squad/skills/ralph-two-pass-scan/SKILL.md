# Skill: Ralph — Two-Pass Issue Scanning
**Confidence:** high
**Domain:** work-monitoring
**Last validated:** 2026-04-20

## Context
Cuts GitHub API calls from N+1 to ~7 per round (~72% reduction) by separating list scanning from full hydration.

## Pattern

### Pass 1 — Lightweight Scan

```
gh issue list --state open --json number,title,labels,assignees --limit 100
```

**Skip hydration if ANY of these match:**

| Condition | Skip reason |
|-----------|-------------|
| `assignees` non-empty AND no `status:needs-review` | Already owned |
| Labels contain `status:blocked` or `status:waiting-external` | Externally gated |
| Labels contain `status:done` or `status:postponed` | Closed loop |
| Title matches stale/noisy pattern (`[chore]`, `[auto]`) | Low-signal |

### Pass 2 — Selective Hydration

For each issue surviving Pass 1:

```
gh issue view <number> --json number,title,body,labels,assignees,comments,state
```

Then apply normal Ralph triage logic. Rule of thumb: hydrate ≤ 30% of scanned list. If more than 30% survive Pass 1, tighten filter rules.

## Enabling Two-Pass Scanning

Two-pass scanning is built into Ralph's default behavior. To verify it's active:

```bash
# Check Ralph's triage output — you'll see Pass 1/Pass 2 indicators
squad ralph watch --duration 30s --verbose
```

To adjust filter rules, edit the skip conditions in this skill file and Ralph will pick them up on the next scan cycle.
