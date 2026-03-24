# rust-release-dist

Full cargo-dist release pipeline: plan → build → GitHub Release → optional Homebrew.

## Inputs

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `tag` | string | *required* | Version tag (e.g. `v1.0.0`) |
| `runner` | string | `arc-runner-set` | Runner for plan/global/host jobs |
| `homebrew-tap` | string | `""` | Homebrew tap repo (e.g. `rararulab/homebrew-tap`) |
| `minio-endpoint` | string | `""` | MinIO endpoint for artifact backup |

## Secrets

| Secret | Required | Description |
|--------|----------|-------------|
| `HOMEBREW_TAP_TOKEN` | No | Token to push to homebrew tap |

## Jobs

`plan` → `build-local-artifacts` (matrix) → `build-global-artifacts` → `host` (GitHub Release) → `publish-homebrew-formula` → `announce`
