# Skill: Personal Squad

## What is a Personal Squad?

A personal squad is a user-level collection of AI agents that travel with you across projects. Unlike project agents (defined in `.squad/`), personal agents live in your global config directory and are automatically discovered.

## Directory Structure

```
~/.config/squad/personal-squad/    # Linux/macOS
%APPDATA%/squad/personal-squad/    # Windows
├── agents/
│   ├── {agent-name}/
│   │   ├── charter.md
│   │   └── history.md
│   └── ...
└── config.json
```

## Commands

| Command | What it does |
|---------|-------------|
| `squad personal init` | Bootstrap a personal squad directory |
| `squad personal list` | List your personal agents |
| `squad personal add {name} --role {role}` | Add a personal agent |
| `squad personal remove {name}` | Remove a personal agent |
| `squad cast` | Show session cast (project + personal) |

## Ghost Protocol

Personal agents operate under Ghost Protocol:
- They **advise** but don't directly modify project files
- Suggestions are executed by project agents
- They're transparent about their personal agent origin
- Project agents take precedence on conflicts

## Kill Switch

Set `SQUAD_NO_PERSONAL=1` to disable personal agent discovery.

## Environment Variables

| Variable | Purpose |
|----------|---------|
| `SQUAD_NO_PERSONAL` | Disable personal squad discovery |
| `SQUAD_PERSONAL_DIR` | Override the default personal squad directory |
