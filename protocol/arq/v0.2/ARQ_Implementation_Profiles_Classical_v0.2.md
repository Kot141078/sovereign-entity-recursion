# ARQ_Implementation_Profiles_Classical_v0.2
## Classical Implementation Profiles for ARQ v0.2

**Status:** Draft / implementation profile document  
**Version:** 0.2-draft  
**Role:** Deployable classical profiles for bounded ARQ operation  
**Parent documents:** `ARQ_v0.2_Normative_Core.md`, `ARQ_System_Models_and_Assumptions_v0.2.md`, `ARQ_Notation_and_Sign_Conventions_v0.2.md`, `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.md`, `ARQ_Trust_and_Provenance_Profile_v0.2.md`, `ARQ_EA_Lifecycle_and_Witness_Binding_v0.2.md`, `ARQ_Capsule_and_Witness_Record_Schemas_v0.2.md`  
**Scope:** Classical persistent-state software systems (no quantum claims)  
**Author:** Ivan Kotov  
**Place / year:** Bruxelles, 2026

---

## 0. Abstract

ARQ is a protocol. A protocol without profiles becomes a sermon.

This document defines **classical implementation profiles** for ARQ v0.2 so that bounded adaptation can be deployed in ordinary software systems without pretending that every software stack has the same physiology.

The document covers four canonical profiles:

- **ARQ-MEM** — persistent memory / knowledge store mutation;
- **ARQ-PLANNER** — bounded plan and action topology change;
- **ARQ-RAG** — retrieval and context assembly under witness discipline;
- **ARQ-VISION** — visual interpretation and perceptual event retention.

Each profile declares:

- its admissible system model references;
- its boundary assumptions;
- its queue and backlog discipline;
- its event payload and commit semantics;
- its rollback class;
- its minimum schema bundle;
- its promotion restrictions;
- its fail-closed triggers.

The central rule is simple:

> **Different classical subsystems produce different kinds of deviation.**  
> **ARQ SHALL NOT treat them as if they were physiologically identical.**

---

## 1. Purpose

This document exists to answer one practical question:

> How does ARQ get instantiated in real classical software subsystems without losing boundedness, witnessability, and promotion discipline?

This document SHALL:

1. define a common implementation-profile contract;
2. define the canonical classical ARQ profiles;
3. specify minimum required bounds and declared parameters for each profile;
4. define minimum witness bundles per profile and per authority level;
5. specify where profile-specific rollback and fail-closed behavior differ;
6. prohibit profile overclaiming.

---

## 2. Scope

This document applies to ARQ deployments in **classical persistent-state systems**, including but not limited to:

- structured memory stores;
- planners and bounded task graphs;
- retrieval pipelines and context assemblers;
- vision-derived semantic pipelines;
- hybrid stacks whose ARQ claim is limited to the classical side.

This document does **not** define:

- quantum trusted-boundary implementations;
- hardware attestation internals beyond what the trust profile already defines;
- model training loops as such;
- unconstrained multi-agent federation logic;
- external API business policy.

---

## 3. Non-Goals

This document does **not** attempt to:

- create one universal software profile for every classical subsystem;
- let a planner use vision-profile shortcuts or vice versa;
- let RAG noise silently become authoritative memory;
- treat a large context window as a trustworthy witness trail;
- collapse rollback into “just retry again”; 
- infer long-term value from one successful run;
- replace `ARQ_Capsule_and_Witness_Record_Schemas_v0.2.md` with prose.

A profile is a declared operating regime, not a vibe.

---

## 4. Normative Keywords

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, **MAY**, and **OPTIONAL** are to be interpreted as described in BCP 14.

---

## 5. Imported Symbols and Dependencies

The following imported symbols SHALL retain their meanings:

- models `M1`, `M2`, `M3`, `M4` from `ARQ_System_Models_and_Assumptions_v0.2.md`;
- `V_raw`, `V_trust`, `A_anom`, `P_anom` from the notation and valuation documents;
- `T_core`, `G_promote`, `τ`, `X_echo` from the trust profile;
- lifecycle labels `candidate_artifact`, `provisional_artifact`, `confirmed_EA`, `rejected`, `fail_closed` from the lifecycle document;
- canonical record types and schema profiles from `ARQ_Capsule_and_Witness_Record_Schemas_v0.2.md`.

This document SHALL NOT redefine those symbols.

---

## 6. Profile Model Mapping

### 6.1 Canonical classical model basis

Every classical implementation profile in this document SHALL declare at least:

- `M1` — finite authoritative persistent-state model;
- `M3` — epoch-gated trust/control model.

Any profile that keeps a bounded unresolved event queue SHALL also declare:

- `M4` — online queue/backlog model.

Any profile that mints retained artifacts into persistent memory SHALL also declare:

- `M2` — commit-metered retention model.

### 6.2 Hard rule

A classical profile MUST NOT claim bounded retained adaptation unless `M1 + M2 + M3` are all declared.

A classical profile MUST NOT claim bounded online unresolved deviation unless `M4` is declared.

---

## 7. Common Profile Contract

Every implementation claiming a profile from this document MUST publish a **Profile Declaration Record** (outside this document it is represented by `BR + ER + profile payload` or an equivalent stable declaration).

### 7.1 Required declaration fields

| Field | Type | Requirement | Meaning |
|---|---|---:|---|
| `profile_id` | string | MUST | One of the canonical profile identifiers in Section 8 |
| `profile_version` | string | MUST | Example: `0.2-draft` |
| `boundary_type` | string | MUST | `CLASSICAL_PERSISTENT` or declared hybrid classical side |
| `model_refs` | array | MUST | Must include the required model IDs |
| `K_queue` | integer | MUST if queue exists | Maximum pending events in live processing |
| `B_event_max` | integer | MUST | Maximum bounded payload size per event in bytes or bits |
| `b_commit_min` | integer | MUST if M2 declared | Minimum committed storage unit |
| `rollback_class` | string | MUST | See Section 7.3 |
| `schema_profile_min` | string | MUST | Minimum schema conformance level |
| `review_window_policy` | string | MUST | Declared observation / review regime |
| `trust_floor_tau` | number | MUST | Profile-specific minimum `τ` for privileged path |
| `G_promote_required` | integer | MUST | Usually `1` |
| `echo_policy` | string | MUST | Quarantine policy when `X_echo = 1` |
| `slot_policy` | string | MUST | Slot A / Slot B declaration |
| `fail_closed_policy` | string | MUST | Declared fail-closed behavior |

### 7.2 Bound declaration rule

The declared values above SHALL be finite.

A profile declaration containing unbounded queue length, unbounded event payload, or undefined commit unit SHALL be treated as non-conformant.

### 7.3 Rollback classes

Every profile MUST declare one rollback class.

| Rollback class | Meaning |
|---|---|
| `R0-NONE` | No rollback; only log / deny / quarantine |
| `R1-POINTER` | Revert pointer or selection without rewriting authoritative memory |
| `R2-SNAPSHOT` | Revert to attested pre-image or bounded snapshot |
| `R3-BRANCH` | Preserve prior authoritative branch and move candidate logic to Slot B shadow path |
| `R4-COMMIT-REPAIR` | Authoritative mutation may be reversed only through witnessed corrective mutation |

### 7.4 Review window policies

| Policy | Meaning |
|---|---|
| `RW0-NONE` | No observation window; actions are suppress or log-only |
| `RW1-SHORT` | Short bounded review window for low-cost local observation |
| `RW2-STRUCTURED` | Explicit observation window with one or more observation records |
| `RW3-EXTENDED` | Multi-step bounded review with challenge possibility and delayed promotion |

### 7.5 Slot discipline

All profiles in this document MUST support:

- **Slot A** — last-known-good canonical operational branch;
- **Slot B** — shadow exploration / reinterpretation branch.

Slot B SHALL NOT authorize real privileged action or authoritative promotion while it remains shadow-only.

If trust falls, contradiction appears, or profile-specific stability checks fail, the system MUST perform `Rollback(B→A)` and record the rollback.

---

## 8. Canonical Profile Registry

This document defines the following classical profiles.

| Profile ID | Name | Main subsystem |
|---|---|---|
| `ARQ-MEM` | Persistent memory mutation profile | memory / note / semantic store |
| `ARQ-PLANNER` | Planner topology profile | bounded planning / workflow graph |
| `ARQ-RAG` | Retrieval assembly profile | retrieval and context composition |
| `ARQ-VISION` | Visual semantic profile | image / frame / scene interpretation |

Implementations MAY define more profiles, but SHALL NOT redefine the meaning of the four canonical ones.

---

## 9. Profile `ARQ-MEM`

### 9.1 Purpose

`ARQ-MEM` governs bounded mutation of authoritative memory objects such as:

- semantic records;
- structured notes;
- memory links and summaries;
- local knowledge-store entries;
- candidate-to-authoritative memory transitions.

This is the profile closest to long-term identity pressure, so its promotion discipline SHALL be strict.

### 9.2 Required model set

`ARQ-MEM` MUST declare:

- `M1`;
- `M2`;
- `M3`;
- `M4`.

### 9.3 Boundary assumptions

The authoritative memory store MUST be finite and explicitly identified.

The implementation MUST declare:

- the authoritative memory namespace(s);
- the maximum mutable object size;
- the minimum commit unit `b_commit_min`;
- whether compaction is supported;
- whether authoritative memory pointers can be reverted without rewriting payloads.

### 9.4 Physiological event type

Typical events in `ARQ-MEM` are:

- merge conflict in memory update;
- novelty candidate in semantic clustering;
- contradiction between old authoritative memory and new candidate;
- compression drift;
- replay mismatch;
- candidate summary that changes retrieval behavior.

### 9.5 Queue and payload discipline

| Parameter | Requirement |
|---|---|
| `K_queue` | MUST be finite; RECOMMENDED small-to-moderate |
| `B_event_max` | MUST be finite and declared |
| `B_authoritative_object_max` | MUST be finite and declared |
| `b_commit_min` | MUST be declared |

When `K_queue` is exhausted, the profile SHALL NOT silently continue mutation. It SHALL either:

- deny new candidate creation,
- downgrade to `log_only`, or
- enter fail-closed according to policy.

### 9.6 Rollback class

`ARQ-MEM` MUST support at least `R2-SNAPSHOT` or `R3-BRANCH`.

`R0-NONE` is NOT sufficient.

### 9.7 Minimum review policy

`ARQ-MEM` MUST support at least `RW2-STRUCTURED`.

Direct promotion from single-pass classification to `confirmed_EA` is forbidden.

### 9.8 Minimum schema bundle

`ARQ-MEM` MUST support at least `ARQ-SCHEMA-REVIEW`.

For any `confirmed_EA` claim it MUST support `ARQ-SCHEMA-PROMOTION`.

### 9.9 Promotion discipline

A memory-derived event MAY reach `candidate_artifact` when:

- `T_core = 1`;
- a valid capsule exists;
- a review window exists or is opened;
- the mutation remains inside the declared authoritative namespace.

A memory-derived event MAY reach `confirmed_EA` only if:

- `G_promote = 1`;
- `τ >= trust_floor_tau`;
- `X_echo = 0` or explicit quarantine review has completed successfully;
- the source-to-authority chain is complete;
- the mutation result is replayable or reconstructible from source records.

### 9.10 Minimum record bundle by authority level

| Lifecycle target | Minimum records |
|---|---|
| `log_only` | `BR`, valid `ER`, `AC` |
| `candidate_artifact` | `BR`, valid `ER`, `AC`, `OWR` |
| `provisional_artifact` | previous bundle + `OR` + provisional `RR` |
| `confirmed_EA` | previous bundle + final `RR(CONFIRM)` + `EBR` + required co-signatures |

### 9.11 Fail-closed triggers

`ARQ-MEM` SHALL enter fail-closed if any of the following occur:

- authoritative namespace hash mismatch;
- snapshot / branch recovery unavailable when required;
- witness continuity break on an authoritative mutation path;
- trust invalidation during a promotion path;
- compaction destroys lineage references needed for replay.

---

## 10. Profile `ARQ-PLANNER`

### 10.1 Purpose

`ARQ-PLANNER` governs bounded deviation in planning and action topology, including:

- plan graph modification;
- heuristic override;
- branch reordering;
- tool-call sequence change;
- insertion or deletion of a bounded task node;
- route change under the same declared authority envelope.

### 10.2 Required model set

`ARQ-PLANNER` MUST declare:

- `M1`;
- `M3`;
- `M4`.

If planner mutations are retained into authoritative memory, it MUST also declare `M2`.

### 10.3 Boundary assumptions

The implementation MUST declare:

- the planner graph or bounded task structure under ARQ control;
- the maximum number of mutable nodes per cycle;
- whether tool effects are simulated, shadowed, or real;
- whether real actions require separate external approval.

### 10.4 Physiological event type

Typical events in `ARQ-PLANNER` are:

- planner branch divergence;
- heuristic contradiction;
- alternative path discovered under the same objective;
- low-cost unexpected ordering that improves execution;
- fragile plan that looks useful but breaks under replay.

### 10.5 Queue and payload discipline

| Parameter | Requirement |
|---|---|
| `K_queue` | MUST be finite and usually smaller than in RAG |
| `B_event_max` | MUST be finite |
| `B_plan_delta_max` | MUST be declared |
| `max_mutable_nodes_per_cycle` | MUST be finite |

### 10.6 Rollback class

`ARQ-PLANNER` MUST support at least `R1-POINTER` or `R3-BRANCH`.

If a real-world action path can be affected, `R3-BRANCH` is RECOMMENDED.

### 10.7 Minimum review policy

`ARQ-PLANNER` MUST support at least `RW1-SHORT`.

If real external action can be influenced, `RW2-STRUCTURED` is REQUIRED.

### 10.8 Minimum schema bundle

`ARQ-PLANNER` MUST support at least `ARQ-SCHEMA-BASE` for log-only operation.

If candidate retention is claimed, it MUST support `ARQ-SCHEMA-REVIEW`.

### 10.9 Promotion discipline

A planner event SHALL NOT become `confirmed_EA` merely because it produced a successful one-off path.

For planner promotion, the review path MUST establish at least one of the following:

- replay stability across bounded re-run;
- reduced cost without exceeding risk ceiling;
- preserved constraint satisfaction under repeated execution;
- no hidden privilege escalation.

### 10.10 Minimum record bundle by authority level

| Lifecycle target | Minimum records |
|---|---|
| `log_only` | `BR`, valid `ER`, `AC` |
| `candidate_artifact` | previous bundle + `OWR` |
| `provisional_artifact` | previous bundle + one or more `OR` + provisional `RR` |
| `confirmed_EA` | previous bundle + final `RR(CONFIRM)` + `EBR` |

### 10.11 Fail-closed triggers

`ARQ-PLANNER` SHALL enter fail-closed or deny privileged progression if:

- planner boundary is ambiguous;
- action path exceeds declared mutable-node budget;
- trust drops below floor during a real-action path;
- Slot B plan attempts to overwrite Slot A without review completion;
- contradiction appears between declared planner state and signed controller action records.

---

## 11. Profile `ARQ-RAG`

### 11.1 Purpose

`ARQ-RAG` governs bounded deviation in retrieval and context assembly, including:

- retrieval set variation;
- ranking instability;
- context compression or chunk fusion;
- evidence-path divergence;
- retrieval inclusion / exclusion that changes downstream interpretation;
- candidate extracted patterns from retrieved material.

### 11.2 Required model set

`ARQ-RAG` MUST declare:

- `M1`;
- `M3`;
- `M4`.

If retrieval-derived artifacts are retained into authoritative memory, `M2` is also REQUIRED.

### 11.3 Boundary assumptions

The implementation MUST declare:

- the retrieval corpora or namespace classes under ARQ observation;
- the maximum retrieval set size under ARQ control;
- the maximum bounded context payload that can enter valuation;
- whether raw source pointers are stable and replayable;
- whether retrieval is local-only or includes remote sources.

### 11.4 Physiological event type

Typical events in `ARQ-RAG` are:

- anomalous but useful retrieval combination;
- ranking inversion;
- contradiction between top-ranked and lower-ranked sources;
- source drift across epochs;
- context compression that changes answer topology;
- retrieval novelty that later proves hollow.

### 11.5 Queue and payload discipline

| Parameter | Requirement |
|---|---|
| `K_queue` | MUST be finite; often larger than planner but still bounded |
| `B_event_max` | MUST be finite |
| `max_docs_per_capsule` | MUST be finite |
| `max_context_tokens_or_bytes` | MUST be finite and declared |
| `stable_source_ref_required` | MUST be declared |

### 11.6 Rollback class

`ARQ-RAG` MUST support at least `R1-POINTER`.

If context compression or memory extraction is authoritative, `R2-SNAPSHOT` or `R3-BRANCH` is RECOMMENDED.

### 11.7 Minimum review policy

`ARQ-RAG` MUST support at least `RW2-STRUCTURED`.

Reason: retrieval claims are especially vulnerable to accidental self-confirmation and source omission.

### 11.8 Minimum schema bundle

`ARQ-RAG` MUST support at least `ARQ-SCHEMA-REVIEW` if it claims candidate retention.

If it claims confirmed retrieval-derived artifacts, `ARQ-SCHEMA-PROMOTION` is REQUIRED.

### 11.9 Promotion discipline

A RAG-derived event MUST NOT be promoted unless the implementation can show:

- stable source references or their hash-bound equivalents;
- the retrieval path that produced the candidate;
- enough source trace to challenge omission or cherry-picking;
- no echo collapse where the candidate merely rephrases the current system bias.

If `X_echo = 1`, the event SHALL remain quarantined at most as `candidate_artifact` until independent evidence path review succeeds.

### 11.10 Minimum record bundle by authority level

| Lifecycle target | Minimum records |
|---|---|
| `log_only` | `BR`, valid `ER`, `AC` |
| `candidate_artifact` | previous bundle + `OWR` |
| `provisional_artifact` | previous bundle + one or more `OR` + provisional `RR` |
| `confirmed_EA` | previous bundle + final `RR(CONFIRM)` + `EBR` + source-trace fields present |

### 11.11 Fail-closed triggers

`ARQ-RAG` SHALL enter fail-closed or deny promotion if:

- source references are unstable or irrecoverably missing;
- retrieval replay is impossible within the declared profile;
- the context payload exceeds declared bound and is truncated without witness;
- ranking or evidence path changes after epoch invalidation without reopening review;
- challenge cannot address omission because source lineage was lost.

---

## 12. Profile `ARQ-VISION`

### 12.1 Purpose

`ARQ-VISION` governs bounded deviation in visual interpretation, including:

- scene-summary instability;
- object/relationship reinterpretation;
- text-in-image extraction differences;
- disclosure-sensitive visual event classification;
- candidate scene patterns that may later become memory.

`ARQ-VISION` is especially sensitive to privacy and disclosure discipline.

### 12.2 Required model set

`ARQ-VISION` MUST declare:

- `M1`;
- `M3`;
- `M4`.

If visual interpretations are retained as authoritative memory, `M2` is REQUIRED.

### 12.3 Boundary assumptions

The implementation MUST declare:

- whether raw pixels remain local;
- whether only capsule-level bounded semantics are exported;
- whether OCR is enabled;
- whether disclosure is possible and under what privilege;
- whether the vision stack version is stable per epoch.

### 12.4 Physiological event type

Typical events in `ARQ-VISION` are:

- object set disagreement;
- relation ambiguity;
- OCR leak risk;
- style/scene reinterpretation that changes downstream planning or memory;
- candidate visual pattern that survives later replay;
- hallucinated object / relation collapse under challenge.

### 12.5 Queue and payload discipline

| Parameter | Requirement |
|---|---|
| `K_queue` | MUST be finite |
| `B_event_max` | MUST be finite |
| `max_objects_per_capsule` | MUST be finite |
| `max_relations_per_capsule` | MUST be finite |
| `shared_pixels_default_false` | MUST be true unless profile says otherwise |

### 12.6 Rollback class

`ARQ-VISION` MUST support at least `R1-POINTER`.

If visual-derived authoritative memory is affected, `R3-BRANCH` is RECOMMENDED.

### 12.7 Minimum review policy

`ARQ-VISION` MUST support at least `RW2-STRUCTURED`.

If disclosure-sensitive interpretation is involved, `RW3-EXTENDED` is RECOMMENDED.

### 12.8 Minimum schema bundle

`ARQ-VISION` MUST support at least `ARQ-SCHEMA-REVIEW` for candidate retention.

If disclosure or authoritative promotion is claimed, `ARQ-SCHEMA-PROMOTION` is REQUIRED.

### 12.9 Promotion discipline

A vision-derived event MUST NOT be promoted if:

- it depends on silent pixel disclosure;
- OCR leakage risk is uncontrolled;
- scene interpretation cannot be replayed from stable source hash or visual capsule lineage;
- the event is merely a stylistic reinterpretation with no bounded downstream utility.

Vision-derived `confirmed_EA` claims SHOULD prefer bounded semantic capsules over raw image retention, unless a lawful and profile-declared disclosure policy explicitly requires otherwise.

### 12.10 Minimum record bundle by authority level

| Lifecycle target | Minimum records |
|---|---|
| `log_only` | `BR`, valid `ER`, `AC` |
| `candidate_artifact` | previous bundle + `OWR` |
| `provisional_artifact` | previous bundle + `OR` + provisional `RR` |
| `confirmed_EA` | previous bundle + final `RR(CONFIRM)` + `EBR` + privacy/disclosure trace if relevant |

### 12.11 Fail-closed triggers

`ARQ-VISION` SHALL enter fail-closed or deny promotion if:

- the declared no-pixels-default policy is violated without witness;
- OCR or text-in-image extraction exceeds declared policy without privilege;
- vision stack version changes across an epoch without reopening review;
- disclosure occurs without the required approval record;
- visual semantics are detached from raw-hash provenance.

---

## 13. Cross-Profile Hard Rules

### 13.1 No profile hopping to escape discipline

An implementation SHALL NOT reinterpret an event under a looser profile merely because the stricter profile would deny promotion.

Example: a planner-meaningful event originating in retrieval SHALL NOT be silently relabeled as `ARQ-PLANNER` just to avoid RAG source-trace requirements.

### 13.2 Source profile primacy

The **originating subsystem** determines the primary profile.

Secondary profiles MAY be attached, but the stricter profile requirements SHALL dominate whenever promotion authority is affected.

### 13.3 Multi-profile events

If one event spans multiple profiles, the implementation MUST declare:

- `profile_primary`;
- `profile_secondary[]`;
- the stricter `schema_profile_min`;
- the stricter rollback requirement;
- the stricter fail-closed trigger set.

---

## 14. Profile Conformance Levels

### 14.1 `ARQ-IMPL-BASE`

Minimum profile implementation for a classical subsystem:

- declared profile;
- declared finite boundary;
- valid epoch path;
- finite queue and payload bounds;
- `log_only` and `suppress` paths;
- append-only capsule chain.

This level is insufficient for `confirmed_EA` claims.

### 14.2 `ARQ-IMPL-REVIEW`

Adds:

- review window support;
- candidate/provisional lifecycle states;
- observation records;
- Slot A / Slot B discipline;
- rollback declaration.

This level is sufficient for `candidate_artifact` and `provisional_artifact` claims.

### 14.3 `ARQ-IMPL-PROMOTION`

Adds:

- `G_promote` support;
- full promotion witness bundle;
- `EBR` support;
- complete authority lineage;
- anti-echo quarantine discipline;
- fail-closed trigger coverage for promotion path.

This is the minimum level for `confirmed_EA` claims.

### 14.4 `ARQ-IMPL-FULL`

Adds:

- retirement and compaction support with lineage preservation;
- challenge and resolution path coverage;
- multi-profile event handling;
- testable replay / audit procedure.

---

## 15. Minimum Audit Questions Per Profile

An implementation claiming a classical ARQ profile SHOULD be able to answer, at minimum:

1. What is the primary profile of this event, and why?
2. What finite boundary contains the authoritative state affected?
3. What queue bound and payload bound were declared?
4. What rollback class applies?
5. What review policy applies?
6. Which schema profile is minimally required for the claim being made?
7. Was Slot B prevented from silently overwriting Slot A?
8. If `confirmed_EA` is claimed, where is the full promotion bundle?
9. If fail-closed did not occur, what specific condition remained valid?
10. If compaction occurred, how is lineage preserved?

If the implementation cannot answer those questions, its profile claim is weak.

---

## 16. Anti-Echo and Slot A / Slot B Discipline

### 16.1 Anti-echo rule

If `X_echo = 1`, no profile in this document MAY directly promote the event to `confirmed_EA`.

At most, the event MAY:

- remain `log_only`,
- enter `candidate_artifact` under quarantine,
- or proceed to review only if a profile-appropriate independent observation path exists.

### 16.2 Slot discipline rule

A profile implementation MUST separate:

- canonical authority-bearing path (`Slot_A`), and
- experimental reinterpretation path (`Slot_B`).

Slot B MUST NOT:

- mutate authoritative memory directly;
- authorize real external action beyond declared profile permissions;
- rewrite thresholds or trust policy;
- collapse review stages.

### 16.3 Auto-rollback

If contradiction, drift, or trust invalidation appears during Slot B operation, the implementation MUST:

1. perform `Rollback(B→A)`;
2. record the rollback in witness trail;
3. preserve enough lineage to explain what was attempted and why it was reversed.

---

## 17. Bridges (Required)

### 17.1 Explicit bridge

ARQ core defines how deviation is handled. These implementation profiles define **where deviation lives physically in software**. Together they turn ARQ from abstract protocol into deployable bounded mechanics.

### 17.2 Hidden bridge #1 — Cybernetics / Ashby

Different software organs require different regulators. A memory store, planner, retrieval pipeline, and visual interpreter do not have the same error physiology. Requisite variety therefore appears as profile variety, not as one global tuning knob.

### 17.3 Hidden bridge #2 — Information theory / bounded channels

A profile is a channel contract: it bounds payload, queue, commit, replay surface, and witness minimum. This keeps adaptation from pretending it has more trustworthy bandwidth than the subsystem can physically and operationally sustain.

---

## 18. Earth Paragraph

This is ordinary engineering. A vector store, a planner, a retriever, and a vision parser do not fail in the same way. Memory corruption behaves like scar tissue. Planner drift behaves like a bad steering geometry. Retrieval noise behaves like a contaminated bibliography. Vision overreach behaves like seeing shapes in fog and calling them facts. That is why ARQ needs profiles: one recovery pattern does not fit every organ.

---

## 19. Normative Summary

1. Every classical ARQ implementation MUST declare a canonical profile.
2. Every declared profile MUST publish finite bounds for queue, payload, and authority path.
3. `ARQ-MEM` MUST use `M1 + M2 + M3 + M4`.
4. `ARQ-PLANNER`, `ARQ-RAG`, and `ARQ-VISION` MUST use at least `M1 + M3 + M4`.
5. Any profile claiming authoritative retention MUST also declare `M2`.
6. No profile SHALL silently bypass stricter source-profile discipline.
7. No `confirmed_EA` claim is valid below `ARQ-IMPL-PROMOTION`.
8. `X_echo = 1` blocks direct promotion in all profiles.
9. Slot B SHALL NOT silently overwrite Slot A.
10. If profile-specific fail-closed conditions are met, the implementation MUST deny privileged continuation or enter fail-closed state.

---

## 20. Reviewer Checklist

- Can the implementation name its profile without hesitation?
- Can it show the declared finite queue and payload bounds?
- Can it show the rollback class actually implemented?
- Can it show which schema bundle backs its strongest claim?
- Can it show where Slot B was prevented from becoming secret Slot A?
- Can it explain why this subsystem uses this profile and not a looser one?
- Can it show the minimum witness set for one promoted artifact from this profile?
- Can it show the exact fail-closed trigger set?

If not, the implementation may still run, but it is not yet a disciplined ARQ profile.
