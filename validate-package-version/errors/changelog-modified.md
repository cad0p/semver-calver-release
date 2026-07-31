## ❌ CHANGELOG.md modified on a non-release branch

**Rule:** Changelog edits — including typo fixes to historical entries — belong on the `release/from-v*` draft release PR. The release action treats main's CHANGELOG.md as the source of truth for finalized sections, so a normal PR landing changelog edits (or premature release headings) corrupts the next release's notes.

**Fix this PR:**
```bash
git checkout origin/{{BASE_BRANCH}} -- CHANGELOG.md
git commit -m "chore: revert CHANGELOG edit (curation happens on the release PR)"
git push
```
Don't lose your changelog text — move it into the **PR body** instead (e.g. a `## Release notes` section). Release curation works by aggregating merged PRs and their bodies to draft the highlights in the next release's user-editable changelog section, so the PR description is the canonical place for user-facing notes; the session editing the release PR will pick them up from there. Make sure the PR body stays accurate if the change evolves during review.

**To cut a release:** find the draft PR on the `release/from-v{{BASE_VERSION}}` branch → paste your notes into CHANGELOG.md between the `USER-EDITABLE SECTION` markers → bump `package.json` → mark ready → merge. The heading date and PR title are set automatically. If checks sit at `action_required` after the bot commit, approve the workflow runs (`gh api -X POST /repos/{owner}/{repo}/actions/runs/<id>/approve`).

Docs: https://github.com/cad0p/semver-calver-release#base-releases-manual-curated
