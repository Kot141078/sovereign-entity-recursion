# INDEX — Arbitration / Review Layer v0.1
## ARL Package Map

**Status:** Draft package map v0.1  
**Canonical home:** `sovereign-entity-recursion`  
**Author:** Ivan Kotov  
**Location:** Brussels  
**Year:** 2026

---

## Purpose

This index defines the internal map, reading path, and document roles for the Arbitration / Review Layer package.

ARL v0.1 should be read as a bounded procedural stack for dispute admission, freeze discipline, review, outcome issuance, and witness-bound traceability.

---

## Primary documents

### 1. `Executive_Summary_Arbitration_Review_Layer_v0.1.md`
**Role:** One-page entry for fast readers, auditors, public framing, and external triage.

### 2. `Multi_Entity_Arbitration_Review_Layer_v0.1.md`
**Role:** Normative core of the package.

This is the primary document defining:
- purpose,
- scope,
- actors,
- standing,
- admissibility,
- judge limits,
- outcomes,
- appeal,
- witness binding,
- fail-closed rules.

---

## Supporting documents

### 3. `Evidence_Admissibility_and_Standing_v0.1.md`
**Role:** Standing classes, admissibility rules, provenance discipline, burden of proof, and invalid evidence classes.

### 4. `Normative_Terms_and_Definitions_ARL_v0.1.md`
**Role:** Canonical terminology lock for the ARL package.

### 5. `Freeze_Hold_Quarantine_Semantics_v0.1.md`
**Role:** Operational state changes under dispute: pre-admissibility hold, evidentiary freeze, privilege freeze, branch quarantine, re-entry prohibition, and release conditions.

### 6. `Decision_Outcomes_and_Appeal_Window_v0.1.md`
**Role:** Allowed outcomes, appeal triggers, appeal standing, deadlines, reopening thresholds, and no-infinite-retry discipline.

### 7. `Conflict_Class_Taxonomy_v0.1.md`
**Role:** Formal taxonomy of dispute classes so arbitration does not collapse into unbounded “general disagreement.”

### 8. `README.md`
**Role:** Package front door and orientation note.

### 9. `DOC_MAP.md`
**Role:** Canonical document-role map for the package-facing layer.

---

## Recommended reading order

### Fast path
1. `Executive_Summary_Arbitration_Review_Layer_v0.1.md`
2. `Multi_Entity_Arbitration_Review_Layer_v0.1.md`

### Full path
1. `README.md`
2. `Executive_Summary_Arbitration_Review_Layer_v0.1.md`
3. `Multi_Entity_Arbitration_Review_Layer_v0.1.md`
4. `Normative_Terms_and_Definitions_ARL_v0.1.md`
5. `Evidence_Admissibility_and_Standing_v0.1.md`
6. `Freeze_Hold_Quarantine_Semantics_v0.1.md`
7. `Decision_Outcomes_and_Appeal_Window_v0.1.md`
8. `Conflict_Class_Taxonomy_v0.1.md`
9. `DOC_MAP.md`

---

## Normative center vs support layers

### Normative center
- `Multi_Entity_Arbitration_Review_Layer_v0.1.md`

### Interpretive / support layers
- `Executive_Summary_Arbitration_Review_Layer_v0.1.md`
- `Normative_Terms_and_Definitions_ARL_v0.1.md`
- `Evidence_Admissibility_and_Standing_v0.1.md`
- `Freeze_Hold_Quarantine_Semantics_v0.1.md`
- `Decision_Outcomes_and_Appeal_Window_v0.1.md`
- `Conflict_Class_Taxonomy_v0.1.md`
- `README.md`
- `DOC_MAP.md`

If interpretation conflicts with the normative core, the normative core prevails.

---

## Canonical package logic

ARL v0.1 answers one bounded question:

> How are multi-entity disputes admitted, frozen, reviewed, and resolved without destroying continuity, laundering confidence, or allowing unlawful re-entry into the active system flow?

The package is intentionally narrow.
It does not attempt to solve the total ecosystem.
It defines the dispute discipline required for the ecosystem not to rot under conflict.

---

## Bridges

**Explicit bridge:**  
`SER continuity ↔ L4 witness / freeze ↔ Arbitration / Review Layer`

**Hidden bridge #1:**  
DEA / EA standing enters as procedural relevance, without duplicating the full standing corpus.

**Hidden bridge #2:**  
SER-FED anti-capture logic constrains ARL so that Judge scope remains bounded and cannot solidify into quiet permanent authority.

---

## Earth paragraph

A dispute system is not a philosopher’s stage. It is closer to a sealed loading dock. Once manifests conflict, the cargo stops moving, access narrows, signatures are checked, and re-entry is not granted because someone sounds confident. It is granted only when the chain holds.
