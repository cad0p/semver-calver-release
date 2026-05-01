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

## Release Branch Workflow

The action maintains a **draft release PR** on a branch named after the **last released** base version (e.g. `release/v1.1.2`). This branch accumulates all changes since that release:

| Event | What happens |
|-------|-------------|
| **Push to `main`** | Auto calver release + updates draft PR with new commits |
| **Push to `release/v1.1.2`** | Updates draft PR only (no tag/release) — for curating the next base release |
| **Merge draft PR to `main`** | Triggers base release with curated CHANGELOG |

### Draft headings include the current date

Draft PR sections use `[calver-released]` when still accumulating, or `[1.1.3] - YYYY-MM-DD` when the version is bumped. The date is the current UTC date at the time of the last push to the branch:

```markdown
## [1.1.3] - 2026-04-30      ← date added automatically when version differs from main
## [calver-released]         ← no date while still accumulating
```

The date refreshes on each push so it stays current. The validation check ensures a dated heading is present before merge.

## Usage

See [`/examples`](./examples) for ready-to-use workflow setups:

| Example | What's included | Best for |
|---------|----------------|----------|
| [`minimal`](./examples/minimal) | Single release workflow on push to `main` | Projects that always auto-release |
| [`minimal-with-validation`](./examples/minimal-with-validation) | Release + validation workflows | **Most projects** — the general-purpose setup. Also used by this repo itself |
| [`basic-npm-package`](./examples/basic-npm-package) | Release + npm publish + validation workflows | npm packages with curated changelogs |

Copy the workflows from the example that fits your project and commit them to `.github/workflows/`.

## How it works

### Calver releases (automatic)

Every push to `main` that changes code triggers:
1. Compute next version (e.g. `1.0.0-20260429.0`)
2. Generate release notes with [git-cliff](https://git-cliff.org)
3. Tag + **prerelease** on GitHub (calver builds are marked as prerelease)
4. Publish to npm (with `next` dist-tag)
5. Update draft changelog PR branch with accumulated changes

> **Note:** Floating tags (`v1`, `v1.x`) are **not** updated for calver releases. Consumers pinning to `@v1` always get the last stable base release.

### Base releases (manual, curated)

When you want to bump the base version (e.g. `1.1.2` → `1.1.3`):

1. **Find the draft PR** on `release/v1.1.2` — it contains accumulated changelogs since `v1.1.2` was released
2. **Edit CHANGELOG.md** on that branch to add your preamble/notes between the `<!-- USER-EDITABLE SECTION -->` markers
3. **Bump `package.json`** version to `1.1.3`
4. **Merge the PR** — the `validate-release-pr` check ensures the version is bumped, the date is present, and no unexpected files are present
5. The merge triggers `v1.1.3` **base release** using your curated CHANGELOG.md — floating tags (`v1`, `v1.x`) are updated to this release


### Draft changelog PRs

After the first calver release following a base release, a branch like `release/v1.1.2` is maintained with accumulated changelogs.

**How it works:**
- The draft heading uses the current `package.json` version (e.g. `## [1.1.3]`) when bumped, or `[calver-released]` when still accumulating
- Historical sections (`[1.1.2]`, `[1.1.0]`, etc.) come from `main` — the branch is rebuilt from `origin/main` on each update
- User-editable sections are preserved across heading changes. A fresh empty section only appears when the branch is first created from main

You can:
- View it to see all changes since the base release
- Edit it to curate the changelog before a base release
- Bump `package.json` — the PR title auto-updates to match
- Merge it when ready to ship the next base version

**Validation not appearing?** Bot commits (like `docs(changelog): ...`) do not trigger GitHub Actions workflows. If the `validate` status check is stuck on "Expected", click **"Update branch"** on the PR to create a merge commit that triggers validation.

**Note:** Auto-creating PRs requires enabling "Allow GitHub Actions to create and approve pull requests" in your repo settings (Settings → Actions → General). Without this, the branch is still maintained automatically — you'll just need to create the PR manually.

## Customizing changelog format

The release action uses [git-cliff](https://git-cliff.org) to generate changelogs. It looks for a `cliff.toml` in your repo root and falls back to a [sensible default](release/cliff.toml) shipped with the action.

To customize:

1. Start from the [default config](release/cliff.toml) or run `git-cliff --init` to generate one
2. Commit `cliff.toml` to your repo root
3. The action will use your config instead of the default

Your custom config is applied **before** PR link injection, so you don't need to include the postprocessor for markdown links — the action adds those automatically.

## Actions

### `validate-package-version`

Prevents accidental `package.json` version changes on feature branches and validates format on release branches.

```yaml
- uses: cad0p/semver-calver-release/validate-package-version@v1
```

**Behavior:**
- **Feature branches** (`feature/*`, `fix/*`, etc.): Errors if `package.json` version differs from `main`
- **Release branches** (`release/v*`): Validates format only (version bump is expected)

**Inputs:**

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `base-branch` | No | `main` | Branch to compare package.json version against |

```yaml
- uses: cad0p/semver-calver-release/validate-package-version@v1
  with:
    base-branch: develop
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
