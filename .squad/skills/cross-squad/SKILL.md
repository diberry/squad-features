---
name: "cross-squad"
description: "Coordinating work across multiple Squad instances"
domain: "orchestration"
confidence: "medium"
source: "manual"
tools:
  - name: "squad-discover"
    description: "List known squads and their capabilities"
    when: "When you need to find which squad can handle a task"
  - name: "squad-delegate"
    description: "Create work in another squad's repository"
    when: "When a task belongs to another squad's domain"
---

# Skill: Cross-Squad Orchestration

## Context

When an organization runs multiple Squad instances (e.g., platform-squad, frontend-squad, data-squad), those squads need to discover each other, share context, and hand off work across repository boundaries.

## Discovery via Manifest

Each squad publishes a `.squad/manifest.json`:

```json
{
  "name": "platform-squad",
  "version": "1.0.0",
  "description": "Platform infrastructure team",
  "capabilities": ["kubernetes", "helm", "monitoring", "ci-cd"],
  "contact": {
    "repo": "org/platform",
    "labels": ["squad:platform"]
  },
  "accepts": ["issues", "prs"],
  "skills": ["helm-developer", "operator-developer", "pipeline-engineer"]
}
```

## Commands

```bash
# Discover available squads
squad discover

# Output:
#   platform-squad  →  org/platform  (kubernetes, helm, monitoring)
#   frontend-squad  →  org/frontend  (react, nextjs, storybook)
#   data-squad      →  org/data      (spark, airflow, dbt)

# Delegate a task to another squad
squad delegate platform-squad "Add Prometheus metrics endpoint"
```

## Work Handoff Protocol

1. **Check manifest** — verify the target squad accepts the work type
2. **Create issue** — `[cross-squad]` prefixed title in target repo
3. **Track** — record the cross-squad issue in orchestration log
4. **Poll** — periodically check if delegated work is done

## Anti-Patterns

- **Direct file writes across repos** — use issues/PRs as the communication protocol
- **Tight coupling** — use the manifest as the public API, not internal structure
- **Unbounded delegation** — always include acceptance criteria and a timeout
