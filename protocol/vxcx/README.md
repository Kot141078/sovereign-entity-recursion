# VXCX — Visual eXperience Capsule eXchange
Status: Draft (v0.1)
Layer: L2 (Exchange) + L4 (Reality Boundary constraints)
Parent stack: SER ecosystem (SER / EWCEP / SER-FED / L3+)

## Scope
VXCX defines a privacy-first exchange format for *visual experience capsules* between entities `c`,
without sharing raw pixels by default.

VXCX is an **adjacent protocol**: it does not modify SER core.
It provides a constrained artifact format that can be referenced as EA/auxiliary evidence,
and can be logged via L4 Witness events.

## Profiles
- VXCX-BASE: no pixels, no embeddings, size-bounded (default).
- VXCX-SEARCH: optional search fields (tokens/embeddings) under explicit policy.
- VXCX-WITNESS: requires canonical hashing + optional signatures + chain linkage.

## Files
- `VXCX_v0.1_Normative_Draft_EN.md` — normative skeleton (MUST/SHOULD, schema, events).
- `CHANGELOG.md` — VXCX changelog.

## Reading order
1) This README
2) `VXCX_v0.1_Normative_Draft_EN.md`
3) PDF snapshot under `/pdf` (for citation)
4) SHA-256 manifest under `/hashes` (for verification)

## Bridges (required)
**Explicit bridge:** `c = a + b` → capsules are “b-shaped” artifacts that remain attributable to `a`
and auditable for `c`.
**Hidden bridge #1 (Ashby):** capsule structure preserves requisite variety without leaking raw channels.
**Hidden bridge #2 (Cover & Thomas):** verification bandwidth is compressed into hashes and bounded payloads.

## Earth paragraph (engineering)
This is like a flight-data recorder abstraction: the system exports *events and structured summaries*,
not raw sensor feeds, unless an explicit disclosure gate is opened.