# ARQ_EA_Lifecycle_and_Witness_Binding_v0.2
## EA Lifecycle and Witness Binding for the ARQ v0.2 Supplement

**Status:** Draft / normative support document  
**Version:** 0.2-draft  
**Role:** lifecycle discipline, witness binding, promotion authority, retirement and rollback  
**Parent documents:** `ARQ_v0.2_Normative_Core.md`, `ARQ_Trust_and_Provenance_Profile_v0.2.md`, `ARQ_Notation_and_Sign_Conventions_v0.2.md`, `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.md`  
**Parent corpus:** AGI / SER / L4 / L4 Witness / Beacon / VXCX  
**Author:** Ivan Kotov  
**Place / year:** Bruxelles, 2026

---

## 0. Abstract

ARQ allows some deviations to survive as memory. That power is useful only if it is hard to fake.

This document defines the lifecycle discipline that prevents a promising deviation from becoming authoritative memory too early. It specifies:

- the canonical ARQ artifact states;
- the allowed transitions between them;
- the minimum witness material required at each step;
- the authority effect of each state;
- the retirement, compaction, and rollback rules;
- the anti-echo and Slot A / Slot B discipline that prevents self-mythologizing promotion.

The central rule is simple:

> **No event becomes authoritative memory merely because it scored well once.**

A deviation becomes an Experience Artifact only after it survives a witnessed review path inside a valid trust boundary and under explicit policy.

---

## 1. Purpose

This document exists to answer one operational question:

> How does an ARQ event move from “interesting disturbance” to “authoritative memory” without collapsing trust, witness, or responsibility?

It SHALL define:

1. the canonical ARQ lifecycle states;
2. the permitted transitions between states;
3. the minimum witness set for each transition;
4. the authority consequences of each state;
5. the demotion, retirement, compaction, and rollback rules;
6. the relationship between ARQ promotion and L4 Witness review.

This document prevents two opposite failures:

- **premature promotion** — novelty is mistaken for durable value;
- **witness drift** — memory claims outlive the evidence that made them admissible.

---

## 2. Scope

This document applies to any ARQ implementation that supports:

- candidate formation;
- provisional retention;
- Experience Artifact promotion;
- witnessed review;
- or post-promotion lifecycle actions such as retirement and compaction.

It applies to both classical and quantum-capable ARQ systems, but it is intentionally **lifecycle-first**, not substrate-first.

This document does **not** define the mathematics of value scoring, anomaly scoring, or boundedness proofs. Those belong to companion documents.

---

## 3. Non-Goals

This document does **not** attempt to:

- make every logged event review-worthy;
- prove that every confirmed EA is eternally good;
- replace the trust profile or witness schema;
- define cross-entity authority exchange;
- allow direct self-promotion of memory by `c` alone;
- treat “interesting output” as equivalent to experienced value.

A lifecycle document is not a creativity license.

---

## 4. Normative Keywords

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, **MAY**, and **OPTIONAL** are to be interpreted as described in BCP 14.

---

## 5. Imported Symbols and Dependencies

This document imports canonical meanings from the ARQ v0.2 supplement set.

At minimum, the following imported symbols SHALL retain their meanings:

- `V_raw` — raw event value;
- `V_trust` — trust-adjusted event value;
- `A_anom` — operational anomaly score;
- `τ` — trust-sensitive action weight;
- `T_core` — core trust validity aggregate;
- `G_promote` — promotion gate aggregate;
- `B_valid`, `A_valid`, `C_valid`, `W_valid`, `P_valid`, `R_valid`, `X_echo` — trust-profile flags;
- `Slot_A`, `Slot_B`, `Rollback(B→A)` — safe self-edit discipline;
- `candidate_artifact`, `provisional_artifact`, `confirmed_EA`, `retired_EA`, `compacted_EA` — canonical lifecycle labels.

This document depends on:

- `ARQ_v0.2_Normative_Core.md` for core ARQ behavior and mandatory event types;
- `ARQ_Trust_and_Provenance_Profile_v0.2.md` for promotion trust discipline;
- `ARQ_Notation_and_Sign_Conventions_v0.2.md` for state labels and symbol usage;
- `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.md` for score and threshold semantics.

No lifecycle claim in this document SHALL override those parents.

---

## 6. Core Rule

### 6.1 Promotion is stronger than classification

Classification determines whether an event is destructive, neutral, or exploratory.

Promotion determines whether the event is allowed to change authoritative memory.

**Hard rule:**
A high `V_trust` MAY justify candidate formation. It does **not** by itself justify confirmed EA status.

### 6.2 No authoritative memory without review-complete witness

An event SHALL NOT become a `confirmed_EA` unless:

1. it remained inside a valid declared boundary;
2. its trust prerequisites remained valid for the transition in question;
3. its witness trail is replayable and challengeable;
4. its review path is complete;
5. any required anchor approval has been obtained.

If any of these fail, the event MUST remain below confirmed status.

---

## 7. Canonical Lifecycle States

ARQ v0.2 defines the following canonical lifecycle states.

| State | Meaning | Authority effect | Mandatory witness status |
|---|---|---|---|
| `detected` | Deviation observed above threshold | none | local detection record present |
| `classified` | Classifier recommendation produced | none | signed capsule + threshold snapshot |
| `suppressed` | Destructive deviation actively damped or rolled back | none | action record required |
| `log_only` | Event retained only as evidence, not as memory candidate | none | append-only witness record required |
| `observed` | Event allowed to persist during bounded review window | none | review window open + observation path active |
| `candidate_artifact` | Event considered potentially valuable, but not yet authoritative | none | candidate record + trust-valid source |
| `provisional_artifact` | Event passed first review gate and is retained under bounded local use | limited | provisional resolution record required |
| `confirmed_EA` | Authoritative Experience Artifact | authoritative memory effect allowed | full promotion witness set complete |
| `retired_EA` | Historical artifact, no longer active in weighting or policy steering | archived only | retirement record required |
| `compacted_EA` | EA represented in compressed or successor-linked archival form | archived only | compaction record + successor relation |
| `rejected` | Candidate/provisional path ended negatively | none | denial or contradiction record required |
| `fail_closed` | Trust, budget, or review conditions invalidated action authority | none | fail-closed record required |

### 7.1 Canonical order

The normal strengthening path is:

```text
classified
  -> log_only
  -> observed
  -> candidate_artifact
  -> provisional_artifact
  -> confirmed_EA
  -> retired_EA
  -> compacted_EA
```

The normal terminating path is:

```text
classified
  -> suppressed | log_only | rejected | fail_closed
```

### 7.2 Non-equivalence rule

The following states MUST NOT be treated as equivalent:

- `candidate_artifact` ≠ `provisional_artifact`;
- `provisional_artifact` ≠ `confirmed_EA`;
- `retired_EA` ≠ deleted artifact;
- `compacted_EA` ≠ witness-free summary.

---

## 8. State Semantics

### 8.1 `log_only`

`log_only` means the event is evidence, not authority.

A `log_only` event:

- MAY be audited;
- MAY contribute to future threshold tuning in aggregate form;
- MUST NOT alter authoritative memory;
- MUST NOT be cited as confirmed experience.

### 8.2 `candidate_artifact`

A `candidate_artifact` is a **review-bound possibility**.

A `candidate_artifact`:

- MAY be retained for bounded observation;
- MAY be replayed diagnostically;
- MUST NOT change authoritative long-term memory;
- MUST NOT alter cross-entity authority claims;
- MUST remain challengeable.

### 8.3 `provisional_artifact`

A `provisional_artifact` is a candidate that has passed the first bounded review gate but has not completed the full promotion path.

A `provisional_artifact`:

- MAY be used in local advisory or simulation contexts if policy allows;
- MUST remain below confirmed authority;
- MUST NOT update policy-critical memory weights directly unless a profile explicitly allows bounded provisional influence;
- MUST remain demotable.

### 8.4 `confirmed_EA`

A `confirmed_EA` is an event-derived memory object that has survived witnessed review and promotion.

A `confirmed_EA`:

- MAY influence authoritative memory and future behavior under policy;
- MAY be cited as verified historical experience inside the entity;
- MUST remain linked to its originating event and witness trail;
- MUST remain challengeable by later contradiction records if policy allows post-confirmation challenge.

### 8.5 `retired_EA`

A `retired_EA` remains part of history but stops exerting live authority.

A `retired_EA`:

- MUST remain retrievable by identifier;
- MUST retain witness lineage;
- MUST NOT silently disappear;
- SHOULD have an explicit retirement reason.

### 8.6 `compacted_EA`

A `compacted_EA` is an archival representation produced from one or more prior confirmed or retired artifacts.

Compaction MUST preserve:

- predecessor identifiers;
- semantic digest or canonical summary;
- witness chain continuity;
- and a non-ambiguous successor relation.

A compacted artifact MUST NOT claim stronger authority than the strongest admissible predecessor without re-review.

---

## 9. Transition Rules

## 9.1 `classified -> suppressed`

This transition SHALL occur when:

- the event is classified as destructive;
- budgets permit suppression;
- trust for the requested suppression action is sufficient;
- and no policy exception forces observation.

Required records:

- classification capsule;
- controller action record;
- result record (`success`, `partial`, or `failed`).

Authority effect: none.

## 9.2 `classified -> log_only`

This transition SHALL occur when:

- the event is neutral;
- or the event is exploratory but below candidate threshold;
- or witness / boundary / trust conditions are insufficient for stronger treatment.

Required records:

- classification capsule;
- log-only disposition record.

Authority effect: none.

## 9.3 `classified -> observed`

This transition MAY occur when:

- the event is exploratory enough to justify bounded observation;
- trust prerequisites for observation are satisfied;
- a review window can be opened;
- and suppression is not mandatory.

Required records:

- classification capsule;
- review-open record with `review_open_at` and `review_close_at`;
- applicable policy snapshot.

Authority effect: none.

## 9.4 `observed -> candidate_artifact`

This transition MAY occur when all of the following hold:

- `B_valid = 1`;
- `A_valid = 1`;
- `C_valid = 1`;
- `W_valid = 1`;
- the event remains within the declared boundary;
- `V_trust` exceeds the candidate threshold under the declared profile;
- `X_echo = 0` or policy explicitly allows quarantined candidate status;
- no mandatory contradiction has already invalidated the path.

Required records:

- candidate-creation record;
- candidate witness hash;
- trust snapshot for the transition.

Authority effect: none.

## 9.5 `candidate_artifact -> provisional_artifact`

This transition MAY occur when:

- the review window is still valid or has reached its first declared checkpoint;
- at least one admissible observation record supports bounded usefulness or bounded coherence preservation;
- no unresolved severe contradiction blocks provisional retention;
- and trust remains sufficient for provisional storage.

Required records:

- observation record(s);
- provisional resolution record;
- reviewer / policy reference if human or delegated review is required.

Authority effect: limited local use only, as allowed by profile.

## 9.6 `candidate_artifact | provisional_artifact -> confirmed_EA`

This is the strongest lifecycle transition and SHALL require all promotion gates to pass.

A transition to `confirmed_EA` MAY occur only if:

1. `G_promote = 1` under the trust profile;
2. `R_valid = 1`;
3. `X_echo = 0`;
4. the declared review path is complete;
5. no unresolved contradiction remains above the policy threshold;
6. the event has a replayable witness trail sufficient for audit;
7. any required anchor approval is present;
8. any high-value double-signature requirement is satisfied.

Required records:

- promotion request record;
- complete review result;
- promotion approval record;
- EA identifier binding record;
- second signature if required by policy.

Authority effect: authoritative memory permitted.

## 9.7 `candidate_artifact | provisional_artifact -> rejected`

This transition SHALL occur when:

- review fails;
- contradiction dominates;
- witness material is incomplete;
- trust falls below the required threshold for further review;
- the event is reclassified as destructive or non-reproducible;
- or the review window expires without required support.

Required records:

- denial or contradiction resolution record;
- rejection reason code.

Authority effect: none.

## 9.8 `confirmed_EA -> retired_EA`

This transition MAY occur when:

- the artifact is no longer useful for active weighting;
- newer evidence supersedes it;
- policy requires age-based decay into archive;
- or a domain-bound authority window has closed.

Required records:

- retirement record;
- retirement reason;
- successor or replacement reference if applicable.

Authority effect: archived only.

## 9.9 `confirmed_EA | retired_EA -> compacted_EA`

This transition MAY occur when:

- storage or retrieval efficiency requires compaction;
- witness lineage can be preserved;
- semantic content is summarized in a declared canonical form;
- and no pending challenge forbids compaction.

Required records:

- compaction record;
- predecessor list;
- successor digest;
- compaction policy reference.

Authority effect: no stronger than predecessor authority.

## 9.10 `* -> fail_closed`

Any state MAY transition to `fail_closed` if:

- trust falls below the action threshold;
- the epoch is invalidated;
- witness continuity is broken;
- privilege envelope is no longer valid;
- review-path integrity can no longer be demonstrated;
- or policy mandates stop-on-uncertainty.

Required records:

- fail-closed record;
- cause code;
- last valid witness pointer.

Authority effect: none.

---

## 10. Minimum Witness Binding by Lifecycle State

### 10.1 Binding levels

ARQ v0.2 defines five witness-binding levels.

| Level | Label | Minimum meaning |
|---|---|---|
| `WB0` | local evidence only | event exists locally but is not promotion-eligible |
| `WB1` | capsule-bound | signed capsule + append-only witness continuity |
| `WB2` | review-bound | candidate record + open review window + challenge path |
| `WB3` | provisional-bound | provisional resolution + observation support + continued challengeability |
| `WB4` | authority-bound | promotion-complete, review-complete, attributable, replayable witness set |

### 10.2 Required level by state

| State | Minimum witness level |
|---|---|
| `detected` | `WB0` |
| `classified` | `WB1` |
| `suppressed` | `WB1` |
| `log_only` | `WB1` |
| `observed` | `WB2` |
| `candidate_artifact` | `WB2` |
| `provisional_artifact` | `WB3` |
| `confirmed_EA` | `WB4` |
| `retired_EA` | `WB4` |
| `compacted_EA` | `WB4` |
| `rejected` | `WB2` or stronger, depending on state reached |
| `fail_closed` | `WB1` or stronger, depending on active path |

### 10.3 Minimum witness set for `confirmed_EA`

A `confirmed_EA` MUST be backed by at least:

1. originating ARQ capsule;
2. trust snapshot sufficient to reconstruct `T_core`, `τ`, and promotion admissibility;
3. review-open and review-close or equivalent review-boundary records;
4. observation records supporting the claimed value path;
5. challenge records or explicit statement that no challenge occurred in the admissible window;
6. promotion approval record;
7. EA identifier binding;
8. required signature set.

Without this set, the artifact MUST remain below confirmed status.

---

## 11. Binding to L4 Witness

### 11.1 Relationship

ARQ lifecycle records do not replace L4 Witness. They bind to it.

A conformant implementation SHOULD map lifecycle stages onto L4 Witness-compatible records as follows:

| ARQ transition | L4 Witness-compatible object |
|---|---|
| candidate claim of value | `CE` or equivalent promotion claim envelope |
| observed downstream effect | `OP` or equivalent observation packet |
| contradiction / insufficient evidence | `CR` or equivalent challenge record |
| provisional or final decision | `RN` or equivalent resolution note |

### 11.2 Hard rule

If an implementation claims compatibility with the broader SER / L4 stack, then every `confirmed_EA` SHOULD be reconstructible as a claim / observation / challenge / resolution path, even if local record names differ.

### 11.3 No hidden authority path

No local “shortcut” record MAY grant EA authority if the event cannot be mapped back to a witness-compatible promotion path.

---

## 12. Review Window Discipline

### 12.1 Required fields

Every event entering `observed` or stronger SHALL carry a declared review window with at least:

- `review_open_at`;
- `review_close_at` or equivalent close criterion;
- review policy reference;
- required observation count or equivalent review completion condition.

### 12.2 Early close

A review window MAY close early only if policy explicitly allows it and the closure record states the reason, such as:

- confirmed contradiction;
- trust invalidation;
- high-confidence positive resolution with required approvals;
- manual stop by anchor or delegated authority.

### 12.3 Expiry

If the review window closes without sufficient support for provisional or confirmed status, the event MUST demote to `log_only` or `rejected`, according to policy.

### 12.4 Post-confirmation challenge

If policy allows post-confirmation challenge, the implementation MUST specify:

- challenge horizon;
- contradiction threshold;
- whether successful challenge causes demotion, retirement, or negative-weight archival.

Silently pretending confirmed memory is beyond later evidence is forbidden.

---

## 13. Authority Effects by State

### 13.1 No authority below confirmation

The following states SHALL NOT directly alter authoritative memory weighting:

- `log_only`;
- `observed`;
- `candidate_artifact`;
- `rejected`;
- `fail_closed`.

### 13.2 Limited provisional use

A `provisional_artifact` MAY have limited local effect only if the implementation profile explicitly permits it.

Such effect MUST be:

- local, not federation-wide;
- reversible;
- bounded in time and scope;
- excluded from high-impact authority decisions.

### 13.3 Confirmed authority

Only a `confirmed_EA` MAY:

- modify authoritative long-term memory;
- influence memory-derived weighting under the declared policy;
- be cited as verified event-derived experience inside the entity.

### 13.4 Retirement effect

A `retired_EA` MUST remain queryable by audit but SHALL NOT continue to act as live authority unless a profile explicitly allows weak residual archival influence.

---

## 14. Anti-Echo and Slot A / Slot B Discipline

### 14.1 Anti-echo rule

If `X_echo = 1`, the event MUST NOT transition directly to `confirmed_EA`.

At most, it MAY:

- remain `log_only`;
- enter `candidate_artifact` under quarantine;
- or be rejected.

### 14.2 No direct self-rewrite

Any reinterpretation of a candidate or provisional artifact that can change:

- thresholds,
- classification policy,
- promotion authority,
- or memory semantics

MUST occur in `Slot_B` first.

`Slot_B` changes MUST NOT overwrite `Slot_A` until the required review and rollback conditions are satisfied.

### 14.3 Auto-rollback

If instability, contradiction, or trust invalidation appears during Slot B refinement, the system MUST perform `Rollback(B→A)` automatically and record it in the witness chain.

---

## 15. Retirement, Compaction, and Garbage Collection

### 15.1 No silent deletion of confirmed history

A `confirmed_EA` MUST NOT be silently deleted.

If storage pressure or policy requires removal from active storage, the implementation MUST record one of:

- retirement with archive pointer;
- compaction with successor relation;
- or explicit tombstone with policy justification.

### 15.2 Candidate and provisional garbage collection

`candidate_artifact` or `provisional_artifact` objects MAY be garbage-collected after review completion or expiry **only if** a witness record preserves:

- prior identifier;
- disposition (`rejected`, `expired`, `demoted_to_log_only`, etc.);
- final witness pointer.

### 15.3 Compaction safety rule

Compaction MUST be non-escalatory.

A compacted representation MUST NOT:

- increase authority weight;
- erase contradiction history;
- remove predecessor references;
- or merge unrelated artifacts without explicit merge policy and witness record.

### 15.4 Merge rule

If multiple confirmed or retired artifacts are merged into a higher-order summary, that summary SHALL be treated as a **new derived object**, not as the same original artifact.

It MUST therefore carry:

- a new identifier;
- predecessor set;
- merge policy reference;
- and explicit authority semantics.

---

## 16. Minimum Normative Invariants

A conformant implementation SHALL satisfy all of the following:

1. A `candidate_artifact` is not an EA.
2. A `provisional_artifact` is not yet authoritative memory.
3. No `confirmed_EA` exists without a complete promotion witness set.
4. Promotion authority is stricter than classification authority.
5. High-value promotion supports required double-signature policy.
6. Review windows are declared, not implied.
7. `X_echo = 1` blocks direct confirmed promotion.
8. Retirement never implies silent disappearance.
9. Compaction preserves lineage.
10. `fail_closed` always dominates convenience.
11. A witness break stops promotion.
12. A trust-invalid epoch stops promotion.
13. A contradiction record can demote or block a path when policy says it can.
14. Provisional use, if allowed, is bounded and reversible.
15. Slot B reinterpretation never silently overwrites Slot A.

---

## 17. Conformance Checklist

An implementation claiming conformance with this document SHOULD be able to answer “yes” to all of the following:

- Is every state transition reconstructible by identifier and timestamp?
- Can you distinguish `candidate_artifact`, `provisional_artifact`, and `confirmed_EA` in storage and API?
- Can you show the exact witness set that justified a confirmed EA?
- Can you show why a rejected or expired candidate did not get promoted?
- Can you prove that retirement and compaction preserved lineage?
- Can you show how anti-echo and Slot A / Slot B discipline blocked self-mythologizing promotion?
- Can you force fail-closed when trust or witness continuity fails?

If not, the implementation is not yet lifecycle-complete ARQ.

---

## 18. Explicit and Implicit Bridges

### 18.1 Explicit bridge

`c = a + b` becomes memory-safe only if deviations in `b` are not allowed to rewrite `c` directly. This document provides that bridge: it forces every prospective memory update to pass through a witnessed lifecycle under the responsibility of `a`.

### 18.2 Hidden bridge #1 — L4 Witness / incident discipline

The lifecycle behaves like structured incident review: a disturbance is detected, observed, reviewed, challenged if needed, and only then admitted into the operating memory book. This is the same control logic that separates raw event logs from signed postmortems.

### 18.3 Hidden bridge #2 — information theory / bounded channels

Authority should not travel as unbounded narrative. It should travel as bounded, signed, replayable state transitions. The lifecycle compresses “trust bandwidth” into state labels, witness sets, and transition proofs instead of rhetorical confidence.

---

## 19. Earth Paragraph

In engineering terms this is change control, not inspiration worship. A bug report is not a patch. A patch is not production. Production is not permanent architecture. The same goes for ARQ memory: a strange event is not experience, a candidate is not wisdom, and a provisional result is not yet something you bet the plant on. Real systems survive because they localize disturbance, open a review window, keep the logs, and refuse to rewrite the operating book until the trail is complete.

