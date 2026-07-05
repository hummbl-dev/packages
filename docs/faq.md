# Distribution Spine FAQ

This FAQ addresses common questions about the HUMMBL distribution spine.  
It is intended as a practical companion to the policy docs, helping package engineers quickly orient themselves.

---

## What is the canonical source for package identity?

The canonical source of package identity is this repository.  
It defines the authoritative metadata and release records that downstream surfaces consume.

---

## How do Homebrew/Scoop/winget/Nix surfaces relate to this repo?

These package managers are *distribution surfaces*.  
They mirror or adapt the canonical identity defined here, but they are not sources of truth themselves.  
This repo provides the upstream definition; the surfaces provide user‑facing installation paths.

---

## What is a release artifact receipt?

A release artifact receipt is the canonical record linking a release artifact to its generated install surfaces.
It includes the package ID, version, artifact URL, checksum, SBOM/provenance pointers, release status, and generated surfaces.

---

## How are versions determined?

Versions are defined in this repository’s canonical release metadata.
Downstream surfaces consume those version identifiers; they do not invent their own.

---

### Receipt of Change

- Added `docs/faq.md` answering common distribution spine questions.
- No new terminology introduced.
- No changes to operator‑authority surfaces.
