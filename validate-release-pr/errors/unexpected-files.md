## ❌ Release PR contains unexpected files

**Rule:** Release branches may only change `package.json`, lockfiles, and `CHANGELOG.md` — a release PR is a curated version bump, not a vehicle for code changes. Found:
```
{{UNEXPECTED_FILES}}
```

**Fix this PR:** move those changes to their own feature branch / PR and merge them to main first; the release branch picks them up automatically when the action rebuilds it from `origin/main`.
```bash
git checkout {{BRANCH}}
git checkout origin/main -- <file>   # per unexpected file, to revert it here
git commit -m "chore: drop non-release files (moved to a feature PR)"
git push
```

Docs: https://github.com/cad0p/semver-calver-release#draft-changelog-prs
