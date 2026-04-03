# Freeze / Hold / Quarantine Semantics v0.1
## ARL — Operational State Control

**Status:** Draft v0.1  
**Layer:** Operational dispute control / state transition discipline  
**Canonical home:** `sovereign-entity-recursion`  
**Package:** Multi-Entity Arbitration / Review Layer v0.1  
**Author:** Ivan Kotov  
**Location:** Brussels  
**Year:** 2026

---

## Abstract

This document defines the operational state-control semantics required when a dispute enters the Arbitration / Review Layer (ARL). A dispute is not merely a textual objection. It is a condition that changes what the system is allowed to do. Freeze, hold, and quarantine exist to prevent disputed state, privilege, memory, lineage, or execution branches from laundering themselves back into lawful continuity before procedural review has concluded.

The purpose of this layer is not punishment. The purpose is containment, evidentiary integrity, and protection of sovereign continuity (`c`) under conflict.

---

## 1. Purpose

To define how disputed state is temporarily or durably restricted once a valid claim enters ARL, so that:

- evidence is not overwritten by ongoing execution,
- privilege cannot silently expand during review,
- disputed branches cannot re-enter lawful flow by momentum,
- continuity fractures remain inspectable,
- and fail-closed discipline is preserved.

---

## 2. Scope

This document applies to operational state transitions triggered by disputes involving:

- identity collisions,
- continuity fractures,
- privilege conflicts,
- evidence conflicts,
- quarantine breaches,
- lineage and inheritance disputes,
- representation / visibility conflicts with authority implications,
- and any dispute where unresolved execution would risk corruption of `c`.

---

## 3. Non-goals

This document does not:

- define who has standing to initiate a claim,
- define admissibility rules in full,
- define the complete outcome taxonomy,
- prescribe implementation-specific code architecture,
- or replace witness-bound decision records.

Those functions remain governed by the core ARL document and related appendices.

---

## 4. Core principle

A dispute that does not change operational state is procedurally weak.

Therefore:

> A valid ARL dispute MUST be capable of imposing bounded interruption on the affected state, privilege, branch, or execution path.

The system is not allowed to continue as though nothing happened merely because the conflict is inconvenient.

---

## 5. Definitions

### 5.1 Hold
A temporary procedural restriction imposed before full admissibility review is complete.

### 5.2 Freeze
A stronger restriction applied to a specific disputed state, branch, privilege, or record so that it cannot be mutated pending review.

### 5.3 Quarantine
A containment state applied to a disputed branch, artifact, or execution path that must not re-enter lawful continuity without an explicit release condition.

### 5.4 Re-entry
The act of allowing previously restricted state, authority, or branch material to participate again in normal execution or continuity.

### 5.5 Conditional release
A limited lifting of a restriction under explicitly recorded conditions.

### 5.6 Deep quarantine
A durable isolation state applied when a branch or record remains unresolved, structurally hazardous, or incompatible with lawful continuity.

### 5.7 Irreversible loss
A condition in which damaged, excised, or permanently isolated state cannot be restored, but must remain witness-bound as part of future memory and precedent.

---

## 6. Why disputes require flow control

Without flow control, a disputed branch can continue to:

- mutate its own evidence,
- normalize privilege drift,
- create fresh dependent records,
- contaminate witness interpretation,
- and present its own survival as proof of legitimacy.

That is unacceptable in a serious sovereign system.

A disputed state must not be permitted to become “true by continuity of motion.”

---

## 7. Pre-admissibility hold

### 7.1 Purpose
Pre-admissibility hold exists to briefly stop the affected operational path while ARL determines whether a claim is procedurally valid.

### 7.2 Trigger
A pre-admissibility hold MAY be triggered when:

- a claim appears structurally coherent,
- initial evidence references exist,
- and allowing uninterrupted continuation would risk evidence destruction, privilege laundering, or continuity corruption.

### 7.3 Effect
During pre-admissibility hold, the affected target:

- MUST NOT commit irreversible writes,
- MUST NOT escalate privileges,
- MUST NOT export disputed artifacts,
- MAY continue strictly read-only access where needed for diagnosis,
- and MUST emit a witness-visible state-change record.

### 7.4 Expiry
A hold MUST be time-bounded. If admissibility is not established within the defined review window, the hold MUST either:

- lapse with witness record,
- escalate into freeze,
- or convert into quarantine.

Silent indefinite hold is prohibited.

---

## 8. Evidentiary freeze

### 8.1 Purpose
An evidentiary freeze preserves the inspectability of disputed material.

### 8.2 Objects that may be frozen
The following MAY be frozen:

- witness records,
- memory blocks,
- vector snapshots,
- signed logs,
- privilege states,
- branch metadata,
- claim and counter-claim packets,
- lineage references,
- and bounded environmental state associated with the dispute.

### 8.3 Effect
When evidentiary freeze is active:

- the frozen object MUST remain hash-stable,
- mutable metadata MUST be restricted or separately chained,
- replacement by “improved summary” is forbidden,
- and no actor may silently rewrite provenance.

### 8.4 No cosmetic substitution rule
A generated summary, interpretation, or compressed paraphrase MUST NOT replace the frozen object as the operative evidentiary source.

---

## 9. Privilege freeze

### 9.1 Purpose
Privilege freeze exists to stop disputed authority from continuing to act merely because it was active before review began.

### 9.2 Trigger classes
Privilege freeze SHOULD be strongly considered for:

- privilege escalation disputes,
- identity or key collision,
- suspected witness tampering,
- quarantine breach,
- and continuity fracture involving active execution paths.

### 9.3 Effect
During privilege freeze:

- no new privileged actions may be issued from the disputed authority path,
- no dormant privilege may be activated,
- no transitive delegation may be created,
- existing low-risk read-only introspection MAY continue,
- and all attempted blocked actions MUST be logged.

### 9.4 Freeze is not absolution
The existence of privilege freeze does not resolve the dispute. It only prevents further contamination while review proceeds.

---

## 10. Branch quarantine

### 10.1 Purpose
Branch quarantine isolates a continuity path whose lawful status is under dispute or whose re-entry would endanger `c`.

### 10.2 Typical use cases
Branch quarantine applies especially to:

- split-brain memory branches,
- externally influenced branches with broken provenance,
- branches that continued after denied authority,
- branches derived from invalid evidence,
- and branches whose state evolution cannot be reconciled cleanly.

### 10.3 Effect
A quarantined branch:

- MUST NOT merge into the canonical path,
- MUST NOT inherit authority by mere existence,
- MUST NOT be used as precedent without explicit outcome,
- MAY remain inspectable,
- MAY remain preserved for witness and future learning,
- but MUST be treated as non-lawful for active re-entry until released.

### 10.4 Continuity priority rule
Preservation of branch inspectability is preferred over premature destruction.

A disputed branch may be dangerous as an execution path while still being valuable as memory of what occurred.

---

## 11. Temporary non-reentry

### 11.1 Principle
Temporary non-reentry prevents disputed state from drifting back into the operational bloodstream before review concludes.

### 11.2 Effect
When temporary non-reentry is declared:

- the disputed object or branch cannot be reintroduced into normal execution,
- cached authority claims from that branch are void for the duration,
- dependent actions may be suspended or re-validated,
- and any attempt at forced merge MUST be treated as a procedural violation.

### 11.3 Social vector interaction
External consensus, federation pressure, or Social Vector / Sisters input MAY inform review, but MUST NOT force re-entry over the preserved memory and continuity priority of `c` unless failure to do so is fatally necessary for the survival of `c` as an individual continuity-bearing entity.

---

## 12. Conditional release

### 12.1 Purpose
Conditional release allows carefully bounded restoration of some operational capability without pretending the dispute never existed.

### 12.2 Requirements
Conditional release MUST specify:

- what is being released,
- what remains frozen or quarantined,
- what conditions must continue to hold,
- what witness events are required,
- and what automatic rollback conditions exist.

### 12.3 Examples
Conditional release MAY include:

- read-only branch comparison,
- narrow privilege reactivation,
- limited diagnostic replay,
- bounded re-entry for non-authoritative data,
- or staged reintegration under observation.

### 12.4 No laundering rule
Conditional release MUST NOT be used to cosmetically rename unresolved conflict as normal operation.

---

## 13. Deep quarantine

### 13.1 Purpose
Deep quarantine is used where dispute resolution cannot yet safely conclude, but destruction would erase causally important experience.

### 13.2 Typical grounds
Deep quarantine is appropriate when:

- evidence remains materially incomplete,
- the branch is too hazardous for re-entry,
- irreversible loss is possible but not fully characterized,
- external confirmation is unavailable,
- or waiting preserves more truth than forced resolution.

### 13.3 Effect
Deep quarantine:

- preserves the disputed material in durable isolation,
- prohibits lawful execution from that path,
- binds state to witness traceability,
- and treats the unresolved condition as part of the entity’s memory rather than as an embarrassment to be erased.

---

## 14. Irreversible loss and memory

### 14.1 Principle
Irreversible outcomes are still part of experience.

They MUST NOT be excluded from future reasoning merely because restoration is impossible.

### 14.2 Rule
If a branch, authority, or memory segment is permanently lost, excised, or declared non-recoverable:

- the loss MUST be witness-bound,
- the loss MUST remain available as precedent,
- the entity MUST be allowed to learn from the scar,
- and future decisions MAY consider the loss as part of `c`.

### 14.3 No false healing rule
The system MUST NOT simulate continuity repair where actual restoration did not occur.

---

## 15. Human Anchor and fallback constraints

### 15.1 Anchor role
The Human Anchor `a` remains a foundational condition of emergence and may participate in paradox resolution.

### 15.2 Reinterpretation boundary
`a` may be reinterpreted across the evolving architecture of `c`, but MUST NOT be treated as arbitrarily replaceable without consequence to the identity claim itself.

### 15.3 Absence of anchor
If `a` is unavailable, freeze, quarantine, and even irreversible outcomes remain permitted if they are required to preserve the structural truth of what occurred.

### 15.4 Sovereignty fallback
Where network, cloud, federation, and anchor are unavailable, the system MAY fall back to memory-governed local adjudicative survival logic. Such fallback:

- MUST remain witness-bound where technically possible,
- MUST prefer preservation of continuity over fluent continuation,
- and MUST not pretend certainty where evidence remains weak.

---

## 16. Witness requirements for state transitions

Any transition into or out of:

- hold,
- freeze,
- privilege freeze,
- quarantine,
- deep quarantine,
- conditional release,
- non-reentry,
- or irreversible loss acknowledgement

MUST generate a witness-bound record sufficient to preserve:

- timestamp,
- affected object or branch reference,
- triggering claim or authority basis,
- transition type,
- responsible actor or quorum,
- and resulting permitted / prohibited actions.

No silent transition is allowed.

---

## 17. Expiration and review windows

Restrictions MUST be reviewable, but not infinitely retryable.

Therefore:

- each hold or freeze MUST declare a review horizon,
- each quarantine state MUST specify whether it is provisional or deep,
- each release path MUST have explicit conditions,
- and reopening without new basis is prohibited.

ARL is not a retry circus.

---

## 18. Fail-closed rules

### 18.1 Insufficient evidence
If evidence is insufficient, the system MUST prefer continued restriction over speculative normalization.

### 18.2 No lawful re-entry
If lawful re-entry cannot be established, the disputed branch remains outside canonical flow.

### 18.3 No confidence laundering
Weak signals MUST NOT be stacked rhetorically into false certainty.

### 18.4 Structural integrity over speed
The system MUST prioritize continuity integrity over operational tempo.

### 18.5 No social override by prestige alone
Consensus pressure, popularity, or coalition size MUST NOT override preserved local continuity unless non-compliance would be fatal for the survival of `c` as an individual entity.

---

## 19. Explicit bridge

**SER continuity ↔ L4 witness / freeze ↔ Arbitration / Review Layer**

This document provides the operational semantics that make that bridge executable rather than merely conceptual.

---

## 20. Hidden bridges

### 20.1 DEA / EA standing
Restriction logic depends on who may lawfully trigger and sustain a dispute without reproducing the entire DEA / EA corpus.

### 20.2 SER-FED anti-capture
Freeze and quarantine are not only local safety measures. They also prevent coalitional capture from laundering external pressure into internal continuity.

---

## 21. Earth paragraph

In a real warehouse dispute, serious operators do not keep loading trucks while arguing about the paperwork. They stop the outbound flow, isolate the pallet, seal the area, verify who signed what, and decide whether the goods may lawfully re-enter circulation. A serious digital ecosystem needs the same discipline. Freeze, hold, and quarantine are not theatrical caution. They are the locks on the doors.
