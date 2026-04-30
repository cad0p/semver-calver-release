# Changelog

All notable changes to this project will be documented in this file.

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

- Add PR links in changelog via cliff.toml postprocessor ([#102](https://github.com/cad0p/semver-calver-release/pull/102))

- Ship default cliff.toml with action, allow consumer override ([#104](https://github.com/cad0p/semver-calver-release/pull/104))


### 🐛 Bug Fixes

- Use native git-cliff commit_preprocessors for PR links, remove sed post-processing ([#105](https://github.com/cad0p/semver-calver-release/pull/105))

- Move commit_preprocessors from [changelog] to [git] section ([#106](https://github.com/cad0p/semver-calver-release/pull/106))

- Use previous base release tag for changelog range ([#107](https://github.com/cad0p/semver-calver-release/pull/107))


### 🚀 Features

- Versioned changelog headings, dynamic PR titles, release PR validation ([#50](https://github.com/cad0p/semver-calver-release/pull/50))

- Auto-rebase release branch on main when behind ([#67](https://github.com/cad0p/semver-calver-release/pull/67))

- Conflict-aware auto-rebase for draft PR branches ([#71](https://github.com/cad0p/semver-calver-release/pull/71))


### 🐛 Bug Fixes

- Validation workflow updates PR title on version bump ([#55](https://github.com/cad0p/semver-calver-release/pull/55))

- Read package.json from branch for versioned changelog and PR title ([#56](https://github.com/cad0p/semver-calver-release/pull/56))

- Prepend new changelog section instead of regenerating entire file ([#60](https://github.com/cad0p/semver-calver-release/pull/60))

- Skip first draft section when extracting old changelog body ([#62](https://github.com/cad0p/semver-calver-release/pull/62))

- Extract only first user-editable section ([#64](https://github.com/cad0p/semver-calver-release/pull/64))

- Remove harmful auto-rebase that silently overwrites main changes ([#70](https://github.com/cad0p/semver-calver-release/pull/70))

- Use cliff.toml with tag_pattern to ignore calver tags in changelog generation ([#76](https://github.com/cad0p/semver-calver-release/pull/76))

- Use JSON input for rebase ref update (boolean force) ([#79](https://github.com/cad0p/semver-calver-release/pull/79))

- Use actual newlines in default user section, strip header from old body ([#82](https://github.com/cad0p/semver-calver-release/pull/82))

- Fetch rebased commit so git show works locally ([#85](https://github.com/cad0p/semver-calver-release/pull/85))

- Ensure OIDC trusted publishing by removing explicit auth tokens ([#88](https://github.com/cad0p/semver-calver-release/pull/88))

- Remove auto-rebase, just accumulate on branch tip ([#89](https://github.com/cad0p/semver-calver-release/pull/89))

- Use OIDC token for npm trusted publishing ([#93](https://github.com/cad0p/semver-calver-release/pull/93))

- Use index() for literal string match in awk (regex chars in version) ([#97](https://github.com/cad0p/semver-calver-release/pull/97))


### 📚 Documentation

- Retroactively fix v1.1.0 changelog heading ([#59](https://github.com/cad0p/semver-calver-release/pull/59))


### ⚙️ Miscellaneous Tasks

- Trigger release to test versioned changelog ([#51](https://github.com/cad0p/semver-calver-release/pull/51))

- Remove trigger test files ([#53](https://github.com/cad0p/semver-calver-release/pull/53))

- Remove VERSIONED.md trigger file ([#54](https://github.com/cad0p/semver-calver-release/pull/54))

- Trigger release to test branch package.json version ([#57](https://github.com/cad0p/semver-calver-release/pull/57))

- Remove test trigger file ([#58](https://github.com/cad0p/semver-calver-release/pull/58))

- Trigger release to test changelog prepend ([#61](https://github.com/cad0p/semver-calver-release/pull/61))

- Remove prepend test file ([#63](https://github.com/cad0p/semver-calver-release/pull/63))

- Trigger release to test clean changelog ([#65](https://github.com/cad0p/semver-calver-release/pull/65))

- Remove CLEAN.md test file ([#66](https://github.com/cad0p/semver-calver-release/pull/66))

- Trigger release to test auto-rebase ([#69](https://github.com/cad0p/semver-calver-release/pull/69))

- Modify CHANGELOG.md to test conflict detection ([#72](https://github.com/cad0p/semver-calver-release/pull/72))

- Trigger release after CHANGELOG.md conflict ([#73](https://github.com/cad0p/semver-calver-release/pull/73))

- Remove conflict test files ([#74](https://github.com/cad0p/semver-calver-release/pull/74))

- Clean up CHANGELOG.md and remove RELEASE_SUMMARY.md ([#75](https://github.com/cad0p/semver-calver-release/pull/75))

- Trigger release to test clean changelog generation ([#77](https://github.com/cad0p/semver-calver-release/pull/77))

- Final test of clean changelog generation ([#78](https://github.com/cad0p/semver-calver-release/pull/78))

- Verify rebase boolean fix ([#81](https://github.com/cad0p/semver-calver-release/pull/81))

- Verify clean changelog generation ([#83](https://github.com/cad0p/semver-calver-release/pull/83))

- Final verify of changelog generation ([#86](https://github.com/cad0p/semver-calver-release/pull/86))

- Test clean accumulate without rebase ([#90](https://github.com/cad0p/semver-calver-release/pull/90))

- Remove test verification files ([#92](https://github.com/cad0p/semver-calver-release/pull/92))

- Trigger clean draft PR ([#95](https://github.com/cad0p/semver-calver-release/pull/95))

- Remove trigger file ([#96](https://github.com/cad0p/semver-calver-release/pull/96))

- Test no duplicate sections ([#98](https://github.com/cad0p/semver-calver-release/pull/98))

- Remove test file ([#100](https://github.com/cad0p/semver-calver-release/pull/100))

- Remove CLEAN2.md ([#101](https://github.com/cad0p/semver-calver-release/pull/101))

- *(release)* V1.1.2 ([#99](https://github.com/cad0p/semver-calver-release/pull/99))


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
