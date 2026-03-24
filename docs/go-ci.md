# go-ci

Go lint + test + optional binary build.

## Inputs

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `go-version` | string | `1.26` | Go version |
| `runner` | string | `ubuntu-latest` | Runner for lint job |
| `build-binary` | string | `""` | Binary name (empty = skip build) |
| `build-path` | string | `.` | Go build path |
| `golangci-config` | string | `.golangci.yml` | golangci-lint config path |
| `test-matrix` | string | `["ubuntu-latest", "macos-latest"]` | OS matrix for test/build |

## Jobs

- **lint** — go mod tidy check, golangci-lint, go vet
- **test** — `go test -v -race -coverprofile=coverage.out ./...` (matrix)
- **build** — binary build + upload artifact (only if `build-binary` set)
