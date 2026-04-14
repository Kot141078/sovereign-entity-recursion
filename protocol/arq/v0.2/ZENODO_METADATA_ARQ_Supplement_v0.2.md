# ZENODO Metadata Draft — ARQ v0.2 Supplement
## Deposit template for GitHub / Zenodo release pairing

**Status:** Draft / depositor metadata template  
**Version:** 0.2-draft  
**Target:** Zenodo release deposit for ARQ v0.2 supplement package  
**Author:** Ivan Kotov  
**Place / year:** Bruxelles, 2026

---

## 0. Depositor note

This file is a structured metadata draft for the Zenodo deposit corresponding to the ARQ v0.2 supplement package.

It is meant to reduce friction at release time.

Before deposit:

- replace placeholder fields where necessary;
- confirm repository URL and tag;
- confirm license and publication type;
- confirm whether this release is linked to a specific GitHub tag or a standalone upload.

---

## 1. Recommended basic metadata

### Title
**ARQ v0.2 Supplement: Anti-Resonance Correction Protocol for Long-Lived Sovereign Entities**

### Version
`0.2-draft`

### Publication date
`2026-__-__`  
Replace with the actual deposit date.

### Resource type
Recommended:
- **Publication** → **Technical note / Protocol supplement**

If Zenodo category granularity changes, choose the closest equivalent that preserves the protocol/documentation nature of the release.

### Language
`English`

### License
Recommended default for text artifacts:
- `CC BY 4.0`

If code examples or machine-readable schemas are included in the same deposit and require a different license, declare the split explicitly in the description.

---

## 2. Creators

### Creator 1
- **Family name:** Kotov
- **Given name:** Ivan
- **Affiliation:** Independent Researcher
- **Place:** Brussels, Belgium
- **ORCID:** optional / add if available

If additional contributors are later added for editing, typesetting, or implementation, they SHOULD be listed separately rather than folded into the author field.

---

## 3. Description draft

### Short description
ARQ v0.2 Supplement is a release-grade document package for the Anti-Resonance Correction Protocol (ARQ), a protocol layer for handling deviation, bounded adaptation, and witnessed memory promotion in long-lived sovereign digital entities.

### Long description
This deposit contains the ARQ v0.2 supplement package, prepared as a structured extension of the broader AGI / SER / L4 corpus.

The package includes:

- the ARQ v0.2 Normative Core;
- system models and assumptions;
- notation and sign conventions;
- error valuation and anomaly scoring discipline;
- Experience Artifact lifecycle and witness binding;
- classical boundedness theorem and proof companion;
- quantum boundary theorem and proof companion;
- capsule and witness record schemas;
- classical implementation profiles;
- failure modes and safe degradation;
- integration map to SER / L4 Witness / Beacon / VXCX;
- test, audit, and conformance matrix;
- release-layer documents, including executive summary, doc map, changelog, and integrity manifest.

The package is designed to make ARQ publishable, reviewable, auditable, and repository-stable without relying on oral explanation or implicit reconstruction of assumptions.

The protocol’s central stance is that a long-lived entity may encounter informative deviation, but no deviation may become authoritative memory without declared boundary discipline, witnessable review, and bounded promotion authority.

---

## 4. Keywords

Recommended keyword set:

- Anti-Resonance Correction Protocol
- ARQ
- long-lived AI entities
- sovereign digital entities
- `c = a + b`
- Reality Boundary Layer
- L4
- witness trails
- Experience Artifacts
- bounded adaptation
- trust and provenance
- anomaly scoring
- bounded entropy
- quantum boundary
- protocol architecture
- cybernetic stability

Use a subset if the platform requires fewer keywords.

---

## 5. Related identifiers

### Parent corpus / contextual references
Recommended related-identifier fields (replace placeholders if needed):

1. **AGI repository / release**  
   Relation: `isSupplementTo` or `isPartOf`  
   Identifier: `<GitHub release URL or DOI>`

2. **SER repository / release**  
   Relation: `isSupplementTo` or `references`  
   Identifier: `<GitHub release URL or DOI>`

3. **L4 Witness repository / release**  
   Relation: `references`  
   Identifier: `<GitHub release URL or DOI>`

4. **GitHub tag for this ARQ supplement**  
   Relation: `isIdenticalTo` or `isSourceOf` depending on workflow  
   Identifier: `<GitHub tag URL>`

### Suggested relation language
- `isSupplementTo` for upstream architectural corpus;
- `references` for adjacent protocols used but not superseded;
- `isVersionOf` for later stabilized releases;
- `isSourceOf` only if the Zenodo record is generated directly from the repository release.

---

## 6. Communities and funding

### Communities
Optional suggested communities if available on Zenodo:

- artificial intelligence
- distributed systems
- trustworthy AI
- protocol engineering
- cybernetics

### Funding
Leave blank unless there is a specific grant or institutional support to declare.

Do **not** imply funded status unless it exists formally.

---

## 7. Notes for repository pairing

If this deposit is paired with a GitHub release:

1. ensure the Git tag matches the title/version;
2. ensure `SHA256SUMS_ARQ_Supplement_v0.2.txt` is included in the release assets or repository root;
3. ensure README and DOC MAP in the repository point to the same canonical file names as the deposit;
4. ensure no placeholder metadata remains in this file before final archive.

---

## 8. Suggested citation draft

**Kotov, Ivan.** *ARQ v0.2 Supplement: Anti-Resonance Correction Protocol for Long-Lived Sovereign Entities.* Zenodo, 2026. Version 0.2-draft.

Replace with final DOI and publication date once the record is minted.

---

## 9. Integrity note

This metadata draft assumes that the release package is accompanied by:

- a canonical file list,
- a SHA-256 manifest,
- and a stable repository tag or archive snapshot.

Metadata without integrity pairing is not enough for a protocol release.

---

## Bridges (required)

**Explicit bridge:** this metadata layer connects the ARQ supplement to the publication discipline already implicit in the wider AGI / SER / L4 corpus: protocols are not just written, they are versioned, archived, linked, and made independently verifiable.

**Hidden bridge #1 (Ashby / institutional control):** repository publication and archival publication serve different control environments. GitHub supports iteration and visibility; Zenodo supports citation and frozen reference. Both are needed because one channel does not regulate the other’s failure mode.

**Hidden bridge #2 (information theory / discoverability):** metadata is a compression layer for trust and retrieval. A good title, keyword set, and related-identifier structure reduce semantic loss when the artifact leaves its original repository context.

---

## Earth paragraph

A good archive record is like the label on a flight recorder pulled from a wreck: not philosophy, not marketing, just enough stable identification that another person can find the right object, match it to the right machine, and verify that the record really belongs there. That is what this metadata is for.
