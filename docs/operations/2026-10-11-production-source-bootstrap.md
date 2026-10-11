# ENVISEAM production source bootstrap

Owner: ENVISEAM. Operator: Jazz LI. Prepared October 11, 2026, Singapore.
Status: local proposal only; publication, settings changes and merge await their
exact approvals. This change does not deploy or transfer the running services.

## Source boundary

Seed `production` with deployed commit
`cd5ca3bfc566176fb0d3c746d18dc410028a4d51`, tree
`772cc9668ace0823eb44cf0a8f888865feada79c`. Preserve the existing ENVISEAM
`main` at `db6212992738d4380a94fb6940140bcebf5d861d` and the existing
`codex/oauth-account-selection` branch. Do not rewrite, force-push or merge
this lineage into main. All fourteen commits absent from ENVISEAM main remain
in production's ancestry; the separate upstream upgrade is outside this change.

The source-to-deployment link was reverified against public OCI provenance for
`ghcr.io/jazzli/google_workspace_mcp@sha256:74d182c28b4fd0fa74a889f50c9c08fb024fa6ea699150f8c73a94014739a5a2`,
the packaged publisher at that exact source commit and `refs/heads/main`, with
GitHub-hosted runners required. This is evidence for the existing personal
artifact, not an ENVISEAM build or corporate deployment qualification.

## Proposed bootstrap order

1. Read back the exact repository, existing heads, protection and Actions policy.
   Stop on drift. Use one coordinated writer; readback is not a server lock.
2. Disable Actions in ENVISEAM only before importing any branch. Preserve
   publisher inactivity throughout bootstrap. This does not change personal
   repository settings or Railway configuration.
3. Create the production ref at the exact deployed source commit. GitHub already
   resolves this commit in the ENVISEAM fork network; use create-ref, which rejects
   an existing production branch, rather than an update-ref or force push.
4. Apply the reviewed main preservation rules and production PR/linear-history
   bootstrap rules; switch ENVISEAM's default branch to production and turn off
   merge commits. No existing main content is edited.
5. Discover the imported workflow IDs. Disable both container publishers,
   the PyPI/MCP Registry publisher and the maintainer-comment workflow; verify
   every disabled state. If GitHub cannot register or disable them while Actions
   is off, leave Actions off and stop. Do not enable Actions to find out.
6. Set the default workflow token to read-only and prevent workflow PR approvals.
   Allow only the three full-SHA checkout/Python/uv actions used by read-only CI;
   require SHA pinning. Enable only pytest and Ruff workflows, then Actions.
7. Publish the separately reviewed CI branch and open a draft PR into production.
   Check the exact PR head/merge SHA, actual pytest/ruff names, GitHub Actions app
   ID and passing results before installing strict required-status-check rules.
8. Merge the CI-only PR only after separate explicit owner merge approval. Verify
   the resulting protected source SHA and main's unchanged SHA. Keep all
   publishers disabled after this merge. No image publication is authorized.

The CI proposal changes only pytest and Ruff workflow configuration plus this
record. Both workflows receive contents-read tokens, retain job names `pytest`
and `ruff`, use full action SHAs and do not retain checkout credentials. Pytest
selects non-integration tests; live Google or Railway tests are not part of this
CI bootstrap. Ruff remains a read-only isolated `uvx` invocation at its locked
version. Main's existing commit and files remain untouched.

## Protection and later release work

The proposed production rules prohibit deletion and force-push, require ordinary
changes through PRs, linear history and resolved review threads, and later require
strict pytest/ruff checks from GitHub Actions. Zero GitHub review submissions is
intentional with one operator; each merge still requires explicit owner approval.
An administrator bypass, if configured, is break-glass only and must be recorded
and remediated. It is not used for the bootstrap CI merge.

Publication code, publisher workflows, packaged contracts, schemas and immutable
base-image pins remain byte-for-byte at the deployed source. Their personal
repository, main-ref and image identities are inherited release controls, not
corporate-ready publication controls. Adapting those contracts and qualifying an
ENVISEAM base image belong to a separately reviewed release phase. Never enable
or dispatch the inherited publishers on the strength of this source import.

The current Railway deployments, image digests, project placement, volumes and
credentials remain unchanged. Recovery of this bootstrap means retaining the
live image, leaving new source refs in place and stopping Actions if qualification
fails; changing settings again requires an exact approval. Do not delete branches,
weaken protections or touch personal systems as an implicit rollback.
