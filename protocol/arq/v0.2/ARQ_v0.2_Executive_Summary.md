# ARQ v0.2 — Executive Summary
## Anti-Resonance Correction Protocol Supplement

**Status:** Draft / Executive release summary  
**Version:** 0.2-draft  
**Scope:** Release summary for the ARQ v0.2 supplement package  
**Parent corpus:** AGI / SER / L4 / L4 Witness / Beacon / VXCX  
**Author:** Ivan Kotov  
**Place / year:** Bruxelles, 2026

---

## 0. What this package is

ARQ v0.2 is a supplement package that turns ARQ from a promising technical idea into a more disciplined, reviewable, and publishable protocol set.

The package does **not** replace the existing ARQ concept. It does something more practical:

- separates normative core from proof notes and implementation notes;
- declares explicit system models before making boundedness claims;
- unifies notation and sign conventions across classical and quantum branches;
- tightens trust, witness, and promotion logic;
- prevents premature elevation of deviations into authoritative memory;
- closes the gap between protocol language and release-ready documentation.

In plain terms: ARQ v0.2 is the point where the protocol stops being only a compelling architecture note and becomes a package that can survive technical reading, audit-style reading, and repository publication.

---

## 1. Problem addressed

ARQ v0.1 introduced the right architectural instinct:

> not every deviation is pure loss, but no deviation should gain authority without bounded review.

That core instinct remains intact.

The problems in v0.1 were structural rather than conceptual:

- mathematical claims were stronger than the explicitly declared models beneath them;
- classical and quantum bounds were mixed too casually;
- sign conventions around entropy and value were not stable enough across documents;
- “anomaly prior” mixed heuristic scoring and probability language;
- Experience Artifact promotion could still look too early or too smooth;
- release-layer material for GitHub / Zenodo was missing.

The v0.2 supplement package exists to close those holes without bloating the corpus into an unreadable paper maze.

---

## 2. Core additions in v0.2

The package introduces the following high-value additions:

### 2.1 Normative separation
ARQ now has a clear **Normative Core** and a set of companion documents for:

- system models,
- notation,
- valuation and anomaly scoring,
- trust and provenance,
- EA lifecycle and witness binding,
- classical boundedness theorem,
- quantum boundary theorem,
- schemas,
- implementation profiles,
- failure and degradation,
- integration map,
- conformance matrix.

### 2.2 Explicit model discipline
System models are declared before inference.

ARQ v0.2 distinguishes at least:

- a classical persistent-state model,
- a commit-metered retention model,
- an epoch-gated trust/control model,
- an online queue/backlog model,
- a fixed trusted quantum boundary model.

This prevents one theorem from pretending to cover every physical or software case at once.

### 2.3 Corrected boundedness logic
The classical boundedness branch is now framed around:

- finite authoritative persistent state,
- bounded retained commits,
- bounded pending queue,
- fail-closed epoch logic.

The quantum branch is separated into its own theorem:

- internal entropy and usable entanglement are bounded by the dimension of the declared trusted quantum boundary.

### 2.4 Stricter memory promotion
A deviation no longer jumps too easily from “interesting” to “authoritative.”

ARQ v0.2 introduces a staged lifecycle:

`detected -> classified -> observed -> candidate_artifact -> provisional_artifact -> confirmed_EA`

with explicit terminating paths such as:

`suppressed`, `log_only`, `rejected`, `fail_closed`.

### 2.5 Trust-first valuation
Value is no longer allowed to float free of witness and attestation.

ARQ v0.2 makes explicit that:

- raw value is not enough;
- trust-adjusted value governs authority-sensitive decisions;
- promotion requires witness sufficiency, trust validity, review survival, and privilege legitimacy;
- anti-echo quarantine and A/B-slot rollback prevent self-reinforcing narrative drift.

---

## 3. Main normative stance

ARQ v0.2 can be summarized in one line:

> A deviation may be informative before it is authoritative, but it may not become authoritative without witness, bounded review, and declared boundary discipline.

This is the heart of the package.

ARQ therefore treats correction, classification, witness, promotion, and degradation as one control problem.

It is not a creativity cult.
It is not a retry loop.
It is not a reward function.

It is a bounded protocol for handling deviation in a persistent entity that claims memory, continuity, and auditability.

---

## 4. Relationship to the wider corpus

ARQ v0.2 does not stand alone.

It sits inside the broader stack as follows:

- **`c = a + b`** provides the ontological coupling of accountable anchor and procedures.
- **SER** provides persistence, liability, and long-horizon entity stability.
- **L4** provides the non-negotiable reality boundary: energy, time, irreversibility, scarcity, trust collapse.
- **L4 Witness** provides replayable, challengeable evidence discipline.
- **Beacon** governs inter-entity recognition and continuity signals.
- **VXCX** provides bounded visual experience exchange without breaking privacy discipline.

ARQ is therefore not “another entity theory.”
It is the protocol layer that governs how deviation is processed inside such an entity stack.

---

## 5. What changed from v0.1

The most important changes are:

1. **Core and companions are separated.**  
   Normative text is no longer overloaded with all mathematics and implementation details.

2. **System models are declared first.**  
   No more universal-looking claims without explicit assumptions.

3. **Notation is stabilized.**  
   Exploration, ordering, entropy, trust-adjusted value, and anomaly scoring are separated cleanly.

4. **Classical boundedness is corrected.**  
   Memory, retention, queue, and energy-related claims are no longer mixed casually.

5. **Quantum boundedness is separated.**  
   Finite trusted-boundary dimension now carries the quantum bound.

6. **EA promotion is delayed and staged.**  
   Candidate does not silently masquerade as confirmed experience.

7. **Trust logic is hardened.**  
   Promotion authority requires more than a high score.

8. **Failure and degradation are first-class.**  
   The package specifies how ARQ behaves when assumptions crack.

9. **Release layer is added.**  
   The package can now be published, mapped, hashed, and cited coherently.

---

## 6. Reading guidance

### If you want the shortest useful path
Read in this order:

1. `ARQ_v0.2_Normative_Core.md`
2. `ARQ_System_Models_and_Assumptions_v0.2.md`
3. `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.md`
4. `ARQ_Trust_and_Provenance_Profile_v0.2.md`
5. `ARQ_EA_Lifecycle_and_Witness_Binding_v0.2.md`
6. `ARQ_Classical_Boundedness_Theorem_v0.2.md`
7. `ARQ_Quantum_Boundary_Theorem_v0.2.md`
8. `ARQ_Test_Audit_and_Conformance_Matrix_v0.2.md`

### If you are reading for implementation
Add:

- `ARQ_Capsule_and_Witness_Record_Schemas_v0.2.md`
- `ARQ_Implementation_Profiles_Classical_v0.2.md`
- `ARQ_Failure_Modes_and_Safe_Degradation_v0.2.md`

### If you are reading for corpus integration
Add:

- `ARQ_Integration_Map_to_SER_L4_Witness_Beacon_VXCX_v0.2.md`

---

## 7. Release note

This supplement package is intended to be published as:

- a GitHub supplement layer to ARQ,
- and a Zenodo-archived release package.

The package is organized so that:

- the **Normative Core** remains stable and readable,
- proofs can evolve with tighter formalization,
- schemas and profiles can be implemented independently,
- the release can be hashed and cited as a coherent artifact set.

---

## 8. Closing statement

ARQ v0.2 does not claim to solve intelligence.
It claims something narrower and more defensible:

> a persistent entity should be able to meet deviation without either collapsing into chaos or mythologizing every disturbance as growth.

That is the protocol’s actual ambition.

Bound deviation.  
Witness it.  
Review it.  
Retain only what earns retention.

---

## Bridges (required)

**Explicit bridge:** `c = a + b` gives ARQ its accountable subject, SER gives it persistence, L4 gives it real-world ceilings, and L4 Witness gives it replayable evidence. ARQ v0.2 is the supplement that turns those layers into a disciplined deviation-handling stack rather than parallel ideas.

**Hidden bridge #1 (Ashby / cybernetics):** stability cannot be maintained by one knob. ARQ therefore distributes regulation across encoding, active correction, review, trust, degradation, and witness. Variety in the controlled system requires variety in the regulator.

**Hidden bridge #2 (Cover & Thomas / channel discipline):** the package reduces ambiguity by forcing deviation through bounded record formats, bounded review states, and bounded authority transitions. Trust bandwidth is compressed into structured records instead of narrative claims.

---

## Earth paragraph

In engineering terms, v0.2 is the difference between a good control idea on a whiteboard and a machine you would actually sign off for extended operation. The question is not whether a system can be surprised. It will be. The question is whether surprise turns into heat, backlog, myth, or a signed artifact that survived replay and review. ARQ v0.2 is built for the fourth case.
