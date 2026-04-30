# Changelog

All notable changes to this project will be documented in this file.

## [1.1.3] - 2026-04-30

<!-- USER-EDITABLE SECTION START -->
<!-- Add your curated release notes here. -->
<!-- USER-EDITABLE SECTION END -->


### 🚀 Features

- Add PR links in changelog via cliff.toml postprocessor ([#102](https://github.com/cad0p/semver-calver-release/pull/102))

- Ship default cliff.toml with action, allow consumer override ([#104](https://github.com/cad0p/semver-calver-release/pull/104))


### 🐛 Bug Fixes

- Use native git-cliff commit_preprocessors for PR links, remove sed post-processing ([#105](https://github.com/cad0p/semver-calver-release/pull/105))

- Move commit_preprocessors from [changelog] to [git] section ([#106](https://github.com/cad0p/semver-calver-release/pull/106))

- Use previous base release tag for changelog range ([#107](https://github.com/cad0p/semver-calver-release/pull/107))

- Use [unreleased] heading for draft PR, keep finalized sections below ([#109](https://github.com/cad0p/semver-calver-release/pull/109))

- Use [unreleased] heading for draft PR, keep finalized sections below ([#109](https://github.com/cad0p/semver-calver-release/pull/109)) ([#110](https://github.com/cad0p/semver-calver-release/pull/110))

- Validate CHANGELOG heading matches package.json version ([#111](https://github.com/cad0p/semver-calver-release/pull/111))

- Always update single draft section at top, never duplicate ([#112](https://github.com/cad0p/semver-calver-release/pull/112))

- Auto-manage draft heading, start fresh on base bump, remove heading validation ([#113](https://github.com/cad0p/semver-calver-release/pull/113))

- Run release action on release/* branches, skip tag/release there ([#114](https://github.com/cad0p/semver-calver-release/pull/114))

- Always update draft PR on release branches regardless of calver/base ([#115](https://github.com/cad0p/semver-calver-release/pull/115))

- Use previous base tag for changelog range ([#116](https://github.com/cad0p/semver-calver-release/pull/116))


## [1.1.0] - 2026-04-30

### 🚀 Features

- Auto-update floating v1 tag on release (#3)
- Add floating v1.0 tag for major.minor pinning (#6)
- Auto-manage CHANGELOG.md with conventional-changelog (#8)
- Use git-cliff with draft changelog PR (#14)

### 🐛 Bug Fixes

- Configure git identity for annotated tag (#4)
- Use lightweight tag instead of annotated tag (#5)
- Replace deprecated conventional-changelog-cli with shell script (#9)
- Tag triggering commit, remove redundant release title (#11)
- Use generate-notes, tag before changelog commit (#13)
- Git-cliff uses positional range, not --from/--to (#15)
- Graceful PR creation, add pull-requests: write permission (#16)
- Force checkout to handle untracked CHANGELOG.md (#17)
- Clearer error when GitHub blocks Actions from creating PRs (#20)
- Unified changelog on draft PR, always reset branch from main (#23)
- Use GitHub API for signed commits on draft PR branch (#24)
- Use JSON input for GitHub API tree/commit creation (#25)
- Use JSON input for PATCH ref update (boolean force) (#26)
- Draft PR, accumulate commits, preserve user-editable section (#27)
- Use heredoc for multiline string in YAML (#28)
- Escape newlines in default user section (#29)
- Conventional commit style for PR title and changelog commits (#32)
- Exclude floating tags from last_tag detection (#34)
- PR body newlines, shorter commit messages (#38)
- Use quoted string with actual newlines for PR body (#40)
- Use $'...' bash syntax for PR body newlines (#42)
- Use printf for PR body newlines (#44)
- Remove literal backslash escapes from PR body (#47)

### 📚 Documentation

- Clean up README with proper usage example (#7)
- Update README with git-cliff and draft PR workflow (#18)
- Retroactively fix v1.1.0 changelog heading (#59)
