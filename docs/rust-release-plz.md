# rust-release-plz

Publish crates when a release PR is merged.

## Inputs

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `runner` | string | `arc-runner-set` | Runner label |

## Secrets

| Secret | Required | Description |
|--------|----------|-------------|
| `CARGO_REGISTRY_TOKEN` | No | Token for crates.io publishing |

## Trigger

Caller must set:
```yaml
on:
  pull_request:
    types: [closed]
    branches: [main]
```

Only fires when PR has `release` label and is merged.
