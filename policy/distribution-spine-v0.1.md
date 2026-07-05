# Distribution Spine v0.1

> Status: **Non-canon** — proposal posture until explicitly adopted by HUMMBL governance.

## Purpose

The Distribution Spine defines a single, canonical source of truth for package
identity, versions, artifact URLs, checksums, SBOM pointers, provenance
pointers, and release status across all HUMMBL-owned packages.

This document establishes the v0.1 boundary: what the spine is, what it is not,
and how downstream install surfaces relate to it.

## Canonical Source of Truth

The `hummbl-dev/packages` repository is the canonical source of truth for:

- **Package identity** — the registry of packages owned and published by HUMMBL
  (see `index/package-identity-registry.json`).
- **Versions** — the set of released versions for each package.
- **Artifact URLs** — the canonical location of each release artifact.
- **Checksums** — the cryptographic checksum (sha256) for each artifact.
- **SBOM pointers** — the location of the Software Bill of Materials for each
  release.
- **Provenance pointers** — the location of the provenance attestation for each
  release.
- **Release status** — the lifecycle status of each release (e.g. `released`,
  `prerelease`, `yanked`).

No other repository or system may independently define canonical artifact
identity. Downstream surfaces consume this metadata; they do not author it.

## Downstream Generated / Policy-Validated Surfaces

The following surfaces are **downstream** of the Distribution Spine. They are
generated from, and validated against, the canonical metadata in this
repository:

| Surface | Repository | Relationship |
| --- | --- | --- |
| Homebrew tap | `hummbl-dev/homebrew-tap` | Generated from canonical metadata |
| Scoop bucket | `hummbl-dev/scoop-bucket` | Generated from canonical metadata |
| Winget manifests | `hummbl-dev/winget-manifests` | Generated from canonical metadata |
| Nix | `hummbl-dev/nix` | Generated from canonical metadata |

Each downstream surface:

1. Is produced by deterministic generation from the canonical metadata in this
   repository.
2. Is policy-validated against the Distribution Spine before publication.
3. Carries a receipt linking it back to the canonical release artifact (see
   `schemas/release-artifact-receipt-v0.1.json`).

## Non-Canon Posture

This v0.1 policy is **non-canon**. It describes a proposed architecture and
boundary. It does not, by itself, bind any downstream repository or release
process. The posture becomes canon only when explicitly adopted by HUMMBL
governance, at which point a versioned adoption record will be filed in this
repository.

Until adoption:

- Downstream surfaces may continue to operate under their existing processes.
- This repository may be used as a reference and staging ground for the
  canonical metadata format.
- No downstream repository is required to consume or validate against the
  spine.

## Scope Boundary

The Distribution Spine v0.1 covers:

- The definition of canonical package identity and metadata.
- The relationship between this repository and downstream install surfaces.
- The receipt schema that links releases to generated surfaces.

It does **not** cover:

- The internal build pipeline of individual packages.
- Signing key management or rotation policy.
- End-user installation workflows.
- Downstream surface-specific formatting rules (those belong in their
  respective repositories, validated against this spine).
