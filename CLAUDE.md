# CLAUDE.md — workflows

## Communication
- 用中文与用户交流

## Purpose

Shared reusable GitHub Actions workflows for the rararulab organization. Other repos call these via:
```yaml
uses: rararulab/workflows/.github/workflows/{name}.yml@main
```

## Structure

```
.github/workflows/   # Reusable workflows (workflow_call trigger)
docs/                 # Per-workflow documentation
templates/            # Example caller workflows for consumers to copy
```

## Naming Conventions

- `rust-*.yml` — Rust workflows
- `go-*.yml` — Go workflows
- No prefix — language-agnostic workflows

## Key Inputs Pattern

All workflows accept `runner` input (default: `arc-runner-set` for Rust, `ubuntu-latest` for Go). Feature toggles are booleans (e.g. `sccache`, `workspace`, `cargo-deny`).

## Guardrails

- All workflows use `workflow_call` trigger — they are never standalone
- Pin action versions with full SHA or vN tag
- Never hardcode secrets — always pass via `secrets` in workflow_call
- Test workflow changes against a real repo before merging
