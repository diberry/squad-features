# Skill: nap

> Context hygiene — compress, prune, archive .squad/ state

## What It Does

Reclaims context window budget by compressing agent histories, pruning old logs,
archiving stale decisions, and cleaning orphaned inbox files.

## When To Use

- Before heavy fan-out work (many agents will spawn)
- When history.md files exceed 15KB
- When .squad/ total size exceeds 1MB
- After long-running sessions or sprints

## Invocation

| Command | What it does |
|---------|-------------|
| `squad nap` | Light cleanup: compress histories, prune old logs |
| `squad nap --deep` | Full cleanup: also archives stale decisions to `decisions-archive.md` |
| `squad nap --dry-run` | Preview what would be cleaned without changing anything |

## What `--deep` Archives

Decisions in `.squad/decisions.md` older than 30 days are moved to `.squad/decisions-archive.md`. The archive is append-only. Active decisions stay in `decisions.md`.

### Before `nap --deep`:
- `decisions.md`: 8 active decisions (some from March)
- `decisions-archive.md`: 3 archived decisions

### After `nap --deep`:
- `decisions.md`: 5 active decisions (only recent ones remain)
- `decisions-archive.md`: 6 archived decisions (old ones moved here)

## Confidence

medium — Confirmed by team vote and initial implementation
