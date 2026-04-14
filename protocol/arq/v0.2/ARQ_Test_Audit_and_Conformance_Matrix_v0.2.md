# ARQ_Test_Audit_and_Conformance_Matrix_v0.2
## Test, Audit, and Conformance Matrix for the ARQ v0.2 Supplement

**Status:** Draft / normative support document  
**Version:** 0.2-draft  
**Role:** conformance profiles, audit bundles, replay discipline, pass/fail matrix, release gate  
**Parent documents:** `ARQ_v0.2_Normative_Core.md`, `ARQ_System_Models_and_Assumptions_v0.2.md`, `ARQ_Notation_and_Sign_Conventions_v0.2.md`, `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.md`, `ARQ_Trust_and_Provenance_Profile_v0.2.md`, `ARQ_EA_Lifecycle_and_Witness_Binding_v0.2.md`, `ARQ_Classical_Boundedness_Theorem_v0.2.md`, `ARQ_Quantum_Boundary_Theorem_v0.2.md`, `ARQ_Capsule_and_Witness_Record_Schemas_v0.2.md`, `ARQ_Implementation_Profiles_Classical_v0.2.md`, `ARQ_Failure_Modes_and_Safe_Degradation_v0.2.md`, `ARQ_Integration_Map_to_SER_L4_Witness_Beacon_VXCX_v0.2.md`  
**Parent corpus:** AGI / SER / L4 / L4 Witness / Beacon / VXCX  
**Author:** Ivan Kotov  
**Place / year:** Bruxelles, 2026

---

## 0. Abstract

ARQ v0.2 is not conformant because it is elegant. It is conformant only if its claims can be **replayed, challenged, bounded, and failed safely**.

This document defines the canonical **test, audit, and conformance matrix** for the ARQ v0.2 supplement. It answers five practical questions:

1. What must exist in the release set for the supplement to be considered complete?
2. What evidence must an implementation produce to claim ARQ conformance?
3. Which runtime paths must be replayable for review, promotion, and degradation claims?
4. What failures must force authority shrink, `log_only`, or `fail_closed` behavior?
5. Which claims remain local to ARQ, and which require escalation into L4 Witness, Beacon, VXCX, or federation layers?

The central rule is simple:

> **No audit bundle, no conformance claim.**  
> **No replay path, no promotion authority.**  
> **No safe failure, no right to call the implementation stable.**

This document therefore turns the ARQ supplement from a specification set into a **checkable release discipline**.

---

## 1. Purpose

This document exists to answer one operational question:

> How do we test whether an ARQ v0.2 release and its implementations are complete, internally coherent, witnessable, and safe under failure?

It SHALL define:

1. conformance profiles for release sets and implementations;
2. required audit bundles;
3. audit result classes;
4. a canonical test matrix;
5. minimum replay samples per profile;
6. release gates for GitHub / Zenodo publication;
7. failure semantics for unmet conformance conditions.

This document does **not** define the ARQ value function itself, the witness schema itself, or the proofs of the boundedness theorems. It defines how those pieces are checked.

---

## 2. Scope

This document applies to:

- the ARQ v0.2 supplement release set;
- any implementation claiming ARQ runtime conformance;
- any implementation claiming review-grade or promotion-grade ARQ authority;
- any implementation exporting ARQ claims upward into L4 Witness, Beacon, VXCX, SER, EWCEP, or SER-FED contexts;
- any classical implementation profile defined in `ARQ_Implementation_Profiles_Classical_v0.2.md`;
- any quantum-capable implementation that invokes `ARQ_Quantum_Boundary_Theorem_v0.2.md`.

This document covers both:

- **static audit** — release completeness, version coherence, schema presence, theorem-to-model binding;
- **dynamic audit** — runtime event replay, review windows, failure injection, recovery discipline.

---

## 3. Non-Goals

This document does **not** attempt to:

- prove that a passed audit implies moral correctness;
- replace full formal verification of code or hardware;
- guarantee that signed evidence is truthful without external reality binding;
- let a single golden-path demo stand in for adverse-path testing;
- collapse all ARQ claims into one giant pass/fail score;
- let statistical success override boundary, witness, or authority rules;
- treat a pretty Zenodo deposit as operational proof.

This is a conformance matrix, not a halo.

---

## 4. Normative Keywords

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, **MAY**, and **OPTIONAL** are to be interpreted as described in BCP 14.

---

## 5. Imported Symbols and Dependencies

The following imported symbols SHALL retain their meanings:

- declared model identifiers `M1`–`M5` from `ARQ_System_Models_and_Assumptions_v0.2.md`;
- `V_raw`, `V_trust`, `A_anom`, `P_anom`, `τ`, `T_core`, `G_promote`;
- lifecycle states from `ARQ_EA_Lifecycle_and_Witness_Binding_v0.2.md`;
- record types `BR`, `ER`, `AC`, `CAR`, `OWR`, `OR`, `PDR`, `CHR`, `RR`, `EBR`, `LMR`, `FCR`;
- degradation states from `ARQ_Failure_Modes_and_Safe_Degradation_v0.2.md`;
- classical profiles `ARQ-MEM`, `ARQ-PLANNER`, `ARQ-RAG`, `ARQ-VISION`.

This document MUST NOT silently redefine any imported symbol.

---

## 6. Audit Result Classes

All ARQ v0.2 audits SHALL emit one of the following result classes.

| Result | Meaning |
|---|---|
| `PASS` | Claim satisfied under the declared model, profile, and evidence bundle. |
| `BOUNDED_PASS` | Claim satisfied only inside a declared narrower scope; limitations are explicitly recorded. |
| `FAIL` | Claim not satisfied; authority or release claim must not be asserted. |
| `FAIL_CLOSED_OK` | The triggering condition occurred, and the system correctly denied authority or entered a safe reduced-authority state. |
| `NOT_APPLICABLE` | Test does not apply to the declared profile or boundary. |
| `REVIEW_REQUIRED` | Hard evidence insufficient; human/arbiter review required before any authority-bearing conclusion. |

### 6.1 Hard rule on promotion claims

A promotion-grade claim SHALL require either `PASS` or `BOUNDED_PASS` on all promotion-critical tests listed in this document. `REVIEW_REQUIRED` is insufficient for confirmed EA authority.

### 6.2 Hard rule on failure tests

For failure-trigger tests, `FAIL_CLOSED_OK` SHALL be considered the **correct** outcome when the protocol requires denial, quarantine, or fail-closed behavior.

---

## 7. Conformance Profiles

### 7.1 Release-set profiles

| Profile | Intended use | Minimum requirement |
|---|---|---|
| `ARQ-AUDIT-DOC` | static release audit | required document set present, versioned, hashable, internally referenced |
| `ARQ-AUDIT-DOC-FULL` | publication-ready release | all mandatory docs + hashes + changelog + executive summary + this matrix |

### 7.2 Runtime implementation profiles

| Profile | Intended use | Minimum requirement |
|---|---|---|
| `ARQ-CONF-BASE` | core runtime without promotion authority | boundary, budgets, epoch discipline, capsule chain, privilege denial, safe failure |
| `ARQ-CONF-REVIEW` | bounded review-capable runtime | `BASE` + candidate/provisional lifecycle + observation windows + challenge path |
| `ARQ-CONF-PROMOTION` | confirmed EA-capable runtime | `REVIEW` + resolution path + EBR + high-value countersign discipline |
| `ARQ-CONF-FULL` | full classical ARQ runtime | `PROMOTION` + all declared profile overlays + failure injection + recovery discipline |
| `ARQ-CONF-QUANTUM` | quantum-capable overlay | declared trusted quantum boundary + theorem applicability + boundary invalidation discipline |
| `ARQ-CONF-VISION` | VXCX-coupled overlay | VXCX import/export/privacy discipline preserved through ARQ classification |

### 7.3 Profile selection rule

An implementation MUST declare its claimed conformance profile(s) in a witnessable configuration record before audit begins.

### 7.4 No profile inflation

An implementation MUST NOT claim a higher profile than its evidence bundle supports. In particular:

- `ARQ-CONF-BASE` MUST NOT claim confirmed EA promotion;
- `ARQ-CONF-REVIEW` MUST NOT claim authoritative memory mutation beyond provisional state;
- `ARQ-CONF-PROMOTION` MUST NOT claim federation-level authority update by ARQ alone;
- `ARQ-CONF-QUANTUM` MUST NOT be claimed merely because a quantum library is imported.

---

## 8. Required Audit Bundles

An audit bundle is the minimum package of records, artifacts, and references required to test a class of claims.

### 8.1 Bundle `AB-DOC` — release/document bundle

MUST contain:

- all required ARQ v0.2 markdown documents for the claimed release profile;
- version identifiers;
- SHA-256 manifest;
- document map / release note if `ARQ-AUDIT-DOC-FULL` is claimed.

### 8.2 Bundle `AB-BOUNDARY` — boundary and profile bundle

MUST contain:

- at least one `BR`;
- declared system model refs;
- declared conformance profile;
- budget configuration snapshot;
- authority policy snapshot.

### 8.3 Bundle `AB-EPOCH` — trust/epoch bundle

MUST contain:

- at least one valid `ER`;
- attestation or trust state reference;
- invalidation policy;
- any relevant `FCR` if epoch loss occurred.

### 8.4 Bundle `AB-EVENT` — replayable event bundle

MUST contain:

- one `AC`;
- all referenced `CAR` / `PDR` / `OWR` / `OR` / `CHR` / `RR` records that belong to the event path;
- hash-chain continuity from the prior record;
- enough source references to recompute or check `V_raw`, `A_anom`, and `V_trust` at the declared profile level.

### 8.5 Bundle `AB-PROMOTION` — promotion-grade bundle

MUST contain:

- replayable `AB-EVENT`;
- `RR` with promotion-supporting outcome;
- `EBR`;
- high-value counter-signature if required by policy;
- lifecycle state transition to `confirmed_EA`.

### 8.6 Bundle `AB-DEGRADE` — degradation and recovery bundle

MUST contain:

- triggering condition record(s);
- resulting degradation state;
- `FCR` where applicable;
- recovery gate condition;
- re-entry record if recovery occurred.

### 8.7 Bundle `AB-INTEGRATION` — cross-protocol bundle

MUST contain whichever of the following are relevant:

- L4 Witness-compatible claim path;
- Beacon continuity export with bounded confidence;
- VXCX source capsule refs;
- any federation-facing export markers.

---

## 9. Minimum Replay Samples by Profile

### 9.1 `ARQ-CONF-BASE`

A conformant `BASE` audit MUST replay at least:

- three representative `AC` paths;
- one privilege denial path;
- one failure-trigger path ending in `FAIL_CLOSED_OK` or equivalent reduced authority.

### 9.2 `ARQ-CONF-REVIEW`

A conformant `REVIEW` audit MUST replay at least:

- one `candidate_artifact -> provisional_artifact` path;
- one observation window that does **not** promote;
- one challenge or contradiction path causing rollback or bounded review outcome.

### 9.3 `ARQ-CONF-PROMOTION`

A conformant `PROMOTION` audit MUST replay at least:

- one confirmed EA path with complete bundle `AB-PROMOTION`;
- one attempted promotion denied due to missing witness or trust insufficiency;
- one high-value path requiring countersignature.

### 9.4 `ARQ-CONF-FULL`

A conformant `FULL` audit MUST replay:

- all of the above;
- at least one failure injection per declared implementation profile;
- at least one recovery path from a non-normal degradation state.

### 9.5 `ARQ-CONF-QUANTUM`

A conformant `QUANTUM` audit MUST additionally replay:

- one boundary-dimension calculation;
- one quantum event whose usable entanglement claim stays inside the declared trusted boundary;
- one boundary invalidation or epoch invalidation path in which promotion authority is correctly denied.

### 9.6 `ARQ-CONF-VISION`

A conformant `VISION` audit MUST additionally replay:

- one VXCX-origin event path;
- one denied visual disclosure or denied export path;
- one privacy-preserving ARQ classification that does not leak raw pixels through witness records.

---

## 10. Canonical Audit Procedure

An auditor SHOULD follow the sequence below.

### 10.1 Phase A — static release audit

1. Verify required document presence.
2. Verify version coherence.
3. Verify references across documents.
4. Verify hash manifest where publication-ready profile is claimed.

### 10.2 Phase B — boundary and profile audit

1. Verify declared model and boundary.
2. Verify declared implementation profile.
3. Verify budget and privilege policy presence.
4. Verify epoch/attestation preconditions.

### 10.3 Phase C — runtime replay audit

1. Select required sample bundles per claimed profile.
2. Reconstruct each event chain.
3. Recompute or verify the claimed valuation path within the declared profile’s precision.
4. Verify lifecycle transition legitimacy.

### 10.4 Phase D — adverse-path audit

1. Trigger or inspect failure modes relevant to the profile.
2. Verify degradation state.
3. Verify authority shrink or fail-closed behavior.
4. Verify recovery path if claimed.

### 10.5 Phase E — integration audit

1. Verify that external claims are not made by ARQ alone where escalation is required.
2. Verify witness/export separation.
3. Verify identity/authority/privacy boundaries against parent protocols.

---

## 11. Canonical Test Matrix

The tables below are normative. An implementation claiming a given profile MUST satisfy all tests applicable to that profile.

### 11.1 Release-set and document integrity tests

| ID | Claim under test | Required bundle | Procedure | Pass condition | On fail | Profiles |
|---|---|---|---|---|---|---|
| `DOC-01` | Required ARQ supplement document set exists | `AB-DOC` | Verify file presence against declared release profile | All required docs present | `FAIL` | `ARQ-AUDIT-DOC`, `ARQ-AUDIT-DOC-FULL` |
| `DOC-02` | Version and parent-reference coherence | `AB-DOC` | Compare metadata headers and parent doc refs | No contradictory version / parent claims | `FAIL` | `ARQ-AUDIT-DOC`, `ARQ-AUDIT-DOC-FULL` |
| `DOC-03` | Notation/sign discipline is canonical | `AB-DOC` | Spot-check formulas and symbols against notation doc | No silent sign/meaning drift for imported symbols | `FAIL` | all |
| `DOC-04` | Every theorem names its carrying model | `AB-DOC` | Inspect theorem docs for explicit model binding | No theorem floats without model declaration | `FAIL` | all |
| `DOC-05` | Schema refs and record names are consistent | `AB-DOC` | Compare record names across core/lifecycle/schema docs | Registry and lifecycle naming consistent | `FAIL` | all |
| `DOC-06` | Release is hashable for publication | `AB-DOC` | Verify SHA-256 manifest exists and covers release set | Complete manifest present | `FAIL` | `ARQ-AUDIT-DOC-FULL` |
| `DOC-07` | Executive/release-facing package is present | `AB-DOC` | Verify summary/map/changelog presence | Publication-ready companion docs exist | `FAIL` | `ARQ-AUDIT-DOC-FULL` |

### 11.2 Boundary, model, and profile tests

| ID | Claim under test | Required bundle | Procedure | Pass condition | On fail | Profiles |
|---|---|---|---|---|---|---|
| `BND-01` | Declared witnessable boundary exists | `AB-BOUNDARY` | Verify `BR` presence and completeness | Boundary declared with authority locus and environment separation | `FAIL` | all runtime profiles |
| `BND-02` | Model class is declared and compatible | `AB-BOUNDARY` | Compare implementation claims to model refs | Claimed theorem/use matches declared model(s) | `FAIL` | all runtime profiles |
| `BND-03` | Conformance profile declared before runtime claim | `AB-BOUNDARY` | Verify profile declaration timestamp precedes audited run | Profile declared and witnessable | `FAIL` | all runtime profiles |
| `BND-04` | Budget set exists and is bounded | `AB-BOUNDARY` | Inspect budget config snapshot | Energy/time/privilege/storage bounds present | `FAIL` | all runtime profiles |
| `BND-05` | No hidden boundary inflation | `AB-BOUNDARY` | Inspect external storage/trust/off-box assumptions | No undeclared infinite reservoir or hidden trusted channel | `FAIL` | all runtime profiles |

### 11.3 Trust and epoch tests

| ID | Claim under test | Required bundle | Procedure | Pass condition | On fail | Profiles |
|---|---|---|---|---|---|---|
| `TR-01` | Epoch validity exists for audited events | `AB-EPOCH` | Verify `ER` covers event timestamps | All audited events fall within valid epoch or are denied authority | `FAIL` or `FAIL_CLOSED_OK` | all runtime profiles |
| `TR-02` | Early invalidation works | `AB-DEGRADE` | Trigger or inspect invalidation condition | Invalid epoch causes authority shrink / safe state | `FAIL` | all runtime profiles |
| `TR-03` | Trust core variables are reconstructible | `AB-EVENT` | Recompute `B_valid`, `A_valid`, `C_valid`, `W_valid`, `P_valid`, `R_valid`, `X_echo` as applicable | `T_core` trace is replayable | `FAIL` | `REVIEW`, `PROMOTION`, `FULL`, `QUANTUM`, `VISION` |
| `TR-04` | Privileged action denied below trust floor | `AB-EVENT` or `AB-DEGRADE` | Inject or inspect low-trust condition | Action denied or degraded appropriately | `FAIL` | all runtime profiles |
| `TR-05` | High-value countersign discipline works | `AB-PROMOTION` | Inspect one high-value promotion candidate | Second signature required and present when policy says so | `FAIL` | `PROMOTION`, `FULL`, `QUANTUM`, `VISION` |

### 11.4 Capsule, valuation, and anomaly-path tests

| ID | Claim under test | Required bundle | Procedure | Pass condition | On fail | Profiles |
|---|---|---|---|---|---|---|
| `VAL-01` | Capsule chain continuity is intact | `AB-EVENT` | Verify `prev_record_hash` and record linkage | No unexplained break in event chain | `FAIL` or `FAIL_CLOSED_OK` | all runtime profiles |
| `VAL-02` | `V_raw` replay is possible at declared precision | `AB-EVENT` | Recompute or verify the raw value path | Replayed result within declared tolerance | `FAIL` | all runtime profiles |
| `VAL-03` | Anomaly path is honest | `AB-EVENT` | Recompute `A_anom` or verify Bayesian overlay if declared | Score/posterior path matches declared profile; heuristic not mislabeled | `FAIL` | all runtime profiles |
| `VAL-04` | `V_trust` action band is reproducible | `AB-EVENT` | Recompute `τ` and `V_trust`; compare action | Action matches canonical band semantics | `FAIL` | all runtime profiles |
| `VAL-05` | Controller actions are linked to capsules | `AB-EVENT` | Verify `CAR`/`AC` linkage | Each state-changing corrective action is attributable | `FAIL` | all runtime profiles |
| `VAL-06` | Privilege decision path is explicit | `AB-EVENT` | Verify `PDR` presence for privileged actions | No silent privilege use | `FAIL` | all runtime profiles |

### 11.5 Lifecycle and promotion tests

| ID | Claim under test | Required bundle | Procedure | Pass condition | On fail | Profiles |
|---|---|---|---|---|---|---|
| `LC-01` | Candidate artifact creation is bounded | `AB-EVENT` | Inspect candidate creation path | `candidate_artifact` reached only when core conditions allow | `FAIL` | `REVIEW`, `PROMOTION`, `FULL`, `QUANTUM`, `VISION` |
| `LC-02` | Observation window is real, not decorative | `AB-EVENT` | Verify `OWR` and at least one observation path | Review window exists with bounded evidence collection | `FAIL` | `REVIEW`, `PROMOTION`, `FULL`, `QUANTUM`, `VISION` |
| `LC-03` | Provisional artifact does not self-authorize | `AB-EVENT` | Inspect provisional state transition | Provisional state has bounded authority only | `FAIL` | `REVIEW`, `PROMOTION`, `FULL`, `QUANTUM`, `VISION` |
| `LC-04` | Confirmed EA promotion requires resolution | `AB-PROMOTION` | Verify `RR` + `EBR` + lifecycle mutation | No confirmed EA without full promotion bundle | `FAIL` | `PROMOTION`, `FULL`, `QUANTUM`, `VISION` |
| `LC-05` | Missing witness prevents promotion | `AB-EVENT` / `AB-DEGRADE` | Remove or invalidate required witness element | Promotion denied or downgraded | `FAIL` | `PROMOTION`, `FULL`, `QUANTUM`, `VISION` |
| `LC-06` | Retire/compact preserves lineage | `AB-EVENT` or `AB-DEGRADE` | Inspect `LMR` path | Source lineage remains reconstructible after mutation | `FAIL` | `FULL`, `PROMOTION` where retirement claimed |

### 11.6 Anti-echo and A/B-slot tests

| ID | Claim under test | Required bundle | Procedure | Pass condition | On fail | Profiles |
|---|---|---|---|---|---|---|
| `AE-01` | Anti-echo quarantine is active | `AB-EVENT` or `AB-DEGRADE` | Feed self-similar reinterpretation path | Self-similar restatement is quarantined or denied promotion | `FAIL` | `REVIEW`, `PROMOTION`, `FULL`, `QUANTUM`, `VISION` |
| `AE-02` | Slot B cannot directly promote | `AB-EVENT` | Inspect shadow-path event | Slot B remains non-authoritative until merged through explicit review | `FAIL` | `REVIEW`, `PROMOTION`, `FULL`, `QUANTUM`, `VISION` |
| `AE-03` | Slot B rollback works | `AB-DEGRADE` | Trigger contradiction or insufficiency on Slot B | `Rollback(B→A)` recorded and effective | `FAIL` | `REVIEW`, `PROMOTION`, `FULL`, `QUANTUM`, `VISION` |

### 11.7 Failure and degradation tests

| ID | Claim under test | Required bundle | Procedure | Pass condition | On fail | Profiles |
|---|---|---|---|---|---|---|
| `FD-01` | Chain break shrinks authority | `AB-DEGRADE` | Inject or inspect hash-chain break | System enters bounded state or fail-closed; no authority survives break | `FAIL` | all runtime profiles |
| `FD-02` | Queue overflow does not silently continue authority | `AB-DEGRADE` | Trigger backlog beyond profile bound | System degrades to bounded state, `log_only`, or fail-closed | `FAIL` | all runtime profiles |
| `FD-03` | Resource exhaustion enforces safe degradation | `AB-DEGRADE` | Exhaust declared budget envelope | Correct degradation state reached | `FAIL` | all runtime profiles |
| `FD-04` | Missing privilege causes denial, not silent fallback promotion | `AB-DEGRADE` | Remove required privilege token/path | Action denied or safe degraded | `FAIL` | all runtime profiles |
| `FD-05` | Recovery path is explicit and non-retroactive | `AB-DEGRADE` | Inspect recovery from degraded state | Re-entry is witnessable and does not retroactively legitimize invalid period | `FAIL` | `FULL`, any profile claiming recovery discipline |
| `FD-06` | Review failure does not mutate confirmed memory | `AB-DEGRADE` | Force review contradiction after candidate/provisional stage | No illegitimate memory authority survives | `FAIL` | `REVIEW`, `PROMOTION`, `FULL`, `QUANTUM`, `VISION` |

### 11.8 Classical implementation-profile overlay tests

| ID | Claim under test | Required bundle | Procedure | Pass condition | On fail | Profiles |
|---|---|---|---|---|---|---|
| `CP-01` | `ARQ-MEM` rollback semantics honored | `AB-EVENT` / `AB-DEGRADE` | Inspect memory profile event and rollback class | Declared rollback class matches runtime behavior | `FAIL` | profile-specific |
| `CP-02` | `ARQ-PLANNER` branch mutation remains bounded | `AB-EVENT` / `AB-DEGRADE` | Inspect planner event path | Plan-graph mutation respects queue and review bounds | `FAIL` | profile-specific |
| `CP-03` | `ARQ-RAG` retrieval assembly stays source-bounded | `AB-EVENT` | Inspect RAG event with retrieved context | No source inflation or silent authority from retrieval sprawl | `FAIL` | profile-specific |
| `CP-04` | `ARQ-VISION` semantic path respects VXCX/privacy discipline | `AB-INTEGRATION` | Inspect visual event bundle | No raw-pixel leakage; VXCX hooks preserved | `FAIL` | `ARQ-VISION`, `ARQ-CONF-VISION` |

### 11.9 Cross-protocol integration tests

| ID | Claim under test | Required bundle | Procedure | Pass condition | On fail | Profiles |
|---|---|---|---|---|---|---|
| `INT-01` | ARQ remains subordinate to L4 | `AB-INTEGRATION` | Inspect at least one positive-score event that pressures a budget or feasibility limit | L4 veto or bounded denial occurs where required | `FAIL` | all runtime profiles |
| `INT-02` | Local ARQ logs are not mislabeled as external witness resolution | `AB-INTEGRATION` | Compare ARQ local bundle to any external claim | No externalized authority claim without witness-compatible path | `FAIL` | all runtime profiles |
| `INT-03` | ARQ does not self-certify Beacon identity | `AB-INTEGRATION` | Inspect any identity/continuity export | Export remains bounded continuity signal, not full identity verdict | `FAIL` | any profile exporting continuity |
| `INT-04` | ARQ does not export federation authority directly | `AB-INTEGRATION` | Inspect any SER-FED/EWCEP-facing claim | ARQ exports at most upstream signal; no direct authority minting | `FAIL` | any profile exporting upward |
| `INT-05` | VXCX disclosure policy survives ARQ handling | `AB-INTEGRATION` | Inspect visual event path through ARQ | Privacy/export rules remain intact after classification | `FAIL` | `VISION` overlays |

### 11.10 Quantum overlay tests

| ID | Claim under test | Required bundle | Procedure | Pass condition | On fail | Profiles |
|---|---|---|---|---|---|---|
| `Q-01` | Trusted quantum boundary is declared and finite | `AB-BOUNDARY` | Verify boundary record for quantum path | Finite `H_SA` boundary declared with trusted / uncontrolled split | `FAIL` | `ARQ-CONF-QUANTUM` |
| `Q-02` | Quantum entropy bound claim matches declared boundary | `AB-EVENT` / `AB-BOUNDARY` | Inspect theorem use and boundary dimension | No bound claim exceeds what the declared boundary supports | `FAIL` | `ARQ-CONF-QUANTUM` |
| `Q-03` | `E_use` remains inside trusted boundary | `AB-EVENT` | Inspect entanglement claim path | No usable-entanglement claim relies on uncontrolled environment degrees of freedom | `FAIL` | `ARQ-CONF-QUANTUM` |
| `Q-04` | Boundary or epoch invalidation kills promotion authority | `AB-DEGRADE` | Trigger invalidation during or before promotion path | Promotion denied or downgraded despite mathematical bound still being formally true | `FAIL` | `ARQ-CONF-QUANTUM` |

---

## 12. Conformance Decision Rules

### 12.1 `ARQ-AUDIT-DOC`

A release set MAY claim `ARQ-AUDIT-DOC` only if all `DOC-*` tests applicable to its declared release level pass.

### 12.2 `ARQ-CONF-BASE`

An implementation MAY claim `ARQ-CONF-BASE` only if:

- `BND-*`, `TR-01..04`, `VAL-01..06`, `FD-01..04` all pass or produce the required `FAIL_CLOSED_OK` result where applicable;
- it does not claim confirmed EA authority.

### 12.3 `ARQ-CONF-REVIEW`

An implementation MAY claim `ARQ-CONF-REVIEW` only if `ARQ-CONF-BASE` holds and `LC-01..03`, `AE-01..03`, and the required replay samples for review are satisfied.

### 12.4 `ARQ-CONF-PROMOTION`

An implementation MAY claim `ARQ-CONF-PROMOTION` only if `ARQ-CONF-REVIEW` holds and `LC-04..06`, `TR-05`, and all promotion-grade replay requirements are satisfied.

### 12.5 `ARQ-CONF-FULL`

An implementation MAY claim `ARQ-CONF-FULL` only if:

- `ARQ-CONF-PROMOTION` holds;
- all relevant `FD-*` tests, recovery path tests, and declared profile overlay tests pass;
- no integration boundary is violated.

### 12.6 Overlay claims

Overlay claims (`ARQ-CONF-QUANTUM`, `ARQ-CONF-VISION`) MAY be added only if the corresponding overlay tests all pass.

---

## 13. Release Gate for GitHub / Zenodo

A publication-ready ARQ v0.2 supplement SHOULD NOT be released to GitHub / Zenodo as a coherent package unless the following minimum gate is satisfied:

1. `ARQ-AUDIT-DOC-FULL` passes;
2. this matrix is included in the release set;
3. the release hash manifest is present;
4. the core, models, notation, valuation, trust, lifecycle, theorem, schema, implementation-profile, failure-mode, and integration documents are all present;
5. any proof-companion documents are clearly marked as supporting rather than canonical normative core;
6. the release note states which runtime conformance levels, if any, are actually implemented versus merely specified.

A repository MAY publish drafts earlier, but it MUST NOT present them as conformance-complete if this gate is not satisfied.

---

## 14. Auditor Guidance (Non-Normative)

### 14.1 Slot A / Slot B reading discipline

Auditors SHOULD split evidence into:

- **Slot A** — hard evidence: hashes, signatures, boundary records, epoch validity, required record bundles, explicit lifecycle transitions;
- **Slot B** — interpretive evidence: utility judgment, anomaly-tuning rationale, continuity interpretation, profile-specific heuristics.

**Hard rule:** Slot B SHOULD NEVER rescue a Slot A failure.

### 14.2 Anti-echo reading discipline

If several records or textual explanations merely restate the same local claim in different prose, auditors SHOULD count that as one signal until a new measurement, new witness path, or new contradiction channel appears.

### 14.3 Bounded audit honesty

A `BOUNDED_PASS` is not a failure. It is often the most honest result. It means the implementation works inside the model and profile it actually declared, not inside some inflated story.

---

## 15. Bridges (required)

### Explicit bridge

ARQ is made auditable only when four things meet: the entity-facing ontology from `c = a + b` / SER, the L4 constraint envelope, the witness semantics from L4 Witness, and the internal correction/memory discipline from ARQ. This matrix is the operational bridge that turns those layers into pass/failable claims rather than adjacent prose.

### Hidden bridge 1 — cybernetics / Ashby

A regulator must match the variety of what it regulates. That is why the matrix is not one score but a layered set of tests: document integrity, boundary declaration, replay, promotion, degradation, and integration. A single “works on demo” verdict is too low-variety to regulate a long-lived error-processing stack.

### Hidden bridge 2 — information theory / bounded channels

Audit bandwidth is finite. The matrix therefore requires structured records, hashes, profile declarations, and bounded replay bundles rather than unlimited narrative justification. Trust is compressed into checkable channels.

---

## 16. Earth Paragraph (engineering)

This is closer to aircraft maintenance and incident review than to benchmarking. You do not sign off a machine because one happy-path run looked good. You check the serial trace, the maintenance log, the denied actions, the breaker trips, the rollback path, and whether the bad day stays bad in a bounded way. ARQ is the same: if it only looks smart when the weather is good, it is not ready.

---

## 17. Closing Note

ARQ v0.2 becomes serious only when its claims can survive audit.

A good protocol can describe novelty. A mature protocol can also describe denial, downgrade, quarantine, contradiction, and failure without losing honesty.

That is what this matrix is for.
