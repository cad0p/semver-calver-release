# Changelog

All notable changes to this project will be documented in this file.

## [1.1.2] - 2026-04-30

<!-- USER-EDITABLE SECTION START -->
<!-- Add your curated release notes here. This section is preserved across calver releases. -->
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

### ⚙️ Miscellaneous Tasks

- Trigger release to test auto-rebase (#69)
- Modify CHANGELOG.md to test conflict detection (#72)
- Trigger release after CHANGELOG.md conflict (#73)
- Remove conflict test files (#74)
- Clean up CHANGELOG.md and remove RELEASE_SUMMARY.md (#75)
- Trigger release to test clean changelog generation (#77)
- Final test of clean changelog generation (#78)
- Verify rebase boolean fix (#81)
- Verify clean changelog generation (#83)
- Final verify of changelog generation (#86)
- Test clean accumulate without rebase (#90)
- Remove test verification files (#92)
- Trigger clean draft PR (#95)
- Remove trigger file (#96)
- Test no duplicate sections (#98)

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
