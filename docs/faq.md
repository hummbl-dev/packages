# Package Distribution FAQ

Status: non-canon orientation document for the v0.1 package distribution spine.

## What is the canonical source for package identity?

The proposed canonical source is this repository, `hummbl-dev/packages`, through the package identity registry and release artifact receipts. The current v0.1 posture is non-canon until explicitly adopted by HUMMBL governance.

## How do Homebrew, Scoop, winget, and Nix surfaces relate to this repo?

They are downstream install surfaces. In the proposed model, this repository owns package identity, version, artifact URL, checksum, SBOM pointer, provenance pointer, and release status. Downstream surfaces are generated or policy-validated from that metadata.

## What is a release artifact receipt?

A release artifact receipt is a structured record for one package release. It records identity, version, artifact location, checksum, SBOM pointer, provenance pointer, release status, and generated downstream surfaces.

## How are versions determined?

Versions should come from the canonical package metadata in this repository. Downstream package managers should not independently invent or advance versions.

## Can downstream repos patch package metadata directly?

In the proposed model, no. Downstream repos may carry surface-specific formatting, but package identity and artifact metadata should trace back to the canonical receipt in this repository.

## What does non-canon mean here?

It means the FAQ explains the current proposal and contributor orientation. It does not bind release processes until the governance path explicitly adopts the policy.

## Receipt

- Added a package distribution FAQ for first-time package engineers.
- Answered canonical identity, downstream surface, release receipt, and versioning questions.
- Kept the document non-canon and did not modify release authority.
