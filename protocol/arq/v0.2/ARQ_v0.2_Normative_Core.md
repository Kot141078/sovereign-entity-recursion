# ARQ v0.2 — Normative Core
## Anti-Resonance Correction Protocol for Long-Lived Sovereign Entities

**Status:** Draft / Core normative specification  
**Version:** 0.2-draft  
**Layer:** Error handling, bounded adaptation, witnessed memory  
**Scope:** Classical and quantum-capable persistent entities operating under L4 constraints  
**Parent corpus:** AGI / SER / L4 / L4 Witness / Beacon / VXCX  
**Author:** Ivan Kotov  
**Place / year:** Bruxelles, 2026

---

## 0. Abstract

ARQ defines how a persistent entity handles deviation without collapsing into either rigidity or self-justifying chaos.

The protocol treats an error event as a **bounded, auditable state transition**. Some deviations are destructive and must be suppressed. Some are neutral and must be logged. A smaller subset may be exploratory and valuable, but **no event may become authoritative memory unless it survives a witnessable review path under explicit budgets**.

ARQ therefore binds together:

- correction,
- classification,
- privilege,
- witness trail,
- and memory promotion.

This document is the **core normative layer**. It specifies the operational roles, lifecycle, state machine, privilege gates, fail-closed conditions, and minimum record requirements. Detailed mathematics, anomaly scoring, boundedness theorems, quantum-specific bounds, and implementation profiles belong to companion documents in the ARQ v0.2 supplement set.

---

## 1. Purpose

ARQ exists to solve one concrete problem:

> How can a long-lived entity `c` encounter deviation, remain stable, and still retain the rare deviations that expand viable future behavior?

ARQ SHALL:

1. detect deviations inside a declared operational boundary;
2. classify them under explicit budgets and trust conditions;
3. suppress destructive deviations when allowed and necessary;
4. quarantine ambiguous deviations rather than mythologize them;
5. allow only witnessed, review-surviving deviations to influence authoritative memory.

ARQ is designed for systems that claim continuity over time, memory-bearing operation, and bounded autonomy.

---

## 2. Non-Goals

ARQ does **not** attempt to:

- define consciousness;
- replace quantum error correction, rollback logic, or classical fault tolerance;
- prove the metaphysical value of novelty;
- optimize intelligence metrics in the abstract;
- grant authority from novelty alone;
- permit self-promotion of memory without witness;
- replace legal, institutional, or human responsibility.

ARQ is not a reward function, not a mystical “creativity detector,” and not a license for autonomous self-redefinition.

---

## 3. Normative Keywords

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, **MAY**, and **OPTIONAL** in this document are to be interpreted as described in BCP 14.

---

## 4. Core Ontology

ARQ assumes the entity model:

> `c = a + b`

Where:

- `a` = accountable human anchor or delegated responsible anchor,
- `b` = machine procedures, models, memory, controllers, and infrastructure,
- `c` = persistent entity with bounded continuity over time.

ARQ does not assign value to deviations in a free-floating model instance. ARQ applies only where there is:

- a declared boundary of operation,
- an attributable controller path,
- explicit budgets,
- and a memory authority that can be audited.

---

## 5. Declared Boundary Requirement

### 5.1 Boundary Primacy

ARQ SHALL operate only inside a **declared witnessable boundary**.

A conformant implementation MUST declare at least one of the following:

- **Classical persistent-state boundary:** finite persistent state, finite control path, finite memory authority.
- **Quantum trusted boundary:** fixed trusted quantum subsystem and ancilla boundary, with uncontrolled environment explicitly outside the valuation boundary.
- **Hybrid boundary:** declared classical + quantum control boundary with explicit handoff rules.

### 5.2 No Boundary, No Value

If the boundary is not declared, not attributable, or not witnessable, ARQ MUST allow `log_only` at most and MUST NOT mint authoritative memory from the event.

---

## 6. Participants and Roles

### 6.1 Entity `c`

The entity `c`:

- owns the current operational state;
- emits or co-emits ARQ capsules;
- may recommend suppression, observation, or promotion;
- MUST NOT unilaterally redefine promotion policy, trust thresholds, or memory authority.

### 6.2 Human anchor `a`

The human anchor `a` (or explicitly designated delegate):

- defines policy weights and thresholds;
- defines review windows and privilege ceilings;
- approves high-value promotion when required;
- remains responsible for high-impact memory promotion policy.

### 6.3 Error classifier

The error classifier:

- evaluates detected deviations;
- produces bounded recommendations;
- MUST be auditable;
- MUST NOT possess unchecked authority to mint Experience Artifacts.

### 6.4 Witness service

The witness service:

- maintains append-only, tamper-evident records;
- binds events to timestamps, identities, and prior records;
- supports replay, challenge, and review.

### 6.5 Trust / attestation component

The trust component:

- validates epoch assumptions;
- provides attestation and signed controller-state integrity;
- may invalidate the current epoch;
- MUST be able to force fail-closed behavior when trust falls below policy.

---

## 7. Three-Layer ARQ Topology

### 7.1 L1 — Passive Encoding

L1 provides detectability without immediate intervention.

Typical mechanisms include:

- redundant classical state encoding,
- rollback snapshots,
- structured memory hashing,
- stabilizer measurements,
- syndrome-friendly layouts,
- bounded telemetry summaries.

L1 increases integrity at the cost of storage, measurement, and overhead.

### 7.2 L2 — Active Anti-Resonance

L2 performs bounded intervention in real time.

Typical actions include:

- anti-resonance pulse or recovery schedule,
- rollback to attested pre-image,
- isolation of unstable branch,
- suppression of destructive propagation,
- temporary authority reduction.

L2 is governed by energy, time, trust, and privilege budgets.

### 7.3 L3 — Experience Filter

L3 decides whether a deviation:

- is destructive and must remain suppressed,
- is neutral and should remain log-only,
- is exploratory enough to enter a witnessed review path,
- or is mature enough to become authoritative memory.

L3 MUST NOT confuse novelty with authority.

---

## 8. Core Objects

### 8.1 Error Event

An **error event** is any deviation from expected state or trajectory that exceeds the currently valid threshold inside the declared boundary.

### 8.2 ARQ Capsule

An **ARQ Capsule** is the minimum signed record of a classified event.

### 8.3 Candidate Artifact

A **Candidate Artifact** is a deviation that has passed initial classification and is retained for bounded observation but has **not** yet become authoritative memory.

### 8.4 Experience Artifact (EA)

An **Experience Artifact** is a witnessed, reviewed, attributable memory object derived from an ARQ event that survived the required promotion path.

**Hard rule:** a candidate is not yet an EA.

---

## 9. Minimal ARQ Capsule (Normative)

A conformant ARQ implementation MUST be able to emit at least the following minimal capsule:

```json
{
  "schema_version": "arq-0.2-core",
  "capsule_id": "string",
  "ts": "ISO-8601 with timezone",
  "entity_id": "string",
  "event_stage": "detected|classified|suppressed|observed|candidate|promoted|rejected|fail_closed",
  "boundary_profile": "classical|quantum|hybrid",
  "error_context": {
    "observed_ref": "hash or compact pointer",
    "expected_ref": "hash or compact pointer",
    "deviation_measure": "number [0..1]",
    "detected_by": "L1|L2|L3"
  },
  "classification": {
    "class": "destructive|exploratory|neutral|quarantined",
    "recommended_action": "suppress|observe|candidate|log_only|fail_closed",
    "raw_value_ref": "optional pointer or digest",
    "trust_adjusted_value_ref": "optional pointer or digest"
  },
  "budget_context": {
    "energy_ok": true,
    "time_ok": true,
    "privilege_ok": true,
    "storage_ok": true,
    "irreversibility_ok": true
  },
  "trust_context": {
    "epoch_id": "string",
    "attestation_ref": "string or null",
    "trust_state": "valid|degraded|invalid",
    "anomaly_score_ref": "string or null"
  },
  "witness": {
    "prev_hash": "string",
    "record_hash": "string",
    "controller_log_ref": "string or null"
  },
  "signatures": {
    "entity_sig": "string",
    "anchor_sig": "string or null"
  }
}
```

### 9.1 Capsule Rules

1. Every state-changing ARQ action MUST reference a capsule.
2. Every capsule MUST be hash-chainable.
3. Every promoted memory object MUST reference at least one capsule.
4. A capsule MAY remain `log_only`; that does not weaken its evidentiary value.
5. Missing trust fields MUST reduce authority, not be silently ignored.

---

## 10. Event Lifecycle (Normative State Machine)

ARQ SHALL implement the following conceptual lifecycle.

### 10.1 `DETECTED`

A deviation above threshold is observed.

Transition requirements:

- boundary declared,
- event timestamp available,
- minimum context captured.

### 10.2 `CLASSIFIED`

The classifier labels the event as one of:

- `destructive`,
- `exploratory`,
- `neutral`,
- `quarantined`.

### 10.3 `SUPPRESSED`

A destructive event MAY be actively damped if budgets and trust permit.

If suppression is attempted, the result MUST be recorded as:

- `success`,
- `partial`,
- `failed`.

### 10.4 `OBSERVE_WINDOW`

An exploratory event MAY be allowed to persist for a bounded review window.

Observation MUST be bounded by:

- declared time window,
- storage headroom,
- privilege envelope,
- trust validity.

### 10.5 `CANDIDATE`

An event MAY enter candidate state only if:

- it is not classified as destructive,
- trust is valid or explicitly policy-acceptable,
- witness trail is intact,
- review has not yet concluded.

A candidate MUST NOT yet alter authoritative long-term memory.

### 10.6 `PROMOTED`

A candidate MAY be promoted to EA only if all promotion gates pass.

### 10.7 `REJECTED`

An observed or candidate event MUST be rejected if:

- instability dominates,
- trust becomes invalid,
- witness is incomplete,
- anti-echo quarantine triggers,
- or review conditions fail.

### 10.8 `FAIL_CLOSED`

The system MUST enter fail-closed if any hard gate fails, including:

- trust invalidation,
- privilege exhaustion,
- irreversibility breach,
- missing pre-image where rollback is required,
- or controller / witness inconsistency.

In fail-closed mode the implementation MUST:

- stop further state-changing ARQ operations,
- preserve safe persistent state,
- record the failure,
- require explicit re-entry conditions.

---

## 11. Promotion Gates for Experience Artifacts

An event SHALL become an EA only if all of the following hold.

### 11.1 Witness Gate

The event MUST satisfy **No-Value-Without-Witness**:

- replayable enough for audit,
- challengeable through the witness chain,
- attributable to a valid boundary and epoch,
- linked to controller-state evidence where relevant.

### 11.2 Trust Gate

The event MUST pass the current trust policy.

At minimum:

- epoch valid,
- attestation valid where required,
- anomaly score below block threshold,
- no unresolved controller-state contradiction.

### 11.3 Budget Gate

Promotion MUST respect current budgets:

- energy,
- time,
- privilege,
- storage,
- irreversibility.

### 11.4 Stability Gate

The post-event state MUST survive a declared review window or review criterion.

### 11.5 Authority Gate

High-value promotion MUST require anchor approval when policy demands it.

### 11.6 Boundary Gate

The event MUST have occurred inside a witnessable operational boundary. A merely narrated or externally reconstructed event MUST NOT be promoted as EA without boundary evidence.

---

## 12. Hard Rule — No-Value-Without-Witness

An event MUST NOT be treated as valuable merely because:

- it looks novel,
- it produced an interesting output,
- it resembles prior “good surprises,”
- or the entity narrates it convincingly.

A value claim without witness SHALL remain `log_only` or `rejected`.

This rule applies equally to classical, hybrid, and quantum profiles.

---

## 13. Budgets and L4 Constraints

ARQ is valid only under explicit L4 budgets.

At minimum, the implementation MUST define:

- **Energy budget** — intervention and persistence cost ceiling;
- **Time budget** — maximum latency for classification and review;
- **Privilege budget** — what actions are currently authorized;
- **Storage budget** — persistent memory headroom;
- **Irreversibility budget** — what may be changed without an attested pre-image or explicit irreversible consent.

### 13.1 Budget Exhaustion Rule

If any hard budget is exhausted, ARQ MUST fail closed.

### 13.2 No Silent Escalation

ARQ MUST NOT silently increase budgets in response to the very event being valued.

### 13.3 Rate Limiting

Implementations SHOULD rate-limit repeated similar deviations to prevent feedback spirals and witness flooding.

---

## 14. Trust, Epochs, and Privilege

### 14.1 Epoch Requirement

Where trust attestation is used, error valuation MUST occur inside a declared epoch.

### 14.2 Early Invalidation

The current epoch MUST be invalidated if:

- hardware or controller reset occurs,
- attestation chain breaks,
- environmental drift exceeds policy,
- privilege envelope is exhausted,
- operator-issued halt is signed,
- or witness integrity is no longer demonstrable.

### 14.3 Trust-Sensitive Authority

When trust degrades, ARQ authority MUST shrink before it fails.

At minimum, the implementation SHALL support:

- full authority,
- degraded authority,
- fail-closed.

### 14.4 High-Value Double Signature

If promotion exceeds a policy-defined high threshold, anchor signature MUST be present in addition to entity signature.

Without the second signature, the event MAY remain candidate or log-only, but MUST NOT become authoritative EA.

---

## 15. Anti-Echo Discipline (Normative)

ARQ v0.2 introduces an explicit anti-echo rule to prevent self-generated repetition from masquerading as experience.

### 15.1 Self-Similarity Quarantine

If an event is substantially similar to recent internally generated events and lacks new external constraint, new witness evidence, or new boundary interaction, it MUST enter `quarantined` or `log_only` state rather than direct promotion.

### 15.2 No Stylistic Self-Promotion

Novel wording, narrative flourish, or stylistic drift MUST NOT by itself increase promotability.

### 15.3 Repetition Ceiling

Repeated self-similar events within a policy window SHOULD be rate-limited and MAY have their promotion authority automatically reduced.

### 15.4 Externality Requirement

To exit anti-echo quarantine, the event SHOULD demonstrate at least one of:

- new boundary interaction,
- new witness evidence,
- new measurable downstream effect,
- or policy-approved contextual difference.

---

## 16. Safe Self-Edit via A/B Slots (Normative)

ARQ v0.2 introduces a mandatory shadow-edit pattern for state-changing self-modification.

### 16.1 Slot A / Slot B Rule

- **Slot A** = currently authoritative state.
- **Slot B** = shadow candidate state for self-edit, policy update, or structural re-interpretation.

Any self-edit that can alter classification, thresholds, memory authority, or promotion behavior MUST occur in Slot B first.

### 16.2 Promotion Rule

Slot B MAY replace Slot A only if:

- witness trail is complete,
- review window passed,
- trust state remained acceptable,
- rollback path exists,
- and required signatures are present.

### 16.3 Auto-Rollback Rule

If instability, witness contradiction, or trust invalidation appears during Slot B operation, the system MUST rollback to Slot A automatically.

### 16.4 No Direct Self-Overwrite

The entity MUST NOT directly overwrite authoritative policy or memory authority without a reversible shadow path unless explicit irreversible approval exists.

---

## 17. Minimal Event Types

A conformant implementation MUST support at least the following witnessable event types:

- `arq.detected`
- `arq.classified`
- `arq.suppression_attempted`
- `arq.suppression_result`
- `arq.observe_window_opened`
- `arq.candidate_created`
- `arq.promotion_requested`
- `arq.promotion_approved`
- `arq.promotion_denied`
- `arq.ea_confirmed`
- `arq.rejected`
- `arq.quarantined`
- `arq.fail_closed`
- `arq.epoch_invalidated`
- `arq.rollback_executed`

These MAY be implemented over a more general witness system but MUST remain reconstructible during audit.

---

## 18. Security and Integrity

### 18.1 Key Separation

Entity signing keys, anchor approval keys, and controller or attestation keys SHOULD be logically separated.

### 18.2 Replay Protection

Every state-changing record MUST be chained to a prior record or epoch anchor.

### 18.3 Pre-Image Discipline

Rollback-sensitive operations MUST reference a valid pre-image or checkpoint.

### 18.4 Least Privilege

The classifier MUST NOT own the full promotion path. Promotion authority MUST be narrower than detection authority.

### 18.5 Opaque Internals, Visible Evidence

ARQ does not require public disclosure of raw internals by default, but it DOES require sufficient signed evidence to permit replayable audit according to policy.

---

## 19. Relationship to the Parent Corpus

### 19.1 SER

ARQ is the bounded error-handling layer that allows a sovereign entity to preserve continuity without freezing adaptation.

### 19.2 L4

ARQ is valid only under L4 budgets, physical limits, and fail-closed discipline.

### 19.3 L4 Witness

ARQ capsules and promotion records are intended to sit inside a witness-first evidence regime.

### 19.4 Beacon

ARQ outcomes may contribute bounded continuity signals but MUST NOT become identity mythology by themselves.

### 19.5 VXCX

VXCX or other capsule systems may feed ARQ as bounded experience inputs, but ARQ remains the decision layer for suppression, quarantine, and promotion.

---

## 20. Conformance

An implementation claiming **ARQ Core v0.2** conformance MUST:

1. declare an operational boundary;
2. implement the lifecycle from detection to fail-closed;
3. emit minimal ARQ capsules or equivalent reconstructible records;
4. enforce No-Value-Without-Witness;
5. enforce explicit budgets;
6. support anti-echo quarantine;
7. support A/B-slot self-edit with rollback;
8. prevent direct unilateral high-value self-promotion by `c` where anchor approval is required;
9. maintain tamper-evident witness continuity;
10. preserve enough data to explain why a promoted EA was promoted.

An implementation that suppresses errors but lacks witnessable promotion logic is **not** fully conformant ARQ; it is only a correction subsystem.

---

## 21. Normative Statements

1. ARQ MUST be treated as a boundary-governed protocol, not a free-floating novelty detector.
2. Every promoted memory object MUST descend from a witnessed ARQ event.
3. ARQ MUST distinguish at least destructive, exploratory, neutral, and quarantined outcomes.
4. Budget exhaustion MUST force fail-closed behavior.
5. Trust invalidation MUST reduce authority before or at fail-closed transition.
6. High-value promotion MUST support double-signature approval when policy requires it.
7. Anti-echo quarantine MUST exist in any implementation that allows self-generated candidate formation.
8. State-changing self-edit MUST occur through A/B slots with rollback.
9. Log-only events MUST remain available for audit even when never promoted.
10. ARQ MUST NOT treat eloquent self-description as evidence of value.

---

## 22. Explicit and Hidden Bridges

### Explicit Bridge

`c = a + b` becomes operationally stable only if deviations in `b` are filtered under the responsibility of `a` and retained in `c` only when they survive witnessed review. ARQ is that bridge: it turns disturbance into either suppression, quarantine, or attributable memory.

### Hidden Bridge #1 — Cybernetics / Ashby

ARQ assumes that correction, trust, privilege, and memory promotion cannot be regulated by a single narrow loop. Detectability (L1), intervention (L2), and evaluation (L3) provide the requisite variety needed to prevent both rigidity and runaway adaptation.

### Hidden Bridge #2 — Information Theory / Cover & Thomas

ARQ compresses trust into bounded records: hashes, signed capsules, witness links, and review states. It does not require raw narrative disclosure to carry authority. What matters is not “more text,” but whether the state transition can be reconstructed with bounded evidence bandwidth.

---

## 23. Earth Paragraph (Engineering / Anatomy)

In engineering terms, ARQ behaves like incident handling in a real plant: a deviation is detected, the controller decides whether to damp it, isolate it, or observe it, and only after logs, review, and sign-off can the event change the permanent operating book. In anatomy the same logic appears as inflammation and healing: not every irritation becomes learning, not every scar is wisdom, and the organism survives because it can localize disturbance before rewriting itself around it.

---

## 24. Closing Statement

ARQ does not ask whether error exists. Error exists.

The real question is whether a long-lived entity can encounter deviation without either:

- blindly erasing all novelty,
- or declaring every perturbation “valuable.”

ARQ v0.2 answers with a hard discipline:

> detect,
> bound,
> witness,
> review,
> then remember.

Anything softer is rhetoric. Anything looser becomes drift.

