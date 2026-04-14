# ARQ — PDF Twins

This directory stores PDF twins for the ARQ subsystem.

The PDF files are publication-facing companions to the Markdown sources in `protocol/arq/` and `docs/arq/`.

## ARQ v0.2 package

- ARQ v0.2 rendered PDF package now lives in `pdf/arq/v0.2/`.
- Its paired Markdown canonical package lives in `protocol/arq/v0.2/`.
- Package integrity is tracked by `hashes/SHA256SUMS_ARQ_Supplement_v0.2.txt`.

## Rules

- PDF files must not become the only discoverable surface.
- Markdown remains the primary editable source.
- Every PDF in this directory must be covered by the ARQ SHA-256 manifest.
- Canonical entry remains `protocol/arq/README.md`.
- Current additive theorem PDF companion: `theorem_bounded_entropy_arq.pdf`.
- Paired Markdown source: `protocol/arq/theorem_bounded_entropy_arq.md`.
