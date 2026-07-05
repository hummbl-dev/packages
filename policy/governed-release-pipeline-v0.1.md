# Governed Release Pipeline v0.1

> Status: **Non-canon** — proposal posture until explicitly adopted by HUMMBL
> governance.

## Purpose

This document defines the governed release pipeline for HUMMBL-owned packages.
It describes how a single canonical release triggers the deterministic
generation of every downstream install surface, and how the receipt chain links
the release to those surfaces.

This policy is a companion to the
[Distribution Spine v0.1](./distribution-spine-v0.1.md).

## Principle: One Release, Many Install Surfaces

A release is authored **once**, in `hummbl-dev/packages`, as a canonical
release artifact receipt (see `schemas/release-artifact-receipt-v0.1.json`).
That single release is the trigger for generating every downstream install
surface:

1. **homebrew-tap**
2. **scoop-bucket**
3. **winget-manifests**
4. **nix**

There is exactly one release event. There are many generated surfaces. The
surfaces are never authored independently of the canonical release.

## Deterministic Generation

Generation of downstream surfaces is **deterministic** from the canonical
metadata:

- The inputs are the package identity, version, artifact URL, checksum, SBOM
  pointer, and provenance pointer from the canonical receipt.
- Given the same canonical metadata, the same surface output is produced.
- No downstream surface introduces artifact identity (URL, checksum, version)
  that is not present in the canonical receipt.

This determinism is what allows the surfaces to be policy-validated rather than
hand-curated.

## Receipt Chain

Every release produces a chain of receipts:

1. **Canonical receipt** — filed in `hummbl-dev/packages` at release time,
   conforming to `schemas/release-artifact-receipt-v0.1.json`.
2. **Generated surface entries** — each downstream surface update is recorded
   as an entry in the canonical receipt's `generatedSurfaces` array, including
   the surface type, target repository, and commit SHA of the generated update.

The chain is traversable: starting from a canonical receipt, a consumer can
locate every generated surface and the exact commit that realized it.
Conversely, starting from a generated surface commit, a consumer can trace back
to the canonical release artifact and its checksum, SBOM, and provenance.

## Pipeline Stages

1. **Author release** — a canonical release artifact receipt is authored in
   `hummbl-dev/packages` with `releaseStatus` set to `prerelease`.
2. **Generate surfaces** — the pipeline deterministically generates updates for
   each downstream surface from the canonical metadata.
3. **Policy-validate** — each generated surface is validated against the
   Distribution Spine: artifact URL, checksum, version, and identity must match
   the canonical receipt.
4. **Publish surfaces** — validated surface updates are committed to their
   respective repositories; the commit SHAs are recorded back into the
   canonical receipt's `generatedSurfaces` array.
5. **Release** — the canonical receipt's `releaseStatus` is advanced to
   `released`.

A release may be **yanked** by advancing `releaseStatus` to `yanked`; the
generated surfaces are regenerated to reflect the yanked state.

## Non-Canon Posture

This v0.1 pipeline policy is **non-canon**. It describes a proposed governed
pipeline. It does not, by itself, bind any downstream repository or release
process. The posture becomes canon only when explicitly adopted by HUMMBL
governance, at which point a versioned adoption record will be filed in this
repository.

Until adoption, existing release processes may continue unchanged.
