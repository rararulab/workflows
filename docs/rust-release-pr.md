# rust-release-pr

Create release PR via release-plz.

## Inputs

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `runner` | string | `arc-runner-set` | Runner label |

## Permissions Required

```yaml
permissions:
  contents: write
  pull-requests: write
```

Only runs for `rararulab` org repos on `main` branch.
