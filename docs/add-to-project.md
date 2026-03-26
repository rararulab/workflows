# add-to-project

Automatically add new issues and PRs to a GitHub Projects V2 board.

## Inputs

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `runner` | string | `arc-runner-set` | Runner label |
| `project-url` | string | *required* | GitHub Projects V2 URL |

## Secrets

| Secret | Description |
|--------|-------------|
| `ADD_TO_PROJECT_TOKEN` | PAT with `project` write scope |

## Caller Trigger

```yaml
on:
  issues:
    types: [opened]
  pull_request:
    types: [opened]
```
