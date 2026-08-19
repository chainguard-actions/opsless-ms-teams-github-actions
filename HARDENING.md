<!-- markdownlint-disable -->

# Hardening Report: opsless--ms-teams-github-actions/1.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **opsless--ms-teams-github-actions/1.2.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses tag-based (non-SHA-pinned) action references. Both `actions/checkout@v4` and `actions/setup-node@v4` use mutable version tags instead of full 40-character commit SHA digests. A compromised or altered tag could silently introduce malicious code into the workflow. These should be pinned to their full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/test.yml:14`
- `.github/workflows/test.yml:17`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/test.yml` has no top-level `permissions:` key, and the `test` job also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be broader than necessary. A minimal `permissions:` block (e.g. `contents: read`) should be added at the top level or per-job.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/test.yml: (1) Pinned actions/checkout@v4 to SHA 34e114876b0b11c390a56381ad16ebd13914f8d5 and actions/setup-node@v4 to SHA 49933ea5288caeca8642d1e84afbd3f7d6820020, preserving the version tag in comments. (2) Added a top-level `permissions: contents: read` block to restrict the GITHUB_TOKEN to the minimum required permissions.

