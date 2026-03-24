# rararulab/workflows

Shared reusable GitHub Actions workflows for the rararulab organization.

## Workflows

| Workflow | Description |
|----------|-------------|
| `rust-lint.yml` | Rust formatting (nightly fmt) + cargo-deny |
| `rust-test.yml` | Clippy + docs + nextest, with optional sccache |
| `rust-release-pr.yml` | Create release PR via release-plz |
| `rust-release-plz.yml` | Publish crate on release PR merge |
| `rust-release-dist.yml` | cargo-dist build + GitHub Release + optional Homebrew |
| `go-ci.yml` | Go lint (golangci-lint, vet) + test + optional build |
| `go-release.yml` | git-cliff version bump + GitHub Release |
| `cleanup-branches.yml` | Delete stale release-plz branches |
| `deploy-pages.yml` | Build & deploy to GitHub Pages |

## Usage Examples

### Standard Rust crate (e.g. kotoba, tenki)

```yaml
# .github/workflows/ci.yml
name: CI
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

concurrency:
  group: ci-${{ github.ref }}
  cancel-in-progress: true

jobs:
  lint:
    uses: rararulab/workflows/.github/workflows/rust-lint.yml@main
  test:
    uses: rararulab/workflows/.github/workflows/rust-test.yml@main
  release-pr:
    needs: [lint, test]
    if: ${{ github.event_name == 'push' && github.ref == 'refs/heads/main' }}
    permissions:
      contents: write
      pull-requests: write
    uses: rararulab/workflows/.github/workflows/rust-release-pr.yml@main
```

```yaml
# .github/workflows/release-plz.yml
name: Release-plz
on:
  pull_request:
    types: [closed]
    branches: [main]

jobs:
  release:
    uses: rararulab/workflows/.github/workflows/rust-release-plz.yml@main
    secrets:
      CARGO_REGISTRY_TOKEN: ${{ secrets.CARGO_REGISTRY_TOKEN }}
```

```yaml
# .github/workflows/cleanup-branches.yml
name: Cleanup stale branches
on:
  pull_request:
    types: [closed]

jobs:
  cleanup:
    uses: rararulab/workflows/.github/workflows/cleanup-branches.yml@main
```

### Rust workspace with sccache + cargo-dist + Homebrew (e.g. rara)

```yaml
# .github/workflows/ci.yml
name: CI
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  lint:
    uses: rararulab/workflows/.github/workflows/rust-lint.yml@main
  test:
    uses: rararulab/workflows/.github/workflows/rust-test.yml@main
    with:
      workspace: true
      sccache: true
  release-pr:
    needs: [lint, test]
    if: ${{ github.event_name == 'push' }}
    permissions:
      contents: write
      pull-requests: write
    uses: rararulab/workflows/.github/workflows/rust-release-pr.yml@main
```

```yaml
# .github/workflows/release-plz.yml (with cargo-dist trigger)
name: Release-plz
on:
  pull_request:
    types: [closed]
    branches: [main]

jobs:
  release:
    uses: rararulab/workflows/.github/workflows/rust-release-plz.yml@main
    # ... extract version, then call rust-release-dist.yml
```

```yaml
# .github/workflows/release.yml (cargo-dist)
name: Release
on:
  workflow_call:
    inputs:
      tag:
        required: true
        type: string

jobs:
  dist:
    uses: rararulab/workflows/.github/workflows/rust-release-dist.yml@main
    with:
      tag: ${{ inputs.tag }}
      homebrew-tap: rararulab/homebrew-tap
      minio-endpoint: http://10.0.0.167:9000
    secrets:
      HOMEBREW_TAP_TOKEN: ${{ secrets.HOMEBREW_TAP_TOKEN }}
```

### Go project (e.g. devkit)

```yaml
# .github/workflows/ci.yml
name: CI
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  ci:
    uses: rararulab/workflows/.github/workflows/go-ci.yml@main
    with:
      build-binary: devkit
```

```yaml
# .github/workflows/release.yml
name: Release
on:
  push:
    branches: [main]

jobs:
  release:
    uses: rararulab/workflows/.github/workflows/go-release.yml@main
```

### GitHub Pages (e.g. rara docs)

```yaml
# .github/workflows/web.yml
name: Web
on:
  push:
    branches: [main]
    paths: [docs/**]
  workflow_dispatch:

jobs:
  deploy:
    uses: rararulab/workflows/.github/workflows/deploy-pages.yml@main
    with:
      build-command: "mdbook build docs"
      output-dir: "docs/book"
```
