## ❌ CHANGELOG.md modified on a non-release branch

**Rule:** Changelog edits — including typo fixes to historical entries — belong on the `release/from-v*` draft release PR. The release action treats main's CHANGELOG.md as the source of truth for finalized sections, so a normal PR landing changelog edits (or premature release headings) corrupts the next release's notes.

**Fix this PR:**
```bash
git checkout origin/{{BASE_BRANCH}} -- CHANGELOG.md
git commit -m "chore: revert CHANGELOG edit (curation happens on the release PR)"
git push
```
Carry your changelog text over to the draft release PR instead of losing it.

**To cut a release:** find the draft PR on the `release/from-v{{BASE_VERSION}}` branch → paste your notes into CHANGELOG.md between the `USER-EDITABLE SECTION` markers → bump `package.json` → mark ready → merge. The heading date and PR title are set automatically. If checks sit at `action_required` after the bot commit, approve the workflow runs (`gh api -X POST /repos/{owner}/{repo}/actions/runs/<id>/approve`).

Docs: https://github.com/cad0p/semver-calver-release#base-releases-manual-curated
