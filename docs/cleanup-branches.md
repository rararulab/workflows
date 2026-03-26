# cleanup-branches

Delete branches from closed (not merged) PRs matching a prefix.

## Inputs

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `runner` | string | `ubuntu-latest` | Runner label |
| `branch-prefix` | string | `release-plz-` | Branch prefix to match |

## Caller Trigger

```yaml
on:
  pull_request:
    types: [closed]
```
