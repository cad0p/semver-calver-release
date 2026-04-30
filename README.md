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

## Usage

Add a single workflow file to your repo:

```yaml
# .github/workflows/ci.yml
name: CI

on:
  pull_request:
    branches: [main]
  push:
    branches: [main]

permissions:
  contents: write
  pull-requests: write
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
          tag: v${{ needs.release.outputs.version }}
```

That's it. No other workflow files needed.

## How it works

### Calver releases (automatic)

Every push to `main` that changes code triggers:
1. Compute next version (e.g. `1.0.0-20260429.0`)
2. Generate release notes with [git-cliff](https://git-cliff.org)
3. Tag + GitHub release
4. Publish to npm (with `next` dist-tag for prereleases)
5. Update floating tags (`v1`, `v1.0`)
6. Update draft changelog PR branch with accumulated changes

### Base releases (manual, curated)

When you want to bump the base version (e.g. `1.0.0` → `1.1.0`):

1. **Find the draft PR** (e.g. `release/v1.0.0`) — it contains accumulated changelogs since the last base release
2. **Edit CHANGELOG.md** on that branch to add your preamble/notes between the `<!-- USER-EDITABLE SECTION -->` markers
3. **Bump `package.json`** version to `1.1.0`
4. **Merge the PR** — the `validate-release-pr` check ensures the version is bumped before merging
5. The merge triggers `v1.1.0` release using your curated CHANGELOG.md

### Draft changelog PRs

After the first calver release following a base release, a branch like `release/v1.0.0` is maintained with accumulated changelogs. The changelog heading uses the current `package.json` version (e.g. `## [1.1.0] - 2026-04-30`) instead of `[unreleased]`.

You can:
- View it to see all changes since the base release
- Edit it to curate the changelog before a base release
- Bump `package.json` — the PR title auto-updates to match
- Merge it when ready to ship the next base version

**Note:** Auto-creating PRs requires enabling "Allow GitHub Actions to create and approve pull requests" in your repo settings (Settings → Actions → General). Without this, the branch is still maintained automatically — you'll just need to create the PR manually.

## Customizing changelog format

The release action uses [git-cliff](https://git-cliff.org) to generate changelogs. It looks for a `cliff.toml` in your repo root and falls back to a sensible default shipped with the action.

To customize:

1. Run `git-cliff --init` in your repo to generate a starting config
2. Commit `cliff.toml` to your repo root
3. The action will use your config instead of the default

Your custom config is applied **before** PR link injection, so you don't need to include the postprocessor for markdown links — the action adds those automatically.

## Actions

### `validate-version`

Validates `package.json` version format on pull requests.

```yaml
- uses: cad0p/semver-calver-release/validate-version@v1
```

### `release`

Computes the next hybrid version, creates a git tag, publishes a GitHub release with git-cliff notes, and maintains draft changelog PRs.

```yaml
- id: release
  uses: cad0p/semver-calver-release/release@v1
```

**Outputs:**

| Output | Description |
|--------|-------------|
| `version` | Computed release version (e.g. `1.0.0-20260429.0`) |
| `has_changes` | `true` if code changes detected since last tag |

**Permissions needed:**

| Permission | Why |
|------------|-----|
| `contents: write` | Create tags and releases |
| `pull-requests: write` | Create draft changelog PRs (optional, falls back gracefully) |

### `npm-publish`

Publishes to npm with **smart skip** — if the version already exists, the action exits cleanly instead of failing. Uses `next` dist-tag for prerelease versions (containing `-`).

```yaml
- uses: cad0p/semver-calver-release/npm-publish@v1
  with:
    tag: v${{ needs.release.outputs.version }}
```

| Input | Required | Description |
|-------|----------|-------------|
| `tag` | No | Git tag to publish (defaults to `github.event.release.tag_name`) |

### `validate-release-pr`

Validates that `package.json` version is bumped before merging a release PR. Auto-updates the PR title to match the bumped version.

```yaml
# .github/workflows/validate-release-pr.yml
name: Validate Release PR

on:
  pull_request:
    branches: [main]

permissions:
  contents: read
  pull-requests: write

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: cad0p/semver-calver-release/validate-release-pr@v1
```

To **block merges** until validation passes, add `validate` as a required status check in your branch protection rules.

## Pinning

| Ref | Meaning |
|-----|---------|
| `@v1` | Latest v1.x.x — recommended for CI |
| `@v1.1` | Latest v1.1.x — minor version locked |
| `@v1.1.0` or `@v1.1.0-20260429.0` | Exact release — immutable |

## Self-releasing this action

For the `semver-calver-release` repo itself, use `@main` to avoid the chicken-and-egg problem:

```yaml
- uses: cad0p/semver-calver-release/release@main
```

Consumer repos should always pin to `@v1`.

## License

MIT
