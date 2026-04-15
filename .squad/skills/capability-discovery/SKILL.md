# Skill: Machine Capability Discovery

## What It Does

Declares what each machine can do so Ralph automatically routes work to the right environment. Issues tagged with `needs:*` labels are only processed on machines with matching capabilities.

## Setup

### 1. Create a Capabilities Manifest

Create `~/.squad/machine-capabilities.json` (user-wide) or `.squad/machine-capabilities.json` (project-local):

```json
{
  "machine": "MY-LAPTOP",
  "capabilities": ["browser", "personal-gh", "docker", "azure-cli"],
  "missing": ["gpu", "azure-speech", "emu-gh"],
  "lastUpdated": "2026-04-20T10:00:00Z"
}
```

### 2. Label Issues with Requirements

| Label | Meaning |
|-------|---------|
| `needs:browser` | Requires Playwright / browser automation |
| `needs:gpu` | Requires NVIDIA GPU |
| `needs:personal-gh` | Requires personal GitHub account |
| `needs:docker` | Requires Docker daemon |
| `needs:azure-cli` | Requires authenticated Azure CLI |

Custom capabilities work too — any `needs:X` label maps to a `capabilities` entry.

### 3. Ralph Auto-Routes

```
⏭️ Skipping #42 "Train ML model" — missing: gpu
✓ Triaged #43 "Fix CSS layout" → Picard (routing-rule)
```

## Kubernetes Integration

On Kubernetes, machine capabilities map to node labels:

```yaml
spec:
  nodeSelector:
    node.squad.dev/gpu: "true"
    node.squad.dev/browser: "true"
```
