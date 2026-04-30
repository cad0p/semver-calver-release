# Release v1.1.2 Summary

This patch release fixes edge cases in the draft changelog PR workflow:

## Fixes

- **Branch-aware package.json reading**: The `release` action now reads `package.json` from the release branch (not `main`) when generating versioned changelog headings and updating PR titles. This ensures the changelog correctly reflects the version the user intends to release.

- **Validation workflow updates PR title**: The `validate-release-pr` action now auto-updates the PR title to match the bumped `package.json` version when validation passes.

## New Features

- **`validate-release-pr` action**: A new composite action that blocks merging of release PRs until `package.json` version is bumped from the base version. Add it as a required status check in branch protection to enforce this.

- **Versioned changelog headings**: Draft PR changelogs now use `[1.1.2] - 2026-04-30` format instead of `[unreleased]`, based on the current `package.json` version and today's date.
