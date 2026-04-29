# semver-calver-release

Composite GitHub Actions for **hybrid SemVer + CalVer versioning** and npm publishing.

## Versioning Scheme

```
1.0.0                 → first release
1.0.0-20260429.0      → same-day patch
1.0.0-20260429.1      → another same-day patch
1.1.0                 → next manual minor bump
```

- Starts from a **SemVer base** (`MAJOR.MINOR.PATCH`) read from `package.json`
- If the base version was already released, appends **CalVer suffix** (`-YYYYMMDD.N`)
- Auto-increments `N` for multiple releases on the same day

## Actions

### `validate-version`

Validates `package.json` version format on pull requests.

```yaml
name: Validate Version
on:
  pull_request:
    branches: [main]
jobs:
  check-version:
    runs-on: ubuntu-latest
    steps:
      - uses: cad0p/semver-calver-release/validate-version@v1
```

### `release`

Computes the next hybrid version, creates a git tag, and publishes a GitHub release.

```yaml
name: Auto Release
on:
  push:
    branches: [main]
permissions:
  contents: write
  id-token: write
jobs:
  release:
    runs-on: ubuntu-latest
    outputs:
      version: ${{ steps.release.outputs.version }}
      has_changes: ${{ steps.release.outputs.has_changes }}
    steps:
      - id: release
        uses: cad0p/semver-calver-release/release@v1

  publish:
    needs: release
    if: needs.release.outputs.has_changes == 'true'
    runs-on: ubuntu-latest
    permissions:
      contents: read
      id-token: write
    steps:
      - uses: cad0p/semver-calver-release/npm-publish@v1
        with:
          tag: v${{ needs.release.outputs.version }}
```

**Outputs:**

| Output | Description |
|--------|-------------|
| `version` | Computed release version |
| `has_changes` | `true` if code changes detected since last tag |

### `npm-publish`

Publishes to npm with **smart skip** — if the version already exists on npm, the action exits cleanly instead of failing. Uses `next` dist-tag for prerelease versions (containing `-`).

```yaml
name: Publish to npm
on:
  release:
    types: [published]
jobs:
  publish:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      id-token: write
    steps:
      - uses: cad0p/semver-calver-release/npm-publish@v1
        with:
          tag: ${{ github.event.release.tag_name }}
```

**Inputs:**

| Input | Required | Description |
|-------|----------|-------------|
| `tag` | No | Git tag to publish (defaults to `github.event.release.tag_name`) |

## Self-releasing this action

For the `semver-calver-release` repo itself, use `@main` to avoid the chicken-and-egg problem with `@v1`:

```yaml
jobs:
  release:
    steps:
      - id: release
        uses: cad0p/semver-calver-release/release@main
```

Consumer repos should still pin to `@v1` for stability.

## Full Example

```yaml
name: CI

on:
  pull_request:
    branches: [main]
  push:
    branches: [main]

permissions:
  contents: write
  id-token: write

jobs:
  validate:
    if: github.event_name == 'pull_request'
    runs-on: ubuntu-latest
    steps:
      - uses: cad0p/semver-calver-release/validate-version@v1

  release:
    if: github.event_name == 'push'
    runs-on: ubuntu-latest
    outputs:
      version: ${{ steps.release.outputs.version }}
      has_changes: ${{ steps.release.outputs.has_changes }}
    steps:
      - id: release
        uses: cad0p/semver-calver-release/release@v1

  publish:
    needs: release
    if: github.event_name == 'push' && needs.release.outputs.has_changes == 'true'
    runs-on: ubuntu-latest
    permissions:
      contents: read
      id-token: write
    steps:
      - uses: cad0p/semver-calver-release/npm-publish@v1
        with:
          tag: ${{ needs.release.outputs.tag }}
```

## Pinning

Use `@v1` to track the latest v1.x release. For immutable references, pin to a specific tag like `@v1.0.0`.

## License

MIT
