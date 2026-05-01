# Examples

Ready-to-use GitHub Actions workflow setups for `semver-calver-release`.

## [`minimal`](./minimal)

Single workflow: auto-release on every push to `main`.

Best for:
- Solo projects
- Projects that always auto-release and don't need curated changelogs

## [`minimal-with-validation`](./minimal-with-validation)

Two workflows: release + validate package version.

Best for:
- Most projects — the general-purpose setup
- Teams that want PR validation without npm publishing
- Projects with curated changelogs but no npm package

## [`basic-npm-package`](./basic-npm-package)

Full 3-workflow setup: release, validate package version, validate release PR, plus npm publish.

Best for:
- npm packages where version bumps matter
- Teams that want validation gates on release PRs
- Projects that publish to npm with provenance
