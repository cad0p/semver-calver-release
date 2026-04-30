# Examples

Ready-to-use GitHub Actions workflow setups for `semver-calver-release`.

## [`minimal`](./minimal)

Single workflow: auto-release on every push to `main`.

Best for:
- Solo projects
- Teams that always auto-release (no curated changelogs)
- CI-only repos without npm publishing

## [`basic-npm-package`](./basic-npm-package)

Full 3-workflow setup: release, validate package version, validate release PR.

Best for:
- Team projects with curated changelogs
- npm packages where version bumps matter
- Teams that want validation gates on release PRs
