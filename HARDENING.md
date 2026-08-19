<!-- markdownlint-disable -->

# Hardening Report: opsless--ms-teams-github-actions/2.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **opsless--ms-teams-github-actions/2.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/test.yml references actions using mutable tag refs (@v4) instead of full 40-character commit SHA digests. If the upstream action tag is moved or the repository is compromised, the workflow will silently execute attacker-controlled code. Failing references: `actions/checkout@v4` (line 15) and `actions/setup-node@v4` (line 17). Pin each to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/test.yml:15`
- `.github/workflows/test.yml:17`

### missing-permissions (severity: medium)

The workflow file .github/workflows/test.yml has no top-level `permissions:` key and the single job (`test`) also has no `permissions:` key. Without explicit permissions, the workflow inherits the repository default (typically `contents: write` for older repos or the org default), granting broader access than necessary. Add a top-level `permissions: {}` block (or the minimal required scopes) to restrict the GITHUB_TOKEN.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/test.yml: (1) Pinned actions/checkout@v4 to full SHA 34e114876b0b11c390a56381ad16ebd13914f8d5 and actions/setup-node@v4 to full SHA 49933ea5288caeca8642d1e84afbd3f7d6820020, preserving the v4 tag as inline comments. (2) Added top-level `permissions: {}` block to restrict the GITHUB_TOKEN to no permissions, preventing unintended broad access.

