# go-release

Automated release via git-cliff: version bump PR + GitHub Release on merge.

## Inputs

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `version-file` | string | `version.go` | File containing version constant |
| `version-pattern` | string | `s/^const Version = "\(.*\)"/\1/p` | sed pattern to extract version |
| `cliff-config` | string | `cliff.toml` | git-cliff config path |
| `runner` | string | `ubuntu-latest` | Runner label |

## Jobs

- **release-pr** — Detects bump via git-cliff, updates version file + CHANGELOG, creates PR
- **publish-release** — On `chore(release):` commit, creates git tag + GitHub Release
