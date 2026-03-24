# rust-test

Clippy + documentation + nextest.

## Inputs

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `runner` | string | `arc-runner-set` | Runner label |
| `workspace` | boolean | `false` | Use `--workspace` flag |
| `sccache` | boolean | `false` | Enable sccache via MinIO |

## Jobs

- **clippy** — `cargo clippy --all-targets --no-deps -- -D warnings`
- **docs** — `cargo +nightly doc --no-deps --document-private-items`
- **test** — `cargo nextest run`
- **rust-success** — Aggregator gate

When `sccache: true`, jobs connect to MinIO at `http://10.0.0.167:9000`.
