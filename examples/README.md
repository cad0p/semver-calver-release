# Examples

Ready-to-use GitHub Actions workflow setups for `semver-calver-release`.

## [`minimal`](./minimal)

Single workflow: auto-release on every push to `main`.

Best for:
- Solo projects
- Projects that always auto-release and don't need curated changelogs

## [`basic-npm-package`](./basic-npm-package)

Full 3-workflow setup: release, validate package version, validate release PR.

Best for:
- Team projects with curated changelogs
- npm packages where version bumps matter
- Teams that want validation gates on release PRs
