# workflows — Agent Guidelines

## Purpose
Shared reusable GitHub Actions workflows for the rararulab organization. Other repos call these via `uses: rararulab/workflows/.github/workflows/{name}.yml@main`.

## Architecture
- `.github/workflows/` — Reusable workflows (all use `workflow_call` trigger)
- `docs/` — Per-workflow documentation (one doc per workflow)
- `templates/` — Example caller workflows for consumer repos to copy

## Critical Invariants
- All workflows MUST use `workflow_call` trigger — they are never standalone
- All workflows MUST expose a `runner` input for runner configurability (default varies by language: `arc-runner-set` for Rust, `ubuntu-latest` for Go/generic)
- Every workflow MUST have a corresponding doc in `docs/`
- Pin action versions with vN tags at minimum

## Naming Conventions
- `rust-*.yml` — Rust workflows
- `go-*.yml` — Go workflows
- No prefix — Language-agnostic workflows (cleanup-branches, add-to-project, deploy-pages)

## What NOT To Do
- Do NOT hardcode secrets or credentials — pass via `secrets` in workflow_call
- Do NOT hardcode runner labels — always use the `runner` input
- Do NOT create standalone workflows — everything here is reusable only
- Do NOT forget to create a doc + template when adding a new workflow

## Dependencies
- Consumer repos call these via `uses:` directive
- Secrets are passed from caller workflows, never stored here
- Some workflows reference org infrastructure (MinIO for sccache, ARC runners)
