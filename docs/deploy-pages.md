# deploy-pages

Build a static site and deploy to GitHub Pages (gh-pages branch).

## Inputs

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `build-command` | string | *required* | Build command (e.g. `mdbook build docs`) |
| `output-dir` | string | *required* | Directory with built files |
| `runner` | string | `self-hosted` | Runner label |

Only deploys on `push` and `workflow_dispatch` events (skips on PRs).
