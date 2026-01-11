# How to Verify Release Integrity (SHA-256)

This repository provides a reproducible integrity manifest for each public release.

The file `SHA256SUMS_v1.3.0.txt` contains SHA-256 checksums for all release artifacts,
including protocol documents and PDFs.

## Purpose

The goal of this procedure is to allow any third party to independently verify that:
- the published files were not modified after release,
- local copies are bit-identical to the released artifacts,
- the release can be cited or archived with cryptographic confidence.

This is an integrity mechanism, not a DRM or access-control system.

---

## Verification (Linux / macOS)

From the repository root:

```bash
sha256sum -c hashes/SHA256SUMS_v1.3.0.txt

