# rararulab/workflows

Shared reusable GitHub Actions workflows.

## Workflows

| Workflow | Docs | Description |
|----------|------|-------------|
| [`rust-lint`](.github/workflows/rust-lint.yml) | [docs](docs/rust-lint.md) | fmt + cargo-deny |
| [`rust-test`](.github/workflows/rust-test.yml) | [docs](docs/rust-test.md) | clippy + doc + nextest |
| [`rust-release-pr`](.github/workflows/rust-release-pr.yml) | [docs](docs/rust-release-pr.md) | release-plz PR |
| [`rust-release-plz`](.github/workflows/rust-release-plz.yml) | [docs](docs/rust-release-plz.md) | release-plz publish |
| [`rust-release-dist`](.github/workflows/rust-release-dist.yml) | [docs](docs/rust-release-dist.md) | cargo-dist + Homebrew |
| [`go-ci`](.github/workflows/go-ci.yml) | [docs](docs/go-ci.md) | lint + test + build |
| [`go-release`](.github/workflows/go-release.yml) | [docs](docs/go-release.md) | git-cliff + GitHub Release |
| [`cleanup-branches`](.github/workflows/cleanup-branches.yml) | [docs](docs/cleanup-branches.md) | Delete stale branches |
| [`deploy-pages`](.github/workflows/deploy-pages.yml) | [docs](docs/deploy-pages.md) | GitHub Pages deploy |

## Quick Start

Copy a template from [`templates/`](templates/) into your repo's `.github/workflows/`.

- **Rust crate** → [`templates/rust-crate/`](templates/rust-crate/)
- **Go CLI** → [`templates/go-cli/`](templates/go-cli/)
