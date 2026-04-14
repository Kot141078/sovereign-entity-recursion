# ARQ v0.2 Supplement — README
## Release entry for the ARQ v0.2 document package

**Status:** Draft / repository entrypoint  
**Version:** 0.2-draft  
**Parent corpus:** AGI / SER / L4 / L4 Witness / Beacon / VXCX  
**Author:** Ivan Kotov  
**Place / year:** Bruxelles, 2026

---

## 0. What this repository layer is

This supplement is the canonical document package for **ARQ v0.2**.

ARQ = **Anti-Resonance Correction Protocol**.

Its role in the wider corpus is simple:

- long-lived entities need memory and continuity;
- continuity requires bounded handling of deviation;
- deviation requires more than fault correction;
- some deviations must be suppressed, some merely logged, and a smaller subset may become authoritative memory only after witnessable review.

This package collects the documents that make that logic explicit, testable, and publishable.

---

## 1. What ARQ is

ARQ is a protocol layer for persistent entities that:

- detects deviation inside a declared boundary,
- classifies it under explicit budgets,
- suppresses destructive propagation,
- stages exploratory deviations through review,
- and permits only witnessed, attributable, bounded promotion into authoritative memory.

ARQ does **not** replace SER, L4, L4 Witness, Beacon, or VXCX.

It sits between them as the deviation-handling and memory-promotion discipline.

---

## 2. Package inventory

The substantive ARQ documents in this package are shipped in paired formats:

- a canonical Markdown file (`.md`);
- and a same-name PDF companion (`.pdf`).

### 2.1 Orientation and entry documents
- `ARQ_v0.2_One_Page_Essence_EN.md` / `ARQ_v0.2_One_Page_Essence_EN.pdf`
- `ARQ_v0.2_Executive_Summary.md` / `ARQ_v0.2_Executive_Summary.pdf`

### 2.2 Core and discipline documents
- `ARQ_v0.2_Normative_Core.md` / `ARQ_v0.2_Normative_Core.pdf`
- `ARQ_System_Models_and_Assumptions_v0.2.md` / `ARQ_System_Models_and_Assumptions_v0.2.pdf`
- `ARQ_Notation_and_Sign_Conventions_v0.2.md` / `ARQ_Notation_and_Sign_Conventions_v0.2.pdf`
- `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.md` / `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.pdf`
- `ARQ_EA_Lifecycle_and_Witness_Binding_v0.2.md` / `ARQ_EA_Lifecycle_and_Witness_Binding_v0.2.pdf`

### 2.3 Theorem and proof branch
- `ARQ_Classical_Boundedness_Theorem_v0.2.md` / `ARQ_Classical_Boundedness_Theorem_v0.2.pdf`
- `ARQ_Classical_Boundedness_Theorem_prouve_v0.2.md` / `ARQ_Classical_Boundedness_Theorem_prouve_v0.2.pdf`
- `ARQ_Quantum_Boundary_Theorem_v0.2.md` / `ARQ_Quantum_Boundary_Theorem_v0.2.pdf`
- `ARQ_Quantum_Boundary_Theorem_prouve_v0.2.md` / `ARQ_Quantum_Boundary_Theorem_prouve_v0.2.pdf`

### 2.4 Schemas, implementation, and safety branch
- `ARQ_Capsule_and_Witness_Record_Schemas_v0.2.md` / `ARQ_Capsule_and_Witness_Record_Schemas_v0.2.pdf`
- `ARQ_Implementation_Profiles_Classical_v0.2.md` / `ARQ_Implementation_Profiles_Classical_v0.2.pdf`
- `ARQ_Failure_Modes_and_Safe_Degradation_v0.2.md` / `ARQ_Failure_Modes_and_Safe_Degradation_v0.2.pdf`
- `ARQ_Test_Audit_and_Conformance_Matrix_v0.2.md` / `ARQ_Test_Audit_and_Conformance_Matrix_v0.2.pdf`

### 2.5 Integration branch
- `ARQ_Integration_Map_to_SER_L4_Witness_Beacon_VXCX_v0.2.md` / `ARQ_Integration_Map_to_SER_L4_Witness_Beacon_VXCX_v0.2.pdf`

### 2.6 Release-layer payload files
- `README_ARQ_Supplement_v0.2.md`
- `DOC_MAP_ARQ_Supplement_v0.2.md`
- `CHANGELOG_ARQ_Supplement_v0.2.md`
- `ZENODO_METADATA_ARQ_Supplement_v0.2.md`

### 2.7 Integrity file
- `SHA256SUMS_ARQ_Supplement_v0.2.txt` (self-excluded from the payload set it verifies)

---

## 3. Quick start

### Reader path: shortest useful path
1. `ARQ_v0.2_One_Page_Essence_EN.md`
2. `ARQ_v0.2_Executive_Summary.md`
3. `ARQ_v0.2_Normative_Core.md`
4. `ARQ_System_Models_and_Assumptions_v0.2.md`
5. `ARQ_EA_Lifecycle_and_Witness_Binding_v0.2.md`
6. `ARQ_Test_Audit_and_Conformance_Matrix_v0.2.md`

### Technical reader path
1. `ARQ_v0.2_Normative_Core.md`
2. `ARQ_System_Models_and_Assumptions_v0.2.md`
3. `ARQ_Notation_and_Sign_Conventions_v0.2.md`
4. `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.md`
5. `ARQ_EA_Lifecycle_and_Witness_Binding_v0.2.md`
6. `ARQ_Capsule_and_Witness_Record_Schemas_v0.2.md`

### Proof path
1. `ARQ_System_Models_and_Assumptions_v0.2.md`
2. `ARQ_Notation_and_Sign_Conventions_v0.2.md`
3. `ARQ_Classical_Boundedness_Theorem_v0.2.md`
4. `ARQ_Classical_Boundedness_Theorem_prouve_v0.2.md`
5. `ARQ_Quantum_Boundary_Theorem_v0.2.md`
6. `ARQ_Quantum_Boundary_Theorem_prouve_v0.2.md`

### Implementer path
1. `ARQ_v0.2_Normative_Core.md`
2. `ARQ_Capsule_and_Witness_Record_Schemas_v0.2.md`
3. `ARQ_Implementation_Profiles_Classical_v0.2.md`
4. `ARQ_Failure_Modes_and_Safe_Degradation_v0.2.md`
5. `ARQ_Test_Audit_and_Conformance_Matrix_v0.2.md`

---

## 4. How this supplement fits the wider stack

### ARQ depends on
- `c = a + b` for accountable entity coupling;
- SER for long-lived sovereignty and responsibility;
- L4 for reality-bound limits;
- L4 Witness for replayable and challengeable evidence.

### ARQ interacts with
- Beacon for continuity signals and inter-entity recognition;
- VXCX for bounded visual-source deviations;
- federation-layer protocols only indirectly, through witness-backed, bounded outputs rather than self-issued authority.

### ARQ does not redefine
- ontology,
- legal responsibility,
- authority issuance,
- provider identity,
- or public evidence standards.

---

## 5. Integrity and publication

### 5.1 Integrity
This release layer assumes a simple rule:

> Normative text is not enough. Every release artifact should be paired with a reproducible integrity manifest.

Use:

- `SHA256SUMS_ARQ_Supplement_v0.2.txt`

for release verification. The manifest validates the package payload set while remaining self-excluded from that set.

### 5.2 Publication targets
This package is prepared for:

- GitHub repository publication,
- Zenodo archival deposit,
- PDF conversion if needed later,
- and cross-repository linking from the broader AGI / SER / L4 corpus.

### 5.3 Versioning note
ARQ v0.2 is a **supplement package**, not a replacement ontology.

The parent stack remains:

- AGI (Advanced Global Intelligence) as architectural context,
- SER as normative entity stability core,
- L4 as reality-bound discipline.

ARQ remains a specialized protocol layer inside that stack.

---

## 6. Design stance

ARQ is built around a hard distinction:

- informative deviation is common;
- authoritative deviation is rare.

That distinction matters because long-lived systems do not fail only by ignorance.
They also fail by **self-mythologizing noise**.

The package therefore insists on:

- declared boundaries,
- signed records,
- explicit budgets,
- review windows,
- promotion discipline,
- and fail-closed degradation.

If that makes ARQ less romantic, good.
The point is endurance, not mythology.

---

## 7. Release checklist

Before publication, verify:

- all files listed in `DOC_MAP_ARQ_Supplement_v0.2.md` exist;
- `SHA256SUMS_ARQ_Supplement_v0.2.txt` matches the release set;
- `CHANGELOG_ARQ_Supplement_v0.2.md` reflects the actual delta from ARQ v0.1;
- `ZENODO_METADATA_ARQ_Supplement_v0.2.md` has no placeholder fields left unresolved;
- repository cross-links to AGI / SER / L4 are correct.

---

## 8. Closing note

The supplement is intentionally boring in the best sense.

It exists so that ARQ can be:

- read,
- checked,
- hashed,
- cited,
- challenged,
- and implemented

without relying on oral explanation.

That is what a real protocol package should do.

---

## Bridges (required)

**Explicit bridge:** ARQ takes the entity from `c = a + b`, the continuity discipline from SER, the hard ceilings from L4, the replay spine from L4 Witness, and then supplies the missing rule for how deviation becomes either suppression, log-only residue, or reviewable memory.

**Hidden bridge #1 (Ashby / regulator variety):** a long-lived entity can drift through many channels at once. The package therefore spreads control across models, schemas, trust, proofs, degradation, and conformance rather than pretending one document can regulate the whole organism.

**Hidden bridge #2 (information theory / integrity bandwidth):** repository publication is part of protocol discipline. Hash manifests, bounded schemas, and doc maps reduce ambiguity by transmitting structure rather than prose alone.

---

## Earth paragraph

Think of this package like a flight manual plus maintenance book for a temperamental but valuable machine. The machine may be clever, but what matters at release time is whether a second person can identify the parts, verify the log, follow the reading order, and tell which disturbance became a signed maintenance event rather than folklore. That is why this README exists.
