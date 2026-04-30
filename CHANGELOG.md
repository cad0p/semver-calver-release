# Changelog

All notable changes to this project will be documented in this file.
## [unreleased]

<!-- USER-EDITABLE SECTION START -->
<!-- Add your curated release notes here. This section is preserved across calver releases. -->
<!-- USER-EDITABLE SECTION END -->


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

### 📚 Documentation

- Clean up README with proper usage example (#7)
- Update README with git-cliff and draft PR workflow (#18)

### ⚙️ Miscellaneous Tasks

- Revert trigger comment (#2)
- Trigger release to test changelog fix (#10)
- Trigger clean release (#12)
- Trigger release (#19)
- Trigger release to test draft PR creation (#21)
- Trigger second release to test commit accumulation (#31)
