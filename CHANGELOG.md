# Changelog

All notable changes to this project will be documented in this file.
## [1.1.2] - 2026-04-30

<!-- USER-EDITABLE SECTION START -->
This release introduces automated changelog management via git-cliff, signed commits via the GitHub API, and draft PRs for curating base releases. The semver-calver-release action now supports unified changelogs that accumulate across calver releases.
<!-- USER-EDITABLE SECTION END -->


### 🚀 Features

- Versioned changelog headings, dynamic PR titles, release PR validation (#50)

### 🐛 Bug Fixes

- Validation workflow updates PR title on version bump (#55)
- Read package.json from branch for versioned changelog and PR title (#56)

### ⚙️ Miscellaneous Tasks

- Trigger release to test versioned changelog (#51)
- Remove trigger test files (#53)
- Remove VERSIONED.md trigger file (#54)
