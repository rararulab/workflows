# rust-test

Clippy + documentation + nextest.

## Inputs

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `runner` | string | `arc-runner-set` | Runner label |
| `workspace` | boolean | `false` | Use `--workspace` flag |
| `sccache` | boolean | `false` | Enable sccache via MinIO |
| `sccache-endpoint` | string | `http://10.0.0.167:9000` | S3-compatible endpoint for sccache |
| `sccache-bucket` | string | `sccache` | S3 bucket name for sccache |

## Jobs

- **clippy** — `cargo clippy --all-targets --no-deps -- -D warnings`
- **docs** — `cargo +nightly doc --no-deps --document-private-items`
- **test** — `cargo nextest run`
- **rust-success** — Aggregator gate

When `sccache: true`, jobs connect to the endpoint specified by `sccache-endpoint` (defaults to `http://10.0.0.167:9000`).
