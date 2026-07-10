# Distribution Spine FAQ

This FAQ addresses common questions about the HUMMBL distribution spine.  
It is intended as a practical companion to the policy docs, helping package engineers quickly orient themselves.

---

## What is the canonical source for package identity?

Under the Distribution Spine v0.1 proposal, this repository is the **proposed** canonical source of package identity and release metadata.  
This posture becomes canon only if explicitly adopted by HUMMBL governance.

---

## How do Homebrew/Scoop/winget/Nix surfaces relate to this repo?

These package managers are *distribution surfaces*.  
They mirror or adapt the canonical identity defined here, but they are not sources of truth themselves.  
This repo provides the upstream definition; the surfaces provide user‑facing installation paths.

---

## What is a release artifact receipt?

Under the v0.1 proposal, a release artifact receipt is a short record that confirms what was published.  
It documents the version, the artifacts produced, and their checksums.  
Receipts use schema fields directly:  
`packageId`, `version`, `artifactUrl`, `sha256`, `sbomPointer`, `provenancePointer`, `releaseStatus`, and `generatedSurfaces`.  
This posture becomes canon only if explicitly adopted by HUMMBL governance.

---

## How are versions determined?

Under the v0.1 proposal, versions follow the upstream project’s release cadence.  
This repo does not invent new numbering schemes; it reflects the version identifiers chosen by the project maintainers.  
Operators ensure consistency across all distribution surfaces.  
This posture becomes canon only if explicitly adopted by HUMMBL governance.

---

## Can downstream repos patch package metadata directly?

In the proposed model, no. Downstream repos may carry surface‑specific formatting, but package identity and artifact metadata should trace back to the canonical receipt in this repository.

---

## What does non‑canon mean here?

It means the FAQ explains the current proposal and contributor orientation. It does not bind release processes until the governance path explicitly adopts the policy.

---

### Receipt of Change

- Added `docs/faq.md` answering common distribution spine questions.
- Added downstream patch and non-canon definition Q&As (salvaged from draft PR #8).
- Preserved v0.1 non‑canon proposal posture throughout.
- No new terminology introduced.
- No changes to operator‑authority surfaces.
