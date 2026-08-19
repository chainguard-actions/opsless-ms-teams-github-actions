<!-- markdownlint-disable -->

# Hardening Report: opsless--ms-teams-github-actions/1.3.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **opsless--ms-teams-github-actions/1.3.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/test.yml references two actions using mutable version tags (@v4) instead of pinned full 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the tag is moved to a malicious commit. Failing references: `actions/checkout@v4` (line 15) and `actions/setup-node@v4` (line 17).

Locations:

- `.github/workflows/test.yml:15`
- `.github/workflows/test.yml:17`

### missing-permissions (severity: medium)

The workflow file .github/workflows/test.yml has no top-level `permissions:` key and the `test` job also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (e.g., write access). A minimal permissions block such as `permissions: read-all` or specific scopes should be added.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/test.yml: (1) Pinned actions/checkout@v4 to SHA 11d5960a326750d5838078e36cf38b85af677262 and actions/setup-node@v4 to SHA 49933ea5288caeca8642d1e84afbd3f7d6820020, preserving the original tags as inline comments. (2) Added a top-level `permissions: contents: read` block — the minimal permission needed for a workflow that checks out code and runs tests.

