# rararulab/workflows

Shared reusable GitHub Actions workflows.

## Workflows

| Workflow | Description | Key Inputs |
|----------|-------------|------------|
| `rust-lint.yml` | fmt + cargo-deny | `runner`, `cargo-deny` |
| `rust-test.yml` | clippy + doc + nextest | `runner`, `workspace`, `sccache` |
| `rust-release-pr.yml` | release-plz PR creation | `runner` |
| `rust-release-plz.yml` | release-plz publish | `runner`, `CARGO_REGISTRY_TOKEN` |
| `rust-release-dist.yml` | cargo-dist + GitHub Release + Homebrew | `tag`, `homebrew-tap`, `minio-endpoint` |
| `go-ci.yml` | golangci-lint + test + build | `go-version`, `build-binary`, `test-matrix` |
| `go-release.yml` | git-cliff + GitHub Release | `version-file`, `cliff-config` |
| `cleanup-branches.yml` | Delete stale release-plz branches | `branch-prefix` |
| `deploy-pages.yml` | Build & deploy GitHub Pages | `build-command`, `output-dir` |

## Usage

```yaml
jobs:
  lint:
    uses: rararulab/workflows/.github/workflows/rust-lint.yml@main
  test:
    uses: rararulab/workflows/.github/workflows/rust-test.yml@main
    with:
      workspace: true
      sccache: true
```
