# rust-lint

Rust formatting check + cargo-deny.

## Inputs

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `runner` | string | `arc-runner-set` | Runner label |
| `cargo-deny` | boolean | `true` | Run cargo-deny checks |

## Jobs

- **rust-format** — `cargo +nightly fmt --all -- --check`
- **cargo-deny** — `cargo deny check` (advisories, licenses, bans)
- **lint-success** — Aggregator gate
