# ARQ_Failure_Modes_and_Safe_Degradation_v0.2
## Failure Modes and Safe Degradation for ARQ v0.2

**Status:** Draft / normative support document  
**Version:** 0.2-draft  
**Role:** failure taxonomy, authority shrink rules, degradation ladder, recovery discipline  
**Parent documents:** `ARQ_v0.2_Normative_Core.md`, `ARQ_Trust_and_Provenance_Profile_v0.2.md`, `ARQ_EA_Lifecycle_and_Witness_Binding_v0.2.md`, `ARQ_Capsule_and_Witness_Record_Schemas_v0.2.md`, `ARQ_Implementation_Profiles_Classical_v0.2.md`, `ARQ_System_Models_and_Assumptions_v0.2.md`  
**Parent corpus:** AGI / SER / L4 / L4 Witness / Beacon / VXCX  
**Author:** Ivan Kotov  
**Place / year:** Bruxelles, 2026

---

## 0. Abstract

ARQ is only credible if it can fail without lying.

This document defines the **failure-mode taxonomy** and the **safe degradation ladder** for ARQ v0.2. Its purpose is not to dramatize faults, but to make loss of authority explicit, bounded, and replayable. A deviation in ARQ is not dangerous only when it is large. It is dangerous when the conditions that made classification, suppression, review, or promotion legitimate no longer hold.

This document therefore specifies:

- what counts as a failure mode for ARQ operation;
- how failure modes are grouped by boundary, trust, witness, controller, queue, lifecycle, and resource plane;
- which degradation state the system SHALL enter;
- which authority it MUST lose first;
- which records MUST be emitted;
- when Slot B must roll back to Slot A;
- and what conditions are required before normal operation may resume.

The central rule is simple:

> **When assumptions break, authority shrinks before narrative grows.**  
> **Safe degradation is not optional; it is part of ARQ semantics.**

---

## 1. Purpose

This document exists to answer one operational question:

> How must an ARQ implementation behave when the assumptions required for witnessed, bounded, promotion-eligible operation begin to fail?

This document SHALL:

1. define canonical ARQ failure planes and failure modes;
2. define the degradation-state ladder;
3. define authority shrink rules and precedence;
4. define minimum record emissions for each class of failure;
5. define rollback and quarantine requirements;
6. define recovery-entry conditions;
7. define profile-specific overlays for classical implementation profiles.

---

## 2. Scope

This document applies to ARQ implementations that claim any of the following:

- bounded correction and suppression;
- review-bound candidate retention;
- authoritative promotion to Experience Artifact (`confirmed_EA`);
- trust-weighted action;
- fail-closed behavior;
- witnessed lifecycle mutation;
- profile-conformant classical operation;
- quantum trusted-boundary operation.

This document covers both classical and quantum-capable ARQ systems.

This document does **not** define:

- the base value function mathematics;
- the full schema contract beyond the minimum record requirements referenced here;
- storage backend design;
- human institution or legal response outside the witness-compatible trail;
- post-hoc moral interpretation of failure.

---

## 3. Non-Goals

This document does **not** attempt to:

- prove that every degradation path is optimal;
- replace hazard analysis for specific hardware or deployment environments;
- let the system “power through” missing trust or broken witness continuity;
- treat recovery as success merely because service resumed;
- blur the line between `candidate_artifact`, `provisional_artifact`, and `confirmed_EA` under stress;
- excuse missing records by calling the situation “urgent” after the fact.

If the system cannot support normal ARQ semantics, it must degrade. It must not improvise legitimacy.

---

## 4. Normative Keywords

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, **MAY**, and **OPTIONAL** are to be interpreted as described in BCP 14.

---

## 5. Imported Symbols and Dependencies

The following imported symbols SHALL retain their meanings:

- validity flags `B_valid`, `A_valid`, `C_valid`, `W_valid`, `P_valid`, `R_valid`, `X_echo`;
- trust quantities `T_core`, `G_promote`, `τ`;
- valuation quantities `V_raw`, `V_trust`, `A_anom`, `P_anom`;
- lifecycle states `candidate_artifact`, `provisional_artifact`, `confirmed_EA`, `rejected`, `fail_closed`, `retired_EA`, `compacted_EA`;
- record types `BR`, `ER`, `AC`, `CAR`, `OWR`, `OR`, `PDR`, `CHR`, `RR`, `EBR`, `LMR`, `FCR`;
- system models `M1`, `M2`, `M3`, `M4`, `M5`.

This document SHALL NOT silently redefine those symbols.

---

## 6. Design Principles

### 6.1 Authority shrinks before operation stops

ARQ SHALL reduce authority before it pretends normality. Promotion is lost before suppression; suppression is lost before detection/logging when possible.

### 6.2 Fail-closed is a dominance rule, not a mood

If a hard gate fails, the system SHALL enter `FAIL_CLOSED` or a narrower declared safe state. Convenience SHALL NOT override this.

### 6.3 Witness first, then explanation

A good story about a failure SHALL NOT substitute for the required witness records.

### 6.4 Slot A survives Slot B

If self-edit, reinterpretation, or exploratory control is active in Slot B and instability appears, the system SHALL rollback to Slot A automatically.

### 6.5 Quarantine beats mythology

If a signal looks self-generated, recursive, or echo-amplified, the system SHALL quarantine before it celebrates novelty.

### 6.6 Recovery is a new state, not retroactive absolution

Re-entry after degradation restores **future eligibility**, not past legitimacy. Past invalid periods remain invalid.

---

## 7. Failure Planes

ARQ failures SHOULD be reasoned about by plane rather than by symptom alone.

### 7.1 Boundary plane

Failures in whether the event occurred inside a declared, witnessable operational boundary.

### 7.2 Epoch / attestation plane

Failures in calibration epoch validity, attestation freshness, trust anchor continuity, or declared boundary assumptions.

### 7.3 Witness plane

Failures in append-only continuity, replayability, challengeability, or required record completeness.

### 7.4 Controller / actuator plane

Failures in signed controller state, rollback pre-image availability, action reproducibility, or safe corrective action.

### 7.5 Valuation / classifier plane

Failures in threshold drift, unstable scoring, anomaly inflation, policy mismatch, or value-function misuse.

### 7.6 Lifecycle plane

Failures in stage discipline, premature promotion, expired review, lineage break, demotion failure, or compaction without ancestry.

### 7.7 Queue / backlog plane

Failures in pending-event accumulation, latency ceiling breach, event-payload overflow, or loss of bounded unresolved ambiguity.

### 7.8 Resource / L4 plane

Failures in energy, time, memory, privilege, thermal, or irreversibility budgets.

### 7.9 Anti-echo / self-edit plane

Failures caused by recursive self-generation, self-certifying candidate inflation, or Slot B overwriting Slot A.

---

## 8. Degradation-State Ladder

ARQ implementations SHALL declare degradation states at least equivalent to the following.

### 8.1 State registry

| State | Short name | Meaning | Promotion authority | Corrective authority | Logging authority |
|---|---|---|---:|---:|---:|
| `NORMAL` | `DG0` | Full policy-compliant ARQ operation | full, subject to `G_promote` | full, within budgets | full |
| `LIMITED` | `DG1` | Non-critical assumptions weakened; authority reduced | blocked or narrowed by policy | allowed if trust-valid | full |
| `QUARANTINED` | `DG2` | Event path or class is isolated pending review | blocked | narrow / local only | full |
| `REVIEW_ONLY` | `DG3` | Observation and review continue; no privileged mutation | blocked | blocked except passive observation | full |
| `DEGRADED_CONTROL` | `DG4` | Corrective action narrowed; logging and safe persistence remain | blocked | limited to safe local actions | full |
| `LOG_ONLY` | `DG5` | Event intake possible, but no suppression/promotion authority remains | blocked | blocked | full |
| `FAIL_CLOSED` | `DG6` | Normal ARQ semantics invalid; only safe persistence and recovery hooks remain | blocked | blocked except emergency-safe persistence | minimum required |
| `RECOVERY_PENDING` | `DG7` | Preconditions for re-entry being verified; future authority not yet restored | blocked | blocked except recovery checks | required recovery logging |

### 8.2 Dominance order

The authority order SHALL be interpreted as:

`FAIL_CLOSED` > `RECOVERY_PENDING` > `LOG_ONLY` > `DEGRADED_CONTROL` > `REVIEW_ONLY` > `QUARANTINED` > `LIMITED` > `NORMAL`

If multiple conditions apply, the system SHALL enter the **most restrictive** required state.

### 8.3 Hard rule

No implementation MAY claim `NORMAL` or equivalent if a required hard gate has already failed in the current path.

---

## 9. Failure-Mode Registry

The following canonical failure modes are defined for ARQ v0.2.

### 9.1 Summary table

| Code | Name | Plane | Default target state |
|---|---|---|---|
| `FM-01` | Boundary missing or mismatched | boundary | `FAIL_CLOSED` for privileged paths; else `LOG_ONLY` |
| `FM-02` | Epoch invalid / expired / drifted | epoch | `FAIL_CLOSED` |
| `FM-03` | Witness chain break | witness | `FAIL_CLOSED` for promotion-capable path |
| `FM-04` | Controller integrity loss | controller | `DEGRADED_CONTROL` or `FAIL_CLOSED` |
| `FM-05` | Privilege envelope invalid / drifted | resource / trust | `LIMITED` or `FAIL_CLOSED` |
| `FM-06` | Rollback pre-image missing when required | controller / lifecycle | `REVIEW_ONLY` or `FAIL_CLOSED` |
| `FM-07` | Queue overflow / latency ceiling breach | queue | `LOG_ONLY` or `FAIL_CLOSED` |
| `FM-08` | Anomaly inflation / classifier instability | valuation | `QUARANTINED` or `REVIEW_ONLY` |
| `FM-09` | Anti-echo breach / recursive self-generation | anti-echo | `QUARANTINED` |
| `FM-10` | Review window expiry without completion | lifecycle | `rejected` or `LOG_ONLY` |
| `FM-11` | Contradictory observations / unresolved challenge | lifecycle / witness | `REVIEW_ONLY` or `QUARANTINED` |
| `FM-12` | Premature promotion attempt | lifecycle / privilege | `FAIL_CLOSED` for promotion path |
| `FM-13` | Lineage loss on retirement / compaction | lifecycle / witness | `REVIEW_ONLY` or `FAIL_CLOSED` |
| `FM-14` | Memory / commit budget exhaustion | resource | `LOG_ONLY` or `FAIL_CLOSED` |
| `FM-15` | Thermal / power / irreversibility breach | L4 | `DEGRADED_CONTROL` or `FAIL_CLOSED` |
| `FM-16` | Quantum trusted-boundary drift | boundary / epoch | `FAIL_CLOSED` |
| `FM-17` | Recovery oscillation / repeated reopen-fail cycle | recovery | `QUARANTINED` or prolonged `FAIL_CLOSED` |
| `FM-18` | Schema-malformed critical record | witness / schema | `FAIL_CLOSED` for affected authority path |

---

## 10. Detailed Failure Modes

### 10.1 `FM-01` Boundary missing or mismatched

A boundary failure occurs when:

- no valid `BR` exists for the referenced `boundary_id`;
- the event references a boundary not declared for the active profile;
- the observed component path lies outside the declared boundary;
- the profile attempts promotion from undeclared external context.

**Mandatory response:**

- privileged suppression and promotion MUST be denied;
- the event MUST degrade to `LOG_ONLY` at most;
- if the path had promotion-capable authority, the system MUST emit `FCR` and enter `FAIL_CLOSED` for that path.

**Minimum record set:** `AC` + `FCR` or denial `PDR`.

### 10.2 `FM-02` Epoch invalid / expired / drifted

An epoch failure occurs when:

- current time exits epoch validity interval;
- attestation invalidation was emitted;
- calibration drift exceeds policy threshold;
- trust-anchor rotation is unresolved;
- quantum boundary assumptions changed without a new valid epoch.

**Mandatory response:**

- `A_valid = 0`;
- `τ` for privileged actions MUST collapse accordingly;
- the implementation MUST enter `FAIL_CLOSED` or a declared narrower safe state.

**Minimum record set:** `ER` + `FCR`.

### 10.3 `FM-03` Witness chain break

A witness failure occurs when:

- `prev_record_hash` continuity fails;
- required source records cannot be retrieved;
- signatures or canonical payload hashes do not verify;
- required record bundle for current lifecycle state is incomplete.

**Mandatory response:**

- promotion authority MUST be removed immediately;
- current candidate/provisional path MUST stop advancing;
- if the broken chain affects already-promoted authority, the affected artifact MUST be quarantined or reopened via `LMR` + `RR`.

**Minimum record set:** `CHR` or `RR` + `FCR` if hard-gate path.

### 10.4 `FM-04` Controller integrity loss

A controller failure occurs when:

- signed controller-state cannot be verified;
- applied action differs materially from recorded action;
- the actuator path is unavailable or non-replayable;
- corrective action cannot be shown to have happened as claimed.

**Mandatory response:**

- `C_valid = 0` for the affected path;
- suppression authority MUST shrink to safe local actions only;
- if no safe local action remains, enter `FAIL_CLOSED`.

**Minimum record set:** `CAR` + `FCR` or `RR`.

### 10.5 `FM-05` Privilege envelope invalid / drifted

A privilege failure occurs when:

- required privilege token is missing, expired, revoked, malformed, or scope-mismatched;
- profile-specific privilege ceiling is exceeded;
- privilege was granted under an invalid epoch;
- role mismatch exists between issuer and requested action.

**Mandatory response:**

- action MUST be denied;
- promotion authority MUST be blocked;
- implementation SHOULD degrade at least to `LIMITED`, and MUST enter `FAIL_CLOSED` if the action was already in flight and cannot be cleanly denied.

**Minimum record set:** `PDR`; `FCR` if hard denial late in path.

### 10.6 `FM-06` Rollback pre-image missing when required

A rollback failure occurs when policy requires `R1`, `R2`, `R3`, or `R4` rollback semantics but:

- no valid pre-image exists;
- predecessor hash cannot be resolved;
- snapshot integrity fails;
- Slot A cannot be reconstructed.

**Mandatory response:**

- the path MUST enter `REVIEW_ONLY` or `FAIL_CLOSED` depending on profile criticality;
- Slot B SHALL NOT continue mutating state;
- candidate or provisional authority MUST freeze.

**Minimum record set:** `CAR` or `LMR` + `FCR`/`RR`.

### 10.7 `FM-07` Queue overflow / latency ceiling breach

A queue failure occurs when:

- pending events exceed declared `K_queue`;
- event payload exceeds `B_event_max`;
- bounded review windows cannot be serviced in time;
- classifier or witness append latency breaks profile ceiling.

**Mandatory response:**

- system SHALL degrade at least to `LOG_ONLY` for new events;
- profile MAY permit dropping to `REVIEW_ONLY` for existing candidates;
- if witness continuity cannot be preserved, transition to `FAIL_CLOSED`.

**Minimum record set:** `AC` + `FCR` or overflow `RR`/`LMR` according to implementation.

### 10.8 `FM-08` Anomaly inflation / classifier instability

A valuation failure occurs when:

- `A_anom` or `P_anom` exceeds profile threshold persistently;
- score oscillation or instability exceeds declared tolerance;
- Slot B valuation repeatedly exceeds Slot A without new external evidence;
- policy weights drift outside declared update discipline.

**Mandatory response:**

- affected events MUST enter `QUARANTINED` or `REVIEW_ONLY`;
- direct promotion MUST be blocked;
- the classifier path SHOULD be revalidated or recalibrated before re-entry.

**Minimum record set:** `AC` + `OWR` and, where needed, `CHR`/`RR`.

### 10.9 `FM-09` Anti-echo breach / recursive self-generation

An anti-echo failure occurs when:

- `X_echo = 1` under declared anti-echo policy;
- the candidate is substantially derived from recent self-generated material without new witnessable external constraint;
- Slot B reinterpretation is being treated as independent confirmation.

**Mandatory response:**

- event MUST be quarantined;
- direct transition to `confirmed_EA` is prohibited;
- the path MAY remain `candidate_artifact` under quarantine if policy allows, else it MUST be rejected or log-only.

**Minimum record set:** `AC` + `OWR` or `RR`.

### 10.10 `FM-10` Review window expiry without completion

A review failure occurs when:

- observation window closes without sufficient `OR` / `RR` support;
- required review signatures do not arrive in time;
- challenge is unresolved when policy requires resolution before promotion.

**Mandatory response:**

- candidate/provisional path MUST demote to `rejected` or `log_only` according to policy;
- authority MUST NOT remain in limbo as if silence were confirmation.

**Minimum record set:** `OWR` + `RR` and optional `LMR`.

### 10.11 `FM-11` Contradictory observations / unresolved challenge

A contradiction failure occurs when:

- observations materially conflict without resolution;
- challenge records remain open beyond tolerance;
- witness evidence supports mutually incompatible promotion narratives.

**Mandatory response:**

- path MUST enter `REVIEW_ONLY` or `QUARANTINED`;
- no promotion may proceed until `RR` resolves the contradiction or the path is rejected.

**Minimum record set:** `CHR` + `RR`.

### 10.12 `FM-12` Premature promotion attempt

A promotion failure occurs when a system attempts to bind or expose `confirmed_EA` authority while:

- `G_promote = 0`;
- required witness bundle is incomplete;
- required co-signature is missing;
- path is still in candidate/provisional state;
- the event remains under anti-echo quarantine.

**Mandatory response:**

- promotion MUST be denied;
- the implementation SHOULD emit denial and MAY enter `FAIL_CLOSED` for the promotion path if the attempt indicates authority bypass.

**Minimum record set:** `PDR` + `RR` + `FCR` if bypass severity is high.

### 10.13 `FM-13` Lineage loss on retirement / compaction

A lineage failure occurs when:

- `retired_EA` or `compacted_EA` cannot be traced to source `confirmed_EA`;
- predecessor set is missing or inconsistent;
- compaction creates authority without preserving ancestry.

**Mandatory response:**

- the affected archival object MUST enter `REVIEW_ONLY`;
- if active authority depends on the broken lineage, authoritative use MUST stop until resolved.

**Minimum record set:** `LMR` + `CHR`/`RR`.

### 10.14 `FM-14` Memory / commit budget exhaustion

A resource failure occurs when:

- no further bounded commits are allowed under `M2`;
- retained-artifact path exceeds commit budget;
- authoritative persistent-state headroom is exhausted;
- compaction/retirement policy has not restored sufficient headroom.

**Mandatory response:**

- new promotions MUST be blocked;
- the system MAY continue `LOG_ONLY` ingestion if witness capacity remains intact;
- if even safe logging cannot continue within profile bounds, enter `FAIL_CLOSED`.

**Minimum record set:** `PDR` or `RR`; `FCR` if hard stop.

### 10.15 `FM-15` Thermal / power / irreversibility breach

An L4 failure occurs when:

- thermal envelope is exceeded;
- power path becomes unstable;
- irreversibility budget is exhausted;
- safe corrective actuation would itself violate the declared physical envelope.

**Mandatory response:**

- corrective authority MUST narrow immediately;
- implementation SHALL enter `DEGRADED_CONTROL` and, if safe persistence is threatened, `FAIL_CLOSED`.

**Minimum record set:** `CAR` + `FCR` and any local platform anomaly record.

### 10.16 `FM-16` Quantum trusted-boundary drift

A quantum boundary failure occurs when:

- trusted ancilla map is no longer admissible;
- declared `M5` boundary dimensions or topology change during a live epoch;
- calibration or environmental drift invalidates the trusted-boundary assumptions.

**Mandatory response:**

- `B_valid = 0` and/or `A_valid = 0` for quantum promotion claims;
- usable-entanglement claims MUST lose authority until a new valid epoch is established;
- quantum promotion path MUST enter `FAIL_CLOSED`.

**Minimum record set:** `ER` + `FCR` + relevant `AC`/`RR`.

### 10.17 `FM-17` Recovery oscillation / repeated reopen-fail cycle

A recovery failure occurs when:

- the system repeatedly leaves `FAIL_CLOSED` and re-enters it within a short bounded horizon;
- trust or witness conditions flap without stabilizing;
- the same fault cluster reappears after nominal recovery without new remediation evidence.

**Mandatory response:**

- prolong the degraded or fail-closed interval;
- quarantine affected authority path;
- require stronger review before future re-entry.

**Minimum record set:** repeated `FCR` + `RR` / recovery records.

### 10.18 `FM-18` Schema-malformed critical record

A schema failure occurs when a required critical record is malformed or semantically incomplete such that replayable meaning is lost.

Examples include:

- missing `payload_hash` or `record_sig` on trust-bearing records;
- missing lifecycle stage field on `LMR`;
- malformed `epoch_id` or `boundary_id` on records where they are mandatory;
- critical field redaction that destroys replayability.

**Mandatory response:**

- affected authority path MUST fail closed or be denied;
- malformed records SHALL NOT be repaired silently in place.

**Minimum record set:** denial `PDR` or `FCR`; corrective mutation as new record only.

---

## 11. Safe Degradation Actions

The following degradation actions are canonical.

### 11.1 Action registry

| Code | Action | Meaning |
|---|---|---|
| `SD-01` | Authority shrink | Reduce allowed action set while keeping logging alive |
| `SD-02` | Promotion freeze | Block candidate/provisional advancement and EA binding |
| `SD-03` | Quarantine lane | Keep event visible but non-authoritative |
| `SD-04` | Slot B rollback | Revert shadow/self-edit path to Slot A |
| `SD-05` | Review-only mode | Permit observation and challenge, deny mutation |
| `SD-06` | Log-only mode | Permit bounded intake/logging only |
| `SD-07` | Degraded control | Permit only safe local corrective actions |
| `SD-08` | Fail-closed | Stop all non-safe state-changing operations |
| `SD-09` | Recalibration required | Require new epoch / attestation before re-entry |
| `SD-10` | Human anchor approval required | Raise human-signature threshold before further progress |

### 11.2 Mandatory precedence

If a failure requires both quarantine and rollback, rollback SHALL happen first where state integrity depends on it, and quarantine SHALL remain in effect afterwards.

If a failure requires both review-only and fail-closed, fail-closed SHALL dominate.

---

## 12. Mapping Failure Modes to Degradation Actions

| Failure mode | Minimum action set |
|---|---|
| `FM-01` | `SD-02` + `SD-06` or `SD-08` |
| `FM-02` | `SD-01` + `SD-08` + `SD-09` |
| `FM-03` | `SD-02` + `SD-08` |
| `FM-04` | `SD-01` + `SD-07`, escalate to `SD-08` if unrecoverable |
| `FM-05` | `SD-01` + deny path; maybe `SD-08` |
| `FM-06` | `SD-04` + `SD-05`, maybe `SD-08` |
| `FM-07` | `SD-06`; if witness continuity breaks then `SD-08` |
| `FM-08` | `SD-03` + `SD-05` |
| `FM-09` | `SD-03` + `SD-02` |
| `FM-10` | `SD-02` + reject/demote path |
| `FM-11` | `SD-05` + `SD-03` |
| `FM-12` | deny + `SD-02`; severe bypass => `SD-08` |
| `FM-13` | `SD-05` + active-authority freeze |
| `FM-14` | `SD-02` + `SD-06`; maybe `SD-08` |
| `FM-15` | `SD-07`, then `SD-08` if envelope remains violated |
| `FM-16` | `SD-02` + `SD-08` + `SD-09` |
| `FM-17` | `SD-03` or prolonged `SD-08` + stronger review |
| `FM-18` | deny affected path + `SD-08` if critical |

---

## 13. Rollback and Slot Discipline Under Failure

### 13.1 Canonical rule

If Slot B is active and any of the following occurs:

- trust invalidation;
- anti-echo trigger;
- missing rollback pre-image;
- contradictory observation path;
- queue overflow threatening replayability;
- promotion-bypass attempt;

then the system SHALL execute `Rollback(B→A)` automatically and record the rollback.

### 13.2 What rollback does **not** mean

Rollback SHALL NOT erase the witness trail of the failed or quarantined path.

Rollback means:

- restore operational authority to the last-known-good Slot A state;
- preserve Slot B history as replayable evidence;
- block Slot B from silently overwriting canonical memory.

### 13.3 Minimum record set for rollback under failure

A rollback induced by failure SHOULD emit at least:

- one `CAR` or equivalent rollback-action record;
- one `LMR` if lifecycle state changed;
- one `FCR` if fail-closed was entered;
- one `RR` if review resolution is already available.

---

## 14. Recovery Entry and Re-Entry Discipline

### 14.1 From `FAIL_CLOSED` to `RECOVERY_PENDING`

A system MAY leave `FAIL_CLOSED` only if all of the following hold for the path being restored:

1. boundary validity is re-established;
2. epoch validity is re-established or explicitly rotated;
3. witness chain continuity is available for the recovery path;
4. required privilege envelope is re-issued;
5. rollback target or stable safe state is identified;
6. queue/backlog is below declared safe threshold;
7. required recovery records are emitted.

### 14.2 From `RECOVERY_PENDING` to `NORMAL` or `LIMITED`

A system MAY return to `NORMAL` only if no active hard-gate failure remains.

A system SHOULD return first to `LIMITED` if:

- the underlying fault was recent;
- a recalibration has not yet completed long enough observation;
- the profile declares post-recovery probation.

### 14.3 No retroactive cleansing

Recovery SHALL NOT retroactively promote or sanitize events that occurred during invalid operation.

Those events remain:

- `log_only`,
- `rejected`,
- quarantined,
- or subject to explicit re-review from source records only.

---

## 15. Failure Precedence Rules

### 15.1 Hard gates dominate soft quality issues

The following failures SHALL be treated as hard-gate failures for privileged operation:

- `FM-01` boundary missing or mismatched;
- `FM-02` epoch invalid;
- `FM-03` witness chain break;
- `FM-12` premature promotion attempt when authority bypass is real;
- `FM-16` quantum trusted-boundary drift;
- `FM-18` malformed critical witness-bearing record.

### 15.2 Trust loss beats score quality

A high `V_trust` or low `A_anom` SHALL NOT override invalid boundary, invalid epoch, broken witness continuity, or missing promotion authority.

### 15.3 Anti-echo beats self-congratulation

If `X_echo = 1`, a path SHALL be treated as quarantined even if the score is numerically attractive.

### 15.4 Resource reality beats rhetorical continuity

If power, thermal, memory, latency, or irreversibility ceilings are breached, the implementation SHALL degrade according to L4 rather than preserve the illusion of a continuous learning path.

---

## 16. Profile-Specific Overlays

### 16.1 `ARQ-MEM`

Critical failure focus:

- rollback pre-image absence;
- authoritative memory commit saturation;
- lineage break during compaction;
- candidate/provisional memory silently treated as confirmed.

Profile-specific rule:

If authoritative memory integrity is uncertain, `ARQ-MEM` SHALL degrade at least to `REVIEW_ONLY`, and promotion SHALL freeze immediately.

### 16.2 `ARQ-PLANNER`

Critical failure focus:

- action graph instability;
- plan branch explosion beyond queue limits;
- inability to map corrective action to attested controller record;
- simulation branch treated as executed fact.

Profile-specific rule:

When planner integrity weakens, execution authority SHALL shrink before interpretive authority does. Planning MAY continue in shadow, but real execution MUST narrow or stop.

### 16.3 `ARQ-RAG`

Critical failure focus:

- retrieval witness mismatch;
- context assembly overflow;
- source churn during active review;
- synthetic rephrasing treated as new external evidence.

Profile-specific rule:

`ARQ-RAG` SHALL quarantine self-derived retrieval loops and MUST NOT promote context-assembly novelty without reconstructible source references.

### 16.4 `ARQ-VISION`

Critical failure focus:

- scene interpretation instability;
- OCR leakage or over-rich attributes;
- repeated same-frame semantic inflation;
- disclosure path bypass in visual-to-memory promotion.

Profile-specific rule:

`ARQ-VISION` SHOULD prefer quarantine over promotion when the same visual source repeatedly yields materially different semantics within one review horizon.

### 16.5 Quantum trusted boundary overlay

Critical failure focus:

- trusted ancilla map drift;
- state estimate irreproducibility;
- usable-entanglement claim outside valid boundary;
- calibration collapse during live valuation.

Profile-specific rule:

When `M5` assumptions fail, quantum promotion authority MUST collapse immediately even if local score terms remain attractive.

---

## 17. Minimum Normative Invariants

A conformant implementation SHALL satisfy all of the following:

1. Every declared hard-gate failure removes the corresponding authority.
2. Promotion authority shrinks before service advertises normality.
3. Broken witness continuity blocks promotion.
4. Invalid epoch blocks promotion and trust-sensitive privilege.
5. Anti-echo quarantine blocks direct confirmed promotion.
6. Slot B SHALL NOT silently overwrite Slot A under failure.
7. Review expiry does not count as confirmation.
8. Recovery does not retroactively sanitize invalid operation.
9. Fail-closed dominates convenience.
10. Degradation states are explicit and replayable.
11. A malformed critical record cannot be silently repaired in place.
12. Lineage loss blocks authority.
13. Repeated recovery oscillation triggers stricter re-entry.
14. Resource exhaustion removes authority even if no contradiction is yet visible.
15. A path may continue logging after degradation only if witness continuity still holds.

---

## 18. Conformance Checklist

An implementation claiming conformance with this document SHOULD be able to answer “yes” to all of the following:

- Can you name the degradation state the system entered and why?
- Can you show which authority was removed first?
- Can you show the exact records emitted for a fail-closed transition?
- Can you prove that Slot B rolled back instead of silently overwriting Slot A?
- Can you show why a quarantined event remained quarantined?
- Can you distinguish review-only, log-only, degraded-control, and fail-closed in API and storage?
- Can you show what conditions were checked before recovery?
- Can you prove that a recovery did not retroactively legitimize invalid-period events?

If not, the implementation is not yet failure-complete ARQ.

---

## 19. Explicit and Hidden Bridges

### 19.1 Explicit bridge

`c = a + b` remains stable only if failure in `b` does not silently rewrite `c` under the rhetorical protection of continuity. This document is that bridge: it forces authority to contract under stress so that `a` remains responsible for what `c` is allowed to remember or do.

### 19.2 Hidden bridge #1 — SER / survival physiology

SER separates interaction governance from survival physiology. This document carries that split into ARQ failure semantics: witness and promotion authority may collapse while the entity still survives in safe persistence. Surviving is not the same as remaining authorized.

### 19.3 Hidden bridge #2 — L4 Witness / incident discipline

L4 Witness says that outcomes matter only when they remain replayable and challengeable. This document adds the inverse form: once replayability or challengeability breaks, authority must shrink. Failure is therefore not just a technical symptom; it is a witness-authority event.

### 19.4 Hidden bridge #3 — Beacon / continuity under stress

Beacon asks whether continuity remains recognizable under challenge. A system that cannot name, log, and bound its own degraded states loses continuity credibility. Safe degradation is therefore part of operational identity, not just fault handling.

### 19.5 Hidden bridge #4 — Hardware perimeter / side-channel reality

The L4 hardware perimeter notes that real systems leak through radios, power, heat, peripherals, and environmental drift. This document is the control complement: when those leaks or drifts break assumptions, ARQ must degrade rather than pretend its higher-level semantics remain intact.

---

## 20. Earth Paragraph

In engineering terms this is the difference between a machine that admits it is sick and one that keeps smiling while the bolts back out. A good plant controller drops authority when sensors drift, logs the bad interval, rolls back the unsafe branch, and waits for calibration before touching production again. In anatomy it is the same: fever, inflammation, reduced activity, and scar isolation are not “failures of life”; they are how an organism refuses to let one local disturbance rewrite the whole body. ARQ safe degradation plays the same role. It is the protocol by which a long-lived entity says: “I may continue existing, but I do not currently have the right to trust myself in the usual way.”

---

## 21. Closing Statement

A persistent entity that learns from deviation must also know how to become smaller under stress.

That is the whole point of this document.

Not every fault is catastrophic. Not every contradiction is fatal. But every lost assumption has a price, and the first price is authority.

ARQ v0.2 is therefore not complete unless it can do three hard things when things go wrong:

> name the failure,  
> shrink the authority,  
> preserve the trail.

Anything softer becomes drift with paperwork.
