## ❌ Release PR without a version bump

**Rule:** A release PR must bump `package.json` `version` above the last released base version ({{MAIN_BASE}}). The bump is what turns the accumulating draft into a curated base release.

**Fix this PR:**
```bash
git checkout {{BRANCH}}
# edit package.json: bump "version" above {{MAIN_BASE}} (e.g. next patch)
# curate CHANGELOG.md between the USER-EDITABLE SECTION markers while you're here
git commit -m "chore(release): v<version> — curate changelog and bump version"
git push
```
The PR title and the CHANGELOG heading date update automatically on push. Checks stuck at `action_required` after the bot commit? Approve the runs: `gh api -X POST /repos/{owner}/{repo}/actions/runs/<id>/approve`.

Docs: https://github.com/cad0p/semver-calver-release#base-releases-manual-curated
