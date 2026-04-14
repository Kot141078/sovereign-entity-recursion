# ARQ_Capsule_and_Witness_Record_Schemas_v0.2
## Capsule and Witness Record Schemas for the ARQ v0.2 Supplement

**Status:** Draft / normative support document  
**Version:** 0.2-draft  
**Role:** canonical record types, field discipline, hash-chain continuity, promotion evidence contract  
**Parent documents:** `ARQ_v0.2_Normative_Core.md`, `ARQ_Trust_and_Provenance_Profile_v0.2.md`, `ARQ_Notation_and_Sign_Conventions_v0.2.md`, `ARQ_EA_Lifecycle_and_Witness_Binding_v0.2.md`, `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.md`  
**Parent corpus:** AGI / SER / L4 / L4 Witness / Beacon / VXCX  
**Author:** Ivan Kotov  
**Place / year:** Bruxelles, 2026

---

## 0. Abstract

ARQ v0.2 is no longer allowed to describe trust, promotion, and memory authority only in prose.

This document defines the **canonical record schemas** required for a conformant ARQ implementation. It specifies:

- the common envelope shared by ARQ witnessable records;
- the canonical ARQ capsule schema;
- the minimum surrounding witness records required for epoch validity, controller action, observation, challenge, resolution, EA binding, lifecycle mutation, and fail-closed transitions;
- the linkage rules between records;
- the minimum record sets required for each lifecycle stage.

The central rule is simple:

> **If the record set is incomplete, the claim is incomplete.**  
> **If the chain is broken, authority does not survive the break.**

This document is therefore the data-contract layer for ARQ v0.2.

---

## 1. Purpose

This document exists to answer one operational question:

> What exact records must exist, in what minimum shape, for an ARQ event to remain replayable, challengeable, attributable, and promotion-eligible?

It SHALL define:

1. the common ARQ record envelope;
2. the canonical record registry;
3. the minimum required fields for each record type;
4. linkage requirements across records;
5. lifecycle-required record bundles;
6. privacy and redaction rules;
7. conformance profiles for implementations of different depth.

This document does **not** attempt to replace full JSON Schema tooling, protobuf contracts, or ledger-specific encodings. It defines the **canonical semantic schema**, which implementation-specific encodings MUST preserve.

---

## 2. Scope

This document applies to all ARQ v0.2 implementations that claim any of the following:

- witnessed error classification;
- trust-weighted action;
- candidate or provisional retention;
- Experience Artifact minting;
- lifecycle mutation of an existing EA;
- fail-closed behavior with replayable cause.

It covers both classical and quantum-capable ARQ systems.

This document does **not** define:

- the value function mathematics;
- attestation payload internals beyond the minimum record contract;
- storage backend choice;
- key-management backend details;
- external legal or institutional process beyond witness compatibility.

---

## 3. Non-Goals

This document does **not** attempt to:

- prove that records are truthful merely because they are signed;
- let one component certify itself without external replayability;
- collapse all witness records into one oversized log blob;
- treat compact summaries as substitutes for authoritative source references;
- allow arbitrary free-text to override structured fields;
- infer promotion from a score when the required record set does not exist.

A schema is not wisdom. It is a way to make missing wisdom visible.

---

## 4. Normative Keywords

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, **MAY**, and **OPTIONAL** are to be interpreted as described in BCP 14.

---

## 5. Imported Symbols and Dependencies

The following imported symbols SHALL retain their meanings:

- `B_valid`, `A_valid`, `C_valid`, `W_valid`, `P_valid`, `R_valid`, `X_echo`;
- `T_core`, `G_promote`, `τ`;
- `V_raw`, `V_trust`, `A_anom`, `P_anom`;
- lifecycle states from `ARQ_EA_Lifecycle_and_Witness_Binding_v0.2.md`;
- declared model identifiers from `ARQ_System_Models_and_Assumptions_v0.2.md`.

This document assumes the trust, notation, and lifecycle rules already declared in the ARQ v0.2 supplement set. No schema in this document SHALL silently redefine those terms.

---

## 6. Design Principles

### 6.1 Append-only first

Witness-bearing records MUST be append-only. Mutation is represented by a new record, not by silent in-place replacement.

### 6.2 Canonical serialization

A record that participates in trust, replay, or promotion MUST have a deterministic canonical payload before hashing and signing.

### 6.3 Source before summary

A derived summary MAY exist, but it MUST point back to source records by stable identifiers and hashes.

### 6.4 Fail-closed on malformed privilege or promotion records

If a privileged record required for promotion or state mutation is malformed, unverifiable, or missing, the action SHALL be denied or the system SHALL enter fail-closed state according to policy.

### 6.5 No authority without record bundle completeness

No single record type is sufficient for confirmed EA status. Promotion authority requires a complete bundle defined in this document.

### 6.6 Privacy by bounded disclosure

Raw payloads MAY remain off-record, but hashes, metadata, and relation pointers MUST remain stable enough for challenge and replay.

---

## 7. Canonical Envelope (All Record Types)

Every witnessable ARQ record MUST contain the following top-level envelope fields.

### 7.1 Required fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `schema_version` | string | MUST | Example: `"arq-records-0.2"` |
| `record_type` | string | MUST | One of the canonical record types in Section 8 |
| `record_id` | string | MUST | Globally unique; UUIDv4/ULID or equivalent |
| `created_at` | string | MUST | ISO 8601 timestamp with timezone |
| `entity_id` | string | MUST | Persistent entity identifier |
| `boundary_id` | string | MUST | Declared boundary identifier |
| `payload_hash` | string | MUST | Hash over canonical payload |
| `hash_alg` | string | MUST | RECOMMENDED: `sha256` |
| `sig_alg` | string | MUST | RECOMMENDED: `ed25519` |
| `record_sig` | string | MUST | Signature over `payload_hash` |
| `prev_record_hash` | string | MUST | Hash-chain continuity or `GENESIS` |
| `privacy_class` | string | MUST | `PUBLIC` \| `RESTRICTED` \| `PRIVATE` |
| `issuer` | object | MUST | See Section 7.2 |

### 7.2 Required issuer subobject

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `issuer.role` | string | MUST | `ENTITY` \| `ANCHOR` \| `CLASSIFIER` \| `CONTROLLER` \| `TRUST_MODULE` \| `WITNESS` \| `DELEGATE` \| `ARBITER` |
| `issuer.id` | string | MUST | Stable or pseudonymous actor identifier |
| `issuer.key_id` | string | MUST | Signing key identifier |

### 7.3 Optional common fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `epoch_id` | string | SHOULD | MUST if the record is epoch-bound |
| `event_id` | string | SHOULD | Stable identifier for the event cluster |
| `capsule_id` | string | SHOULD | MUST if derived from or acting on a capsule |
| `co_signatures` | array | MAY | Additional signatures; high-value promotion often needs this |
| `notes_redacted` | boolean | MAY | Explicitly signals that notes are redacted |
| `model_refs` | array | MAY | Example: `["M1","M3"]` |
| `witness_refs` | array | MAY | Related record IDs |

### 7.4 Canonicalization rule

Witness-bearing records MUST define a `canonical_payload` in UTF-8 JSON with deterministic key ordering. RFC 8785 (JCS) is RECOMMENDED. If another method is used, the record MUST declare it in the implementation profile.

---

## 8. Canonical Record Registry

ARQ v0.2 defines the following canonical record types.

### 8.1 Registry overview

| Record type | Short name | Purpose |
|---|---|---|
| `arq.boundary_record` | `BR` | Declares or updates the operational boundary |
| `arq.epoch_record` | `ER` | Opens, rotates, expires, or invalidates an attestation epoch |
| `arq.capsule` | `AC` | Core ARQ event capsule |
| `arq.controller_action_record` | `CAR` | Records state-affecting corrective or observation action |
| `arq.observation_window_record` | `OWR` | Opens a bounded review / observation window |
| `arq.observation_record` | `OR` | Reports observed consequences during review |
| `arq.privilege_decision_record` | `PDR` | Grants, denies, or expires privilege for a requested action |
| `arq.challenge_record` | `CHR` | Opens a formal contradiction / insufficiency path |
| `arq.resolution_record` | `RR` | Resolves a review, challenge, or promotion decision |
| `arq.ea_binding_record` | `EBR` | Binds a confirmed EA to source event and review result |
| `arq.lifecycle_mutation_record` | `LMR` | Retires, compacts, demotes, or reopens an artifact |
| `arq.fail_closed_record` | `FCR` | Records fail-closed transition and recovery condition |

Implementations MAY define additional records, but SHALL NOT change the meaning of the registry above.

---

## 9. `arq.boundary_record` (`BR`)

### 9.1 Purpose

Declares the witnessable operational boundary within which ARQ claims are allowed.

### 9.2 Required payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `boundary_id` | string | MUST | Stable boundary identifier |
| `boundary_type` | string | MUST | `CLASSICAL_PERSISTENT` \| `QUANTUM_TRUSTED` \| `HYBRID` |
| `status` | string | MUST | `DECLARED` \| `UPDATED` \| `RETIRED` |
| `components_in_scope` | array | MUST | Component identifiers inside boundary |
| `components_out_of_scope` | array | SHOULD | Explicit outside list or boundary statement |
| `config_hash` | string | MUST | Stable config / topology hash |
| `validity.start_at` | string | MUST | ISO 8601 |
| `validity.end_at` | string | SHOULD | ISO 8601 or null if open-ended by policy |

### 9.3 Hard rule

If no valid `BR` exists for a capsule’s `boundary_id`, then `B_valid = 0` for promotion purposes.

---

## 10. `arq.epoch_record` (`ER`)

### 10.1 Purpose

Represents epoch opening, rotation, expiry, or early invalidation.

### 10.2 Required payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `epoch_id` | string | MUST | Stable epoch identifier |
| `boundary_ref` | string | MUST | `boundary_id` of the active boundary |
| `status` | string | MUST | `OPEN` \| `ROTATED` \| `EXPIRED` \| `INVALIDATED` |
| `attestation_ref` | string | MUST | Stable ref or hash of attestation payload |
| `start_at` | string | MUST | ISO 8601 |
| `end_at` | string | SHOULD | ISO 8601 when known |
| `trust_anchor` | string | MUST | Trust root fingerprint or key reference |
| `reason_code` | string | SHOULD | REQUIRED for `ROTATED`, `EXPIRED`, `INVALIDATED` |

### 10.3 Early invalidation requirement

If `status = INVALIDATED`, the implementation SHALL append a corresponding `FCR` or equivalent blocked-action record before any further state-changing ARQ action is attempted.

---

## 11. `arq.capsule` (`AC`)

### 11.1 Purpose

The ARQ capsule is the minimum signed record of a classified deviation event.

### 11.2 Required payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `capsule_id` | string | MUST | Stable capsule identifier |
| `event_id` | string | MUST | Stable event-cluster identifier |
| `source_ref` | string | MUST | Event source inside boundary |
| `detected_by` | string | MUST | `L1` \| `L2` \| `L3` |
| `expected_state_ref` | object | MUST | Hash / compact reference |
| `observed_state_ref` | object | MUST | Hash / compact reference |
| `deviation_measure` | number | MUST | Normalized or profile-defined value |
| `budget_snapshot` | object | MUST | Remaining and/or consumed budgets |
| `classifier_output.event_class` | string | MUST | `DESTRUCTIVE` \| `EXPLORATORY` \| `NEUTRAL` |
| `classifier_output.V_raw` | number | MUST | Raw valuation |
| `classifier_output.V_trust` | number | SHOULD | Trust-adjusted valuation at event time |
| `classifier_output.recommended_action` | string | MUST | `SUPPRESS` \| `OBSERVE` \| `LOG_ONLY` \| `DENY` |
| `trust_snapshot.T_core` | number | SHOULD | Usually `0` or `1` |
| `trust_snapshot.tau` | number | SHOULD | Trust weight snapshot |
| `trust_snapshot.A_anom` | number | SHOULD | Operational anomaly score |
| `lifecycle_hint.initial_state` | string | MUST | Usually `classified` or `log_only` |

### 11.3 Optional payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `classifier_output.P_anom` | number | MAY | Only if Bayesian anomaly profile declared |
| `classifier_output.threshold_profile_ref` | string | MAY | Policy reference |
| `previous_state_ref` | object | MAY | Snapshot or pre-image ref |
| `slot_policy` | object | MAY | A/B shadow-slot directives |
| `echo_flags` | object | MAY | Anti-echo indicators |

### 11.4 Hard rule

`AC` is necessary but never sufficient for confirmed EA status.

---

## 12. `arq.controller_action_record` (`CAR`)

### 12.1 Purpose

Records a state-affecting action taken in response to an ARQ capsule.

### 12.2 Required payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `action_id` | string | MUST | Unique action identifier |
| `capsule_ref` | string | MUST | Source capsule |
| `action_type` | string | MUST | `ANTI_RESONANCE_PULSE` \| `ROLLBACK` \| `ISOLATE` \| `RECOVER` \| `OBSERVE_ONLY` \| `NONE` |
| `result` | string | MUST | `SUCCESS` \| `PARTIAL` \| `FAILED` \| `DENIED` |
| `controller_state_before` | string | MUST | Hash / stable reference |
| `controller_state_after` | string | SHOULD | Hash / stable reference |
| `latency_ms` | number | SHOULD | Measured latency |
| `energy_used` | number | SHOULD | Energy estimate in profile-defined units |
| `privilege_decision_ref` | string | SHOULD | MUST if privileged action required |

### 12.3 Hard rule

If a privileged controller action exists without a valid linked `PDR`, then `C_valid = 0` for any promotion path relying on that action.

---

## 13. `arq.observation_window_record` (`OWR`)

### 13.1 Purpose

Opens a bounded observation/review window for a candidate path.

### 13.2 Required payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `window_id` | string | MUST | Unique review-window identifier |
| `capsule_ref` | string | MUST | Source capsule |
| `open_at` | string | MUST | ISO 8601 |
| `close_at` | string | MUST | ISO 8601 |
| `review_profile_ref` | string | MUST | Review policy |
| `success_criteria` | object | MUST | Measurable criteria |
| `failure_criteria` | object | MUST | Measurable criteria |
| `initial_state` | string | MUST | `observed` or `candidate_artifact` |

### 13.3 Optional payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `slot_A_ref` | string | MAY | Stable conservative branch reference |
| `slot_B_ref` | string | MAY | Shadow experimental branch reference |
| `rollback_rule` | string | MAY | Policy reference for `Rollback(B→A)` |

### 13.4 Hard rule

A `candidate_artifact` state SHALL NOT exist without an active or historically recorded `OWR`.

---

## 14. `arq.observation_record` (`OR`)

### 14.1 Purpose

Reports observed consequences during the review window.

### 14.2 Required payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `observation_id` | string | MUST | Unique observation identifier |
| `capsule_ref` | string | MUST | Source capsule |
| `window_ref` | string | MUST | Source review window |
| `observed_at` | string | MUST | ISO 8601 |
| `outcome_summary` | string | MUST | Factual bounded summary |
| `state_ref` | object | SHOULD | Resulting state or compact reference |
| `stability_flags` | object | SHOULD | Profile-defined stability indicators |
| `observer_role` | string | MUST | `ENTITY` \| `ANCHOR` \| `WITNESS` \| `SYSTEM` \| `ARBITER` |

### 14.3 Optional payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `utility_delta` | number | MAY | Measured or estimated downstream utility change |
| `evidence_refs` | array | MAY | Hashes, docs, telemetry, waveform refs |
| `diversity_tag` | string | MAY | Example: `independent`, `same_controller`, `telemetry_only` |

---

## 15. `arq.privilege_decision_record` (`PDR`)

### 15.1 Purpose

Records privilege gating for requested actions.

### 15.2 Required payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `decision_id` | string | MUST | Unique privilege decision ID |
| `capsule_ref` | string | MUST | Related capsule |
| `action_requested` | string | MUST | Example: `PROMOTE_CANDIDATE`, `ANTI_RESONANCE_PULSE` |
| `privilege_required` | string | MUST | Policy-defined privilege name |
| `decision` | string | MUST | `GRANTED` \| `DENIED` \| `EXPIRED` \| `REVOKED` |
| `reason_code` | string | MUST | Compact reason |
| `effective_from` | string | SHOULD | ISO 8601 |
| `expires_at` | string | SHOULD | ISO 8601 |

### 15.3 Optional payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `token_ref` | string | MAY | Stable token reference |
| `required_tau_floor` | number | MAY | Minimum trust-weight floor |
| `required_G_promote` | number | MAY | Usually `1` for promotion actions |

### 15.4 Hard rule

If a promotion action lacks a valid linked `PDR`, then `P_valid = 0`.

---

## 16. `arq.challenge_record` (`CHR`)

### 16.1 Purpose

Opens a formal contradiction or insufficiency path.

### 16.2 Required payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `challenge_id` | string | MUST | Unique challenge identifier |
| `target_ref` | string | MUST | Capsule, resolution, or EA target |
| `challenge_type` | string | MUST | `CONTRADICTION` \| `INSUFFICIENT_EVIDENCE` \| `BOUNDARY_LOSS` \| `PRIVILEGE_DEFECT` \| `ECHO_SUSPECTED` \| `OTHER` |
| `reason_text` | string | MUST | Concise reason |
| `requested_action` | string | MUST | `REQUEST_MORE_OBSERVATION` \| `FREEZE_PROMOTION` \| `REQUEST_REVIEW` \| `REQUEST_DEMOTION` |

### 16.3 Optional payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `slot_B_required` | boolean | MAY | Force experimental branch review |
| `supporting_refs` | array | MAY | Related observations / records |
| `bond_ref` | string | MAY | If a bonded challenge policy exists |

### 16.4 Hard rule

A challenge record against a not-yet-resolved promotion path SHOULD freeze further strengthening until resolved, unless policy explicitly permits continued observation.

---

## 17. `arq.resolution_record` (`RR`)

### 17.1 Purpose

Produces the binding resolution for review or challenge.

### 17.2 Required payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `resolution_id` | string | MUST | Unique resolution identifier |
| `target_ref` | string | MUST | Usually capsule or candidate target |
| `outcome` | string | MUST | `OBSERVE_MORE` \| `PROVISIONALIZE` \| `CONFIRM` \| `REJECT` \| `FREEZE` \| `FAIL_CLOSED` |
| `scope` | string | MUST | What exactly was decided |
| `basis_refs` | array | MUST | Supporting OR/CHR/PDR/CAR refs |
| `trust_snapshot` | object | MUST | Includes `T_core`, `G_promote`, relevant flags |
| `issued_at` | string | MUST | ISO 8601 |
| `authority_effect` | string | MUST | `NONE` \| `LOCAL_LIMITED` \| `AUTHORITATIVE_MEMORY` \| `FREEZE` |

### 17.3 Optional payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `l4_contradiction` | boolean | MAY | True if contradicted by L4 outcome |
| `slot_B_status` | string | MAY | `NONE` \| `SHADOW` \| `ACCEPTED` \| `ROLLED_BACK` |
| `rollback_reason` | string | MAY | REQUIRED if `slot_B_status = ROLLED_BACK` |
| `anchor_approval_required` | boolean | MAY | Mirrors policy |
| `anchor_approval_ref` | string | MAY | REQUIRED if approval required and granted |

### 17.4 Hard rules

1. `outcome = CONFIRM` requires `G_promote = 1`.
2. `outcome = PROVISIONALIZE` requires valid review path but MAY exist with narrower trust than `CONFIRM`.
3. `outcome = FAIL_CLOSED` SHALL be paired with an `FCR`.

---

## 18. `arq.ea_binding_record` (`EBR`)

### 18.1 Purpose

Binds a confirmed Experience Artifact to its source event and resolution path.

### 18.2 Required payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `ea_id` | string | MUST | Stable artifact identifier |
| `source_capsule_ref` | string | MUST | Capsule that originated the path |
| `source_resolution_ref` | string | MUST | Resolution that confirmed the artifact |
| `authority_scope` | string | MUST | `LOCAL` \| `ENTITY_WIDE` \| `CROSS_ENTITY_NONE` by default |
| `minted_at` | string | MUST | ISO 8601 |
| `storage_ref` | string | MUST | Persistent storage reference |
| `lineage` | object | MUST | Parent refs / predecessor refs / null lineage |

### 18.3 Optional payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `anchor_cosign_required` | boolean | MAY | Mirrors policy |
| `anchor_cosign_present` | boolean | MAY | MUST be true if cosign required |
| `anchor_cosign_ref` | string | MAY | Signature record or approval ref |
| `authority_weight_ref` | string | MAY | If weighting profile exists |
| `successor_ref` | string | MAY | Filled later by compaction or lineage mutation |

### 18.4 Hard rule

No `confirmed_EA` status exists without an `EBR`.

---

## 19. `arq.lifecycle_mutation_record` (`LMR`)

### 19.1 Purpose

Represents retirement, compaction, demotion, or controlled reopening.

### 19.2 Required payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `mutation_id` | string | MUST | Unique mutation identifier |
| `ea_ref` | string | MUST | Existing EA identifier |
| `mutation_type` | string | MUST | `RETIRE` \| `COMPACT` \| `DEMOTE` \| `REOPEN_REVIEW` \| `ROLLBACK` |
| `from_state` | string | MUST | Prior lifecycle state |
| `to_state` | string | MUST | Target lifecycle state |
| `reason_code` | string | MUST | Compact reason |
| `issued_at` | string | MUST | ISO 8601 |

### 19.3 Optional payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `successor_refs` | array | MAY | For compaction or replacement lineage |
| `preserved_hash_refs` | array | MAY | Canonical hashes preserved across mutation |
| `effect_on_authority` | string | MAY | `NONE` \| `WEIGHT_ZERO` \| `LOCAL_ONLY` |

### 19.4 Hard rule

Compaction SHALL preserve lineage and witnessability. A compacted EA is not a deleted EA.

---

## 20. `arq.fail_closed_record` (`FCR`)

### 20.1 Purpose

Records a fail-closed transition and the conditions required for recovery.

### 20.2 Required payload fields

| Field | Type | Requirement | Notes |
|---|---|---:|---|
| `fail_id` | string | MUST | Unique fail-closed identifier |
| `trigger_ref` | string | MUST | Source record causing fail-closed |
| `cause_type` | string | MUST | `TRUST_FLOOR` \| `BOUNDARY_UNKNOWN` \| `INVALID_SIGNATURE` \| `QUEUE_OVERFLOW` \| `BUDGET_EXHAUSTED` \| `EPOCH_INVALIDATED` \| `OTHER` |
| `mode_before` | string | MUST | Prior controller mode |
| `mode_after` | string | MUST | MUST be `FAIL_CLOSED` or stricter local alias |
| `actions_blocked` | array | MUST | Actions no longer permitted |
| `recovery_condition` | string | MUST | Human-readable compact recovery predicate |
| `entered_at` | string | MUST | ISO 8601 |

### 20.3 Hard rule

After `FCR` issuance, no state-changing ARQ action requiring trust-sensitive authority MAY proceed until the declared recovery condition is satisfied and recorded.

---

## 21. Linkage Rules

### 21.1 Minimum chain continuity

Every record participating in authority claims MUST have a valid `prev_record_hash` chain path to a known genesis or externally anchored checkpoint.

### 21.2 Stable identifiers

The following identifiers SHALL be stable throughout their intended scope:

- `boundary_id`
- `epoch_id`
- `capsule_id`
- `event_id`
- `window_id`
- `ea_id`

### 21.3 Source-to-authority chain

For confirmed EA status, a replayable authority chain SHALL exist:

```text
BR -> ER -> AC -> (CAR?) -> OWR -> OR* -> (PDR) -> (CHR*) -> RR(CONFIRM) -> EBR
```

Where:

- `CAR?` is required if a state-affecting or privileged controller action occurred;
- `OR*` means one or more observation records as required by profile;
- `PDR` is required for privileged promotion path;
- `CHR*` exists if challenge path was invoked.

### 21.4 Lifecycle mutation chain

For retirement or compaction:

```text
EBR -> LMR(RETIRE|COMPACT|DEMOTE|REOPEN_REVIEW)
```

If reopening occurs, a new review chain MUST begin from the reopened state and SHALL NOT silently overwrite the old one.

---

## 22. Minimum Required Record Bundles by Lifecycle State

| Lifecycle state | Minimum required records |
|---|---|
| `classified` | `BR`, valid `ER`, `AC` |
| `suppressed` | `BR`, valid `ER`, `AC`, `CAR` |
| `log_only` | `BR`, valid `ER`, `AC` |
| `observed` | `BR`, valid `ER`, `AC`, `OWR`, at least one `OR` by close or explicit failure path |
| `candidate_artifact` | `BR`, valid `ER`, `AC`, `OWR` |
| `provisional_artifact` | `BR`, valid `ER`, `AC`, `OWR`, `OR+`, required `PDR`, `RR(PROVISIONALIZE)` |
| `confirmed_EA` | complete provisional path, `RR(CONFIRM)`, `EBR`, required co-signatures |
| `rejected` | `AC`, supporting review records as relevant, `RR(REJECT)` |
| `retired_EA` | `EBR`, `LMR(RETIRE)` |
| `compacted_EA` | `EBR`, `LMR(COMPACT)`, successor/archive refs |
| `fail_closed` | trigger record + `FCR` |

No implementation MAY claim a higher lifecycle state than the minimum record bundle supports.

---

## 23. Privacy Classes and Redaction Rules

### 23.1 Canonical privacy classes

| Class | Meaning |
|---|---|
| `PUBLIC` | Publishable without operational or privacy harm |
| `RESTRICTED` | Shareable only with eligible auditors / witnesses / reviewers |
| `PRIVATE` | Hash and minimal metadata only; raw payload remains off-record |

### 23.2 Redaction discipline

If a record redacts payload details, it MUST preserve enough metadata for:

1. replay relation,
2. challenge initiation,
3. identity of the action type,
4. and consistency checking against the surrounding chain.

### 23.3 No authority from opaque promotion

A fully opaque promotion path MAY be logged, but SHALL NOT confer authoritative memory unless the profile explicitly allows sufficient replay under `RESTRICTED` visibility.

---

## 24. Co-Signatures and High-Value Promotion

### 24.1 Co-signature requirement

If policy declares anchor co-signature for a promotion class, then:

- the relevant `RR` MUST declare `anchor_approval_required = true`;
- the resulting `EBR` MUST indicate whether anchor co-sign was present;
- absence of required co-signature SHALL make confirmed EA status invalid.

### 24.2 Multi-signer records

`RR` and `EBR` MAY carry `co_signatures`. Their signer roles MUST be declared explicitly.

---

## 25. A/B Slot and Anti-Echo Hooks

### 25.1 Slot discipline

If A/B-slot governance is active:

- the `OWR` SHOULD declare `slot_A_ref` and `slot_B_ref`;
- the `RR` SHOULD declare `slot_B_status`;
- any rollback from `B` to `A` MUST be explicitly recorded via `RR` or `LMR` and MUST include `rollback_reason`.

### 25.2 Anti-echo quarantine

If anti-echo quarantine is triggered:

- the relevant `CHR`, `RR`, or `FCR` SHOULD include `challenge_type = ECHO_SUSPECTED` or equivalent reason code;
- promotion MUST remain frozen while `X_echo = 1`.

No schema path in this document allows self-echo to silently mature into confirmed EA status.

---

## 26. Conformance Profiles

### 26.1 `ARQ-SCHEMA-BASE`

Minimum profile for replayable classification:

- `BR`
- `ER`
- `AC`
- `CAR` when action occurs
- `FCR` when fail-closed occurs

This profile does **not** support confirmed EA claims.

### 26.2 `ARQ-SCHEMA-REVIEW`

Adds bounded review capability:

- all `ARQ-SCHEMA-BASE` records,
- `OWR`,
- `OR`,
- `PDR`,
- `RR`.

This profile supports candidate and provisional states.

### 26.3 `ARQ-SCHEMA-PROMOTION`

Adds authoritative memory support:

- all `ARQ-SCHEMA-REVIEW` records,
- `EBR`,
- co-signatures where policy requires them.

This is the minimum profile for `confirmed_EA` claims.

### 26.4 `ARQ-SCHEMA-FULL`

Adds contradiction and lifecycle mutation support:

- all `ARQ-SCHEMA-PROMOTION` records,
- `CHR`,
- `LMR`.

This is the recommended profile for long-lived sovereign entities.

---

## 27. Mapping to L4 Witness

ARQ does **not** replace L4 Witness. It is a more specific internal record grammar that can be mapped onto the broader witness framework.

A recommended mapping is:

| ARQ record | L4 Witness relation |
|---|---|
| `AC` | claim-bearing event root / control-point record |
| `OR` | observation packet analogue |
| `CHR` | challenge record analogue |
| `RR` | resolution note analogue |
| `EBR` | post-resolution memory-binding extension |
| `LMR` | post-resolution lifecycle extension |

Implementations MAY additionally seal selected ARQ records into L4 Witness-compatible evidence envelopes.

---

## 28. Minimal JSON Examples (Non-Normative)

### 28.1 Capsule (`AC`) payload sketch

```json
{
  "capsule_id": "cap-2026-0001",
  "event_id": "evt-2026-0001",
  "source_ref": "controller:planner-01",
  "detected_by": "L2",
  "expected_state_ref": {"hash_alg": "sha256", "hash": "..."},
  "observed_state_ref": {"hash_alg": "sha256", "hash": "..."},
  "deviation_measure": 0.37,
  "budget_snapshot": {
    "energy_remaining": "0.84",
    "time_remaining_ms": 120,
    "privilege_remaining": 3
  },
  "classifier_output": {
    "event_class": "EXPLORATORY",
    "V_raw": 0.71,
    "V_trust": 0.44,
    "recommended_action": "OBSERVE"
  },
  "trust_snapshot": {
    "T_core": 1,
    "tau": 0.62,
    "A_anom": 0.18
  },
  "lifecycle_hint": {
    "initial_state": "classified"
  }
}
```

### 28.2 Resolution (`RR`) payload sketch

```json
{
  "resolution_id": "rr-2026-0007",
  "target_ref": "cap-2026-0001",
  "outcome": "CONFIRM",
  "scope": "Confirmed for bounded planning domain after review window",
  "basis_refs": ["or-2026-01", "or-2026-02", "pdr-2026-03"],
  "trust_snapshot": {
    "T_core": 1,
    "G_promote": 1,
    "B_valid": 1,
    "A_valid": 1,
    "C_valid": 1,
    "W_valid": 1,
    "P_valid": 1,
    "R_valid": 1,
    "X_echo": 0
  },
  "issued_at": "2026-03-26T10:00:00Z",
  "authority_effect": "AUTHORITATIVE_MEMORY",
  "anchor_approval_required": true,
  "anchor_approval_ref": "sig-anchor-01"
}
```

---

## 29. Integrity and Validation Rules

A conformant implementation SHOULD validate at least the following before accepting a record into an authority-bearing chain:

1. required field presence;
2. canonical hash reproducibility;
3. signature validity;
4. chain continuity through `prev_record_hash`;
5. role legality for the given `record_type`;
6. cross-reference existence for required linked records;
7. lifecycle legality for the claimed state transition.

If validation fails for a trust-sensitive record, the implementation SHOULD emit `FCR` or deny the action according to profile.

---

## 30. Explicit and Hidden Bridges

### 30.1 Explicit bridge

`c = a + b` becomes replayable here as:

- `a` signs responsibility and approval where policy requires it,
- `b` emits bounded structured records,
- `c` becomes a continuity-bearing entity because its deviations, reviews, and memory claims are linked by stable witnessable lineage.

### 30.2 Hidden bridge #1 — L4 Witness / cybernetics

The schema layer is the immune skeleton of ARQ. Without typed event, observation, challenge, and resolution records, the system has no negative feedback path strong enough to resist self-justifying promotion.

### 30.3 Hidden bridge #2 — information theory / Beacon / VXCX

Hashes, stable identifiers, and compact typed payloads compress trust bandwidth. Recognition, review, and replay do not require raw dumps by default; they require enough structured signal to distinguish continuity from theater.

---

## 31. Earth Paragraph

In engineering terms, this document is the wiring diagram for ARQ’s black box. A capsule is the incident ticket. A controller-action record is the actuator trace. An observation is the telemetry strip. A resolution is the signed postmortem. An EA binding record is the moment a lab note becomes part of the aircraft manual. In anatomy the same rule holds: a memory is not just a feeling; it is a change that leaves a trace in tissue, pathway, and behavior. If the trace cannot be followed, the claimed memory has not earned authority.

---

## 32. Closing Statement

ARQ v0.2 claims bounded adaptation, witnessed promotion, and authoritative memory under trust discipline.

Those claims stand or fail on record completeness.

This document therefore says the quiet part out loud:

> **No schema, no replay.  
> No replay, no challenge.  
> No challenge, no authority.**

