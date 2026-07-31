## ❌ package.json version changed on a non-release branch

**Rule:** `package.json` `version` may only change on `release/from-v*` branches (found: `{{BASE_VERSION}}` → `{{CURRENT_VERSION}}`). Version bumps are how the release action detects a curated base release; a bump on a feature branch corrupts that signal.

**Fix this PR:**
```bash
git checkout origin/{{BASE_BRANCH}} -- package.json
git commit -m "chore: revert version bump (releases bump version on the release PR)"
git push
```

**To cut a release:** find the draft PR on the `release/from-v{{BASE_VERSION}}` branch → curate CHANGELOG.md (between the `USER-EDITABLE SECTION` markers) → bump `package.json` there → merge. Merging tags the base release and updates the floating tags.

Docs: https://github.com/cad0p/semver-calver-release#base-releases-manual-curated
