# SER v1.3.0 — Protocol Sources (EN/RU)

This directory contains the canonical Markdown sources of the SER v1.3.0 specification.

## Files

- `SER_v1.3_EN.md` — English specification (canonical).
- `SER_v1.3_RU.md` — Russian specification (canonical translation).
- `README.md` — this file.

## PDF builds

Rendered PDFs are stored in `/pdf`:

- `/pdf/SER_v1.3_EN.pdf`
- `/pdf/SER_v1.3_RU.pdf`

The Markdown sources and PDFs must remain structurally consistent:
section numbering, titles, and ordering should match across EN/RU and PDF.

## Integrity

This repository uses a reproducible SHA-256 manifest:

- `/hashes/SHA256SUMS_v1.3.0.txt`

Hashing instructions (PowerShell / Linux) should be placed under `/hashes` (if present).

## Relationship to L4 (Reality-Bound)

SER is designed to be compatible with the L4 Reality Boundary Layer published in the
Reality-Bound AI (L4) repository. In short:

- L4 provides the boundary conditions (cost, time, scarcity, identity, irreversibility).
- SER defines sovereign entity governance on top of those conditions:
  physical anchoring, topology, emergency modes, defense, and trust boundaries.
