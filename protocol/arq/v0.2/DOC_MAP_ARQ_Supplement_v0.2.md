# ARQ v0.2 Supplement — DOC MAP
## Canonical reading order and dependency map

**Status:** Draft / document map  
**Version:** 0.2-draft  
**Scope:** Reading paths for ARQ v0.2 supplement package  
**Author:** Ivan Kotov  
**Place / year:** Bruxelles, 2026

---

## 0. Start here

ARQ v0.2 is not one paper.
It is a **disciplined package**.

Different readers should enter through different doors.

This map provides:

- fast reading tracks,
- canonical dependency order,
- minimal paths by audience,
- and “read before / read after” guidance.

All substantive ARQ documents in this package ship as same-name `.md` and `.pdf` companions.
The tracks below name the Markdown artifact as the canonical reading surface.

---

## 1. Reading tracks

### Track A — Executive / fast orientation
For readers who want the shortest possible reliable overview.

1. `ARQ_v0.2_One_Page_Essence_EN.md`
2. `ARQ_v0.2_Executive_Summary.md`
3. `README_ARQ_Supplement_v0.2.md`
4. `ARQ_v0.2_Normative_Core.md`
5. `CHANGELOG_ARQ_Supplement_v0.2.md`

Use this track if you need to know:

- what changed,
- what ARQ is,
- and whether the package is worth deeper reading.

---

### Track B — Normative protocol reader
For readers who care about protocol structure and operational rules.

1. `ARQ_v0.2_Normative_Core.md`
2. `ARQ_System_Models_and_Assumptions_v0.2.md`
3. `ARQ_Notation_and_Sign_Conventions_v0.2.md`
4. `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.md`
5. `ARQ_EA_Lifecycle_and_Witness_Binding_v0.2.md`
6. `ARQ_Capsule_and_Witness_Record_Schemas_v0.2.md`
7. `ARQ_Test_Audit_and_Conformance_Matrix_v0.2.md`

Use this track if you want the actual protocol logic.

---

### Track C — Proof / theorem reader
For readers who care about what is actually proven and under which assumptions.

1. `ARQ_System_Models_and_Assumptions_v0.2.md`
2. `ARQ_Notation_and_Sign_Conventions_v0.2.md`
3. `ARQ_Classical_Boundedness_Theorem_v0.2.md`
4. `ARQ_Classical_Boundedness_Theorem_prouve_v0.2.md`
5. `ARQ_Quantum_Boundary_Theorem_v0.2.md`
6. `ARQ_Quantum_Boundary_Theorem_prouve_v0.2.md`

Use this track if you want the cleanest answer to:

- what is bounded,
- in which model,
- and what is **not** claimed.

---

### Track D — Implementation / engineering reader
For readers who need data models, profiles, and degradation rules.

1. `ARQ_v0.2_Normative_Core.md`
2. `ARQ_Capsule_and_Witness_Record_Schemas_v0.2.md`
3. `ARQ_Implementation_Profiles_Classical_v0.2.md`
4. `ARQ_Failure_Modes_and_Safe_Degradation_v0.2.md`
5. `ARQ_Test_Audit_and_Conformance_Matrix_v0.2.md`
6. `SHA256SUMS_ARQ_Supplement_v0.2.txt`

Use this track if you want to build, test, or review an implementation.

---

### Track E — Integration / corpus reader
For readers who need to know where ARQ belongs in the larger stack.

1. `ARQ_v0.2_Normative_Core.md`
2. `ARQ_Integration_Map_to_SER_L4_Witness_Beacon_VXCX_v0.2.md`
3. `ZENODO_METADATA_ARQ_Supplement_v0.2.md`
4. `CHANGELOG_ARQ_Supplement_v0.2.md`

Use this track if your question is not “how does ARQ work?” but “where does ARQ stop and where do other protocols begin?”

---

## 2. Canonical dependency order

If the whole package is read linearly, the canonical order is:

1. `ARQ_v0.2_One_Page_Essence_EN.md`
2. `ARQ_v0.2_Executive_Summary.md`
3. `README_ARQ_Supplement_v0.2.md`
4. `ARQ_v0.2_Normative_Core.md`
5. `ARQ_System_Models_and_Assumptions_v0.2.md`
6. `ARQ_Notation_and_Sign_Conventions_v0.2.md`
7. `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.md`
8. `ARQ_EA_Lifecycle_and_Witness_Binding_v0.2.md`
9. `ARQ_Classical_Boundedness_Theorem_v0.2.md`
10. `ARQ_Classical_Boundedness_Theorem_prouve_v0.2.md`
11. `ARQ_Quantum_Boundary_Theorem_v0.2.md`
12. `ARQ_Quantum_Boundary_Theorem_prouve_v0.2.md`
13. `ARQ_Capsule_and_Witness_Record_Schemas_v0.2.md`
14. `ARQ_Implementation_Profiles_Classical_v0.2.md`
15. `ARQ_Failure_Modes_and_Safe_Degradation_v0.2.md`
16. `ARQ_Integration_Map_to_SER_L4_Witness_Beacon_VXCX_v0.2.md`
17. `ARQ_Test_Audit_and_Conformance_Matrix_v0.2.md`
18. `CHANGELOG_ARQ_Supplement_v0.2.md`
19. `ZENODO_METADATA_ARQ_Supplement_v0.2.md`
20. `SHA256SUMS_ARQ_Supplement_v0.2.txt`

---

## 3. Read-before / read-after table

| Document | Read before | Read after |
|---|---|---|
| `ARQ_v0.2_Normative_Core.md` | Everything except One-Page Essence / Executive / README | System models, valuation, lifecycle |
| `ARQ_System_Models_and_Assumptions_v0.2.md` | Boundedness theorems, implementation arguments | Core |
| `ARQ_Notation_and_Sign_Conventions_v0.2.md` | Valuation, theorem docs | System models |
| `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.md` | Lifecycle, some implementation choices | Notation |
| `ARQ_EA_Lifecycle_and_Witness_Binding_v0.2.md` | Schemas, promotion audit logic | Valuation |
| `ARQ_Classical_Boundedness_Theorem_v0.2.md` | Proof companion | Models + notation |
| `ARQ_Quantum_Boundary_Theorem_v0.2.md` | Quantum proof companion | Models + notation |
| `ARQ_Capsule_and_Witness_Record_Schemas_v0.2.md` | Implementation profiles, conformance matrix | Lifecycle |
| `ARQ_Implementation_Profiles_Classical_v0.2.md` | Failure/degradation, conformance | Schemas |
| `ARQ_Failure_Modes_and_Safe_Degradation_v0.2.md` | Conformance matrix | Profiles + lifecycle + valuation |
| `ARQ_Integration_Map_to_SER_L4_Witness_Beacon_VXCX_v0.2.md` | Release and corpus linking | Core |
| `ARQ_Test_Audit_and_Conformance_Matrix_v0.2.md` | Release gate, audit review | Schemas + profiles + failure |

---

## 4. Minimum document sets by audience

### Auditor minimum set
- `ARQ_v0.2_One_Page_Essence_EN.md`
- `ARQ_v0.2_Executive_Summary.md`
- `ARQ_v0.2_Normative_Core.md`
- `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.md`
- `ARQ_EA_Lifecycle_and_Witness_Binding_v0.2.md`
- `ARQ_Test_Audit_and_Conformance_Matrix_v0.2.md`
- `SHA256SUMS_ARQ_Supplement_v0.2.txt`

### Theorem reviewer minimum set
- `ARQ_System_Models_and_Assumptions_v0.2.md`
- `ARQ_Notation_and_Sign_Conventions_v0.2.md`
- `ARQ_Classical_Boundedness_Theorem_v0.2.md`
- `ARQ_Classical_Boundedness_Theorem_prouve_v0.2.md`
- `ARQ_Quantum_Boundary_Theorem_v0.2.md`
- `ARQ_Quantum_Boundary_Theorem_prouve_v0.2.md`

### Repository maintainer minimum set
- `README_ARQ_Supplement_v0.2.md`
- `DOC_MAP_ARQ_Supplement_v0.2.md`
- `CHANGELOG_ARQ_Supplement_v0.2.md`
- `SHA256SUMS_ARQ_Supplement_v0.2.txt`
- `ZENODO_METADATA_ARQ_Supplement_v0.2.md`

### Implementer minimum set
- `ARQ_v0.2_Normative_Core.md`
- `ARQ_Capsule_and_Witness_Record_Schemas_v0.2.md`
- `ARQ_Implementation_Profiles_Classical_v0.2.md`
- `ARQ_Failure_Modes_and_Safe_Degradation_v0.2.md`
- `ARQ_Test_Audit_and_Conformance_Matrix_v0.2.md`

---

## 5. What not to do

Do **not** start with proof notes if you have not read the system models.

Do **not** start with implementation profiles if you have not read the normative core.

Do **not** treat integration-map text as a substitute for the protocol itself.

Do **not** use the changelog as your primary technical source.

Do **not** read only the valuation document and assume you understand promotion. Promotion lives across valuation, trust, lifecycle, and schemas.

---

## 6. Release discipline

Before publishing or citing the package:

1. verify file presence against this map;
2. verify hashes against `SHA256SUMS_ARQ_Supplement_v0.2.txt`;
3. verify metadata fields in `ZENODO_METADATA_ARQ_Supplement_v0.2.md`;
4. verify that changelog claims match actual files;
5. verify repository entrypoint links.

---

## 7. Closing note

A protocol package becomes unreadable the moment every reader has to invent their own path through it.

This map exists to prevent that.

---

## Bridges (required)

**Explicit bridge:** the DOC MAP ties the ARQ supplement to the same architectural discipline as the wider AGI / SER / L4 corpus: one entry layer, multiple reading tracks, one stable path from overview to normativity to proof to audit.

**Hidden bridge #1 (Ashby / control of complexity):** the package is too diverse for one flat reading order. Multiple tracks are not a convenience feature; they are the requisite variety needed so different reviewers do not misread the same corpus for different reasons.

**Hidden bridge #2 (information theory / routing of trust):** document order is part of integrity. Bad reading order injects ambiguity and false inference just like a noisy channel injects decoding error.

---

## Earth paragraph

On a workbench, parts laid out in the wrong order make even a good machine look broken. A wiring harness before the chassis, a test report before the board, a proof before the model — and suddenly the reader thinks the system is chaos. This map is the bench layout for ARQ v0.2.
