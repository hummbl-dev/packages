# Distribution Spine FAQ

This FAQ addresses common questions about the HUMMBL distribution spine.  
It is intended as a practical companion to the policy docs, helping package engineers quickly orient themselves.

---

### What is the canonical source for package identity?
The canonical source of package identity is this repository.  
It defines the authoritative metadata and release records that downstream surfaces consume.

---

### How do Homebrew/Scoop/winget/Nix surfaces relate to this repo?
These package managers are *distribution surfaces*.  
They mirror or adapt the canonical identity defined here, but they are not sources of truth themselves.  
This repo provides the upstream definition; the surfaces provide user‑facing installation paths.

---

### What is a release artifact receipt?
A release artifact receipt is a short record that confirms what was published.  
It documents the version, the artifacts produced, and their checksums.  
Receipts make it easy to verify that a distribution event occurred and what it contained.

---

### How are versions determined?
Versions follow the upstream project’s release cadence.  
This repo does not invent new numbering schemes; it reflects the version identifiers chosen by the project maintainers.  
Operators ensure consistency across all distribution surfaces.

---

## Receipt of Change
- Added `docs/faq.md` answering common distribution spine questions.
- No new terminology introduced.
- No changes to operator‑authority surfaces.
