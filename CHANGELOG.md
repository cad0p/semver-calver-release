# Changelog

All notable changes to this project will be documented in this file.

## [1.1.3]

<!-- USER-EDITABLE SECTION START -->
This release improves the draft changelog PR workflow, fixes several edge cases in changelog generation, and adds OIDC-based npm trusted publishing.

**Highlights:**
- Draft changelog PRs now accumulate commits cleanly on the branch tip without auto-rebase artifacts
- Fixed duplicate section bug when version strings contain regex characters
- Changelog generation properly ignores calver tags and uses `index()` for literal matching
- npm publishing uses OIDC trusted publishing (no explicit tokens required)
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

- Compare against main package.json for heading decision ([#118](https://github.com/cad0p/semver-calver-release/pull/118))

- Validate against main package.json instead of branch name ([#119](https://github.com/cad0p/semver-calver-release/pull/119))

- Only skip draft sections when extracting old changelog body ([#121](https://github.com/cad0p/semver-calver-release/pull/121))

- Use main package.json for draft PR branch name ([#122](https://github.com/cad0p/semver-calver-release/pull/122))

- Preserve user-editable section on version bump, scope extraction to first section ([#126](https://github.com/cad0p/semver-calver-release/pull/126))


### 🚜 Refactor

- Use main package.json for changelog range start ([#120](https://github.com/cad0p/semver-calver-release/pull/120))


### ⚙️ Miscellaneous Tasks

- Test calver release on main ([#125](https://github.com/cad0p/semver-calver-release/pull/125))

- Bump version to 1.1.3


## [1.1.2] - 2026-04-30

<!-- USER-EDITABLE SECTION START -->
This release improves the draft changelog PR workflow, fixes several edge cases in changelog generation, and adds OIDC-based npm trusted publishing.

**Highlights:**
- Draft changelog PRs now accumulate commits cleanly on the branch tip without auto-rebase artifacts
- Fixed duplicate section bug when version strings contain regex characters
- Changelog generation properly ignores calver tags and uses `index()` for literal matching
- npm publishing uses OIDC trusted publishing (no explicit tokens required)
<!-- USER-EDITABLE SECTION END -->

### 🚀 Features

- Auto-rebase release branch on main when behind (#67)
- Conflict-aware auto-rebase for draft PR branches (#71)

### 🐛 Bug Fixes

- Remove harmful auto-rebase that silently overwrites main changes (#70)
- Use cliff.toml with tag_pattern to ignore calver tags in changelog generation (#76)
- Use JSON input for rebase ref update (boolean force) (#79)
- Use actual newlines in default user section, strip header from old body (#82)
- Fetch rebased commit so git show works locally (#85)
- Ensure OIDC trusted publishing by removing explicit auth tokens (#88)
- Remove auto-rebase, just accumulate on branch tip (#89)
- Use OIDC token for npm trusted publishing (#93)
- Use index() for literal string match in awk (regex chars in version) (#97)

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
