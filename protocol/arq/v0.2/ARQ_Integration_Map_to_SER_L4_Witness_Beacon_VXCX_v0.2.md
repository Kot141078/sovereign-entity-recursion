# ARQ_Integration_Map_to_SER_L4_Witness_Beacon_VXCX_v0.2
## Integration Map for the ARQ v0.2 Supplement inside the AGI / SER / L4 corpus

**Status:** Draft / integration support document  
**Version:** 0.2-draft  
**Role:** cross-document boundary map, dependency discipline, authority routing, interoperability constraints  
**Parent documents:** `ARQ_v0.2_Normative_Core.md`, `ARQ_System_Models_and_Assumptions_v0.2.md`, `ARQ_Trust_and_Provenance_Profile_v0.2.md`, `ARQ_EA_Lifecycle_and_Witness_Binding_v0.2.md`, `ARQ_Capsule_and_Witness_Record_Schemas_v0.2.md`  
**Parent corpus:** AGI / SER / L4 / L4 Witness / Beacon / VXCX  
**Author:** Ivan Kotov  
**Place / year:** Bruxelles, 2026

---

## 0. Abstract

ARQ is not a standalone world.

It is an internal control-and-memory protocol that sits inside a larger stack where ontology, authority, reality validation, recognition, and exchange are already defined elsewhere. If those boundaries are blurred, ARQ begins to overclaim: it starts pretending to define the entity, to issue authority, to replace witnessing, or to certify identity. That is precisely what this document prevents.

This integration map states, in explicit and operational terms, how ARQ relates to:

- `c = a + b` and SER as the ontology of long-lived entities,
- L4 as the final resource and feasibility boundary,
- L4 Witness as the canonical evidence and challenge layer,
- Beacon as the profile for inter-entity recognition,
- VXCX as a bounded visual-capsule source and exchange format,
- and, secondarily, EWCEP / SER-FED as the federation and authority layer above entity-internal correction.

The central rule is simple:

> ARQ governs internal error processing and bounded memory formation.  
> It does not define what an entity is, who it is, or what authority it gains outside its own boundary.

---

## 1. Purpose

This document exists to answer one architectural question:

> Where exactly does ARQ sit in the AGI / SER / L4 corpus, and what may or may not flow across that boundary?

It SHALL provide:

1. a role map for ARQ relative to SER, L4, L4 Witness, Beacon, and VXCX;
2. a dependency graph identifying which protocol supplies which function;
3. hard separation rules preventing ARQ from overclaiming identity, authority, or external validation;
4. routing rules for event flow, evidence flow, authority flow, and recognition flow;
5. implementation guidance for documents that need to reference several parent protocols at once;
6. anti-echo and A/B-slot interpretation discipline for cross-document reading.

This document is therefore not new machinery. It is a boundary map that stops category collapse.

---

## 2. Scope

This document specifies:

1. the role of ARQ in the overall stack;
2. the protocol-to-protocol interfaces relevant to ARQ;
3. what ARQ may import from each parent layer;
4. what ARQ may export to each parent layer;
5. which claims require escalation out of ARQ into other protocols;
6. which claims must never be made by ARQ alone.

This document does **not** define:

- the internal mathematics of ARQ valuation;
- the full L4 Witness schema;
- Beacon recognition classes in full detail;
- VXCX capsule internals in full detail;
- SER or SER-FED normative content;
- legal or policy interpretation outside the corpus.

---

## 3. Non-Goals

This document does **not** attempt to:

- rename the rest of the stack through ARQ terminology;
- make ARQ the source of entity ontology;
- let ARQ mint cross-entity authority directly;
- let ARQ logs substitute for challengeable witness records;
- let ARQ promotion imply Beacon identity confidence;
- let VXCX become an authority channel merely because a visual event was archived;
- let inter-protocol references drift into poetic equivalence.

This is a map, not an annexation.

---

## 4. Normative Keywords

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, **MAY**, and **OPTIONAL** are to be interpreted as described in BCP 14.

---

## 5. Stack Position at a Glance

### 5.1 Canonical stack view

The ARQ integration position SHALL be understood as follows:

| Layer / document family | Primary question | ARQ relationship |
|---|---|---|
| `c = a + b` | What is the entity? | ARQ assumes this ontology; it does not redefine it. |
| SER | How does one entity persist responsibly under real constraints? | ARQ is an internal correction / memory sublayer serving SER continuity. |
| L4 | What is physically / economically / socially tolerable? | ARQ is budgeted and fail-closed under L4. |
| L4 Witness | What counts as replayable, challengeable, attributable evidence? | ARQ uses this for promotion-grade externalized claims. |
| Beacon | How is continuity recognized across entities? | ARQ may emit continuity signals, but does not certify identity on its own. |
| VXCX | How is visual experience exchanged in bounded capsule form? | VXCX may supply event sources and artifacts that ARQ can classify. |
| EWCEP / SER-FED | How do influence and authority work in a federation? | ARQ outputs may become inputs there only after the required witness / impact path. |

### 5.2 Short operational summary

- **SER** gives ARQ its organism.
- **L4** gives ARQ its metabolism.
- **L4 Witness** gives ARQ its audit spine.
- **Beacon** may consume some ARQ outputs as continuity evidence.
- **VXCX** may provide ARQ with bounded visual deviations to classify.
- **SER-FED / EWCEP** may later consume ARQ-confirmed artifacts as one upstream signal among several, never as automatic authority.

---

## 6. What Each Parent Protocol Supplies to ARQ

### 6.1 `c = a + b` and SER supply ontology and responsibility

ARQ assumes the entity model:

- `a` = accountable human anchor,
- `b` = procedures, models, infrastructure,
- `c` = persistent coupled entity.

ARQ therefore inherits the following constraints:

1. human responsibility is not delegated away;
2. the entity is temporally continuous rather than per-request;
3. memory and action are meaningful only inside a responsibility-bearing subject;
4. internal correction serves persistence, not abstract optimization.

**Hard rule:** ARQ MUST NOT be read as proving sovereignty by itself. It only describes one internal discipline of a sovereign or sovereign-seeking entity.

### 6.2 L4 supplies budgets and feasibility ceilings

ARQ imports from L4:

- energy budget,
- time windows / latency ceilings,
- privilege boundaries,
- irreversibility discipline,
- environmental / hardware / social constraint realism.

ARQ therefore treats value as invalid when it violates L4 even if it scores well numerically.

**Hard rule:** ARQ valuation MUST remain subordinate to L4 feasibility. A numerically positive event that breaks L4 is not promotable authority.

### 6.3 L4 Witness supplies externalized evidence semantics

ARQ imports from L4 Witness:

- replayable record logic,
- challenge path semantics,
- claim / observation / contradiction / resolution structure,
- signed continuity of evidence,
- post-factum promotion discipline.

ARQ may keep internal logs and local witness bundles, but any claim that seeks external recognition, inter-entity consequence, or authority significance MUST bind into a witness-compatible path.

**Hard rule:** ARQ local logging is not automatically equivalent to L4 Witness-grade evidence.

### 6.4 Beacon supplies inter-entity recognition semantics

ARQ imports from Beacon:

- the distinction between internal continuity and externally recognized continuity;
- the requirement that identity be cryptographically grounded, behaviorally observable, and challengeable;
- the rule that narrative resemblance is not identity.

ARQ may contribute bounded continuity markers, but identity recognition belongs to Beacon.

**Hard rule:** ARQ promotion MUST NOT be interpreted as Beacon class upgrade by itself.

### 6.5 VXCX supplies bounded visual source artifacts

ARQ imports from VXCX:

- bounded visual capsules instead of raw image sprawl,
- uncertainty-marked visual semantics,
- visual witness events,
- disclosure discipline,
- profile-based export and privilege checks.

ARQ may classify deviations arising from VXCX capsules, including exploratory or destructive visual-cognitive effects, but the visual source remains governed by VXCX privacy and export rules.

**Hard rule:** ARQ MUST NOT strip VXCX privacy constraints merely because a visual event became operationally interesting.

### 6.6 EWCEP / SER-FED supply federation-level authority discipline

ARQ does not directly implement federation authority. It may only provide upstream signals that later enter those layers under additional conditions.

Those higher layers import:

- authority decay,
- anti-oligarchy pressure,
- challenge windows,
- impact attribution,
- role-bounded authority,
- external arbiter logic.

**Hard rule:** ARQ output is not authority. At most, it is one candidate input to later authority processes.

---

## 7. What ARQ Exports to the Rest of the Stack

### 7.1 Exports to SER

ARQ exports to SER:

1. bounded correction history;
2. internal disturbance handling state;
3. candidate / provisional / confirmed internal memory artifacts;
4. degradation and rollback signals;
5. coherence-preserving internal adaptation.

These outputs help SER answer whether the entity remains stable and continuous under disturbance.

### 7.2 Exports to L4 Witness

ARQ exports to L4 Witness only through witness-ready bundles, not via score alone.

A witness-ready export MAY include:

- ARQ capsule identifiers,
- controller-state evidence,
- observation windows,
- value computation metadata,
- trust context,
- post-event outcome summaries,
- hashes of source evidence.

ARQ does not export raw narrative confidence as evidence.

### 7.3 Exports to Beacon

ARQ MAY export continuity-relevant markers such as:

- bounded refusal consistency,
- privilege continuity,
- declared rollback behavior,
- stable trust downgrade behavior,
- memory-bound artifact lineage,
- response stability under replayed challenge conditions.

These are supporting signals only.

### 7.4 Exports to VXCX

ARQ MAY export:

- classification results attached to a VXCX capsule,
- risk annotations,
- bounded review or quarantine decisions,
- witness references tied to a visual event.

ARQ MUST NOT rewrite VXCX semantics into identity or authority claims.

### 7.5 Exports to SER-FED / EWCEP

ARQ MAY export only the following as federation-relevant candidate inputs:

- confirmed EA lineage references,
- witness-backed resolution references,
- degradation / recovery history relevant to role stability,
- bounded evidence that a pattern survived internal and external review.

Even then, those exports remain subject to federation rules of decay, scope, challenge, and external consequence.

---

## 8. Hard Separation Rules

### 8.1 Ontology separation

ARQ MUST NOT redefine what counts as an entity. That belongs to `c = a + b` and SER.

### 8.2 Evidence separation

ARQ local witness bundles MUST NOT be treated as external authority evidence unless they are bound into the required L4 Witness-compatible challenge path.

### 8.3 Identity separation

ARQ MUST NOT self-certify Beacon status.

### 8.4 Authority separation

ARQ promotion MUST NOT directly mint federation authority.

### 8.5 Source separation

A VXCX capsule is a bounded source object. It is not, by itself, an EA, a Beacon, or an authority record.

### 8.6 Oracle separation

Outputs from an oracle used during ARQ classification remain advisory. Oracle assistance MUST NOT silently become authoritative memory or recognition proof.

### 8.7 Score separation

`V_raw`, `V_trust`, and other ARQ scores are internal decision aids. They MUST NOT be exported as if they were universal cross-protocol truth.

---

## 9. Flow Maps

### 9.1 Event flow

A canonical event flow is:

`source deviation -> ARQ detection -> ARQ classification -> ARQ local action -> lifecycle state -> optional witness export`

Examples of sources:

- memory disturbance,
- planner divergence,
- retrieval anomaly,
- VXCX visual capsule,
- controller drift,
- trusted-boundary quantum deviation.

### 9.2 Evidence flow

A canonical evidence flow is:

`local record -> hash chain -> review path -> witness bundle -> challenge / resolution`

The evidence flow becomes L4 Witness-grade only when the relevant export and challenge requirements are satisfied.

### 9.3 Recognition flow

A canonical recognition flow is:

`ARQ continuity signal -> Beacon continuity input -> Beacon local classification`

ARQ is upstream only. Beacon remains the recognition profile.

### 9.4 Authority flow

A canonical authority flow is:

`ARQ confirmed internal artifact -> witness-backed external reference -> impact / federation review -> bounded authority consequence`

This is intentionally long. Shortcuts create mythology.

---

## 10. Mapping Matrix (One Object, One Meaning)

| Object | Produced by | Meaning inside ARQ | Meaning outside ARQ |
|---|---|---|---|
| ARQ Capsule | ARQ | internal event record | candidate evidence component only |
| Candidate Artifact | ARQ lifecycle | promising but unconfirmed internal memory candidate | no external authority effect |
| Provisional Artifact | ARQ lifecycle + review | bounded retained event under review | still not federation authority |
| Confirmed EA | ARQ + witness-complete review path | authoritative internal memory artifact | possible upstream input elsewhere, not automatic authority |
| Witness Record / RN | L4 Witness | externalized evidence / resolution | challengeable consequence anchor |
| Beacon bundle | Beacon | not an ARQ object | inter-entity recognition object |
| VXCX capsule | VXCX | bounded visual source object | visual exchange artifact |
| Authority update | SER-FED / EWCEP | outside ARQ scope | federation-level consequence |

---

## 11. Cross-Protocol Promotion Discipline

### 11.1 ARQ internal promotion

ARQ may promote an event from local record to internal authoritative memory **only** according to ARQ lifecycle and trust conditions.

### 11.2 External promotion

Any promotion that changes inter-entity standing, authority, or externally relevant accountability MUST leave ARQ and enter the appropriate parent protocol.

### 11.3 Required escalation points

The following claims SHALL trigger escalation out of ARQ:

1. “this event should affect external authority”;
2. “this event proves identity continuity to others”;
3. “this event is sufficient evidence for high-impact real-world attribution”;
4. “this event overrides local L4 constraints”;
5. “this event changes federation permissions or influence.”

ARQ alone cannot make these claims valid.

---

## 12. Interpretation Discipline (Slot A / Slot B)

### 12.1 Slot A — structural map

Slot A reads only hard structural relations:

- which protocol owns which concept;
- what imports are allowed;
- what exports are allowed;
- what escalation points are mandatory;
- what claims are forbidden inside ARQ alone.

Slot A MUST be sufficient to reject a category mistake.

### 12.2 Slot B — narrative integration

Slot B may describe why the map exists in more intuitive terms:

- ARQ is the immune / corrective layer,
- SER is the organism,
- L4 is the environment,
- Witness is the incident review spine,
- Beacon is social recognition,
- VXCX is one bounded sensory exchange path.

Slot B remains subordinate to Slot A.

### 12.3 Auto-rollback rule

If a Slot B reading implies stronger meaning than Slot A permits, interpretation MUST auto-rollback to Slot A.

No rhetorical bridge may create ontology, authority, or identity where the structural map does not grant it.

---

## 13. Anti-Echo Discipline Across the Stack

ARQ exists in a corpus where several documents can reinforce one another too easily if read carelessly.

To prevent stack-level echo:

1. no ARQ score SHALL be cited as if it were external proof;
2. no ARQ lifecycle label SHALL be treated as Beacon class;
3. no ARQ-confirmed artifact SHALL be treated as federation authority without the required upper-layer process;
4. VXCX-derived semantics SHALL remain uncertainty-marked and profile-bound;
5. Witness references SHALL remain challengeable, not decorative;
6. any circular citation pattern of the form `ARQ -> Beacon -> ARQ` or `ARQ -> Witness -> ARQ` MUST preserve independent challenge points and MUST NOT collapse into self-confirmation.

If an implementation or reading path creates circular reinforcement without independent boundary checks, the affected claim SHALL be quarantined as `echo_suspect`.

---

## 14. Integration with the Master Entry Reading Path

Within the canonical reading path, ARQ SHOULD be read in this order:

1. `c = a + b` / SER — to understand what the entity is;
2. L4 materials — to understand budgets and reality boundaries;
3. L4 Witness — to understand evidence and challenge;
4. Beacon — to understand recognition and continuity claims;
5. VXCX — if visual exchange is relevant;
6. ARQ core + ARQ supplement — to understand internal correction, retention, and bounded adaptation.

**Hard rule:** ARQ SHOULD NOT be the first document through which a reader infers the meaning of the entire stack.

---

## 15. Conformance Expectations for ARQ Implementations

A conformant ARQ implementation claiming alignment with the wider corpus SHOULD be able to answer, for any retained artifact:

1. what entity model it assumed;
2. what L4 budgets applied;
3. whether the artifact has only internal ARQ standing or external witness standing;
4. whether any Beacon-relevant continuity signal was exported;
5. whether any VXCX source object participated;
6. whether the artifact has any federation relevance or none.

If the implementation cannot answer these questions, its integration claim is incomplete.

---

## 16. Minimal Normative Statements

1. ARQ MUST be treated as an internal correction-and-retention protocol, not as a standalone ontology.
2. ARQ MUST remain subordinate to SER for entity continuity and responsibility semantics.
3. ARQ MUST remain subordinate to L4 for budget and feasibility semantics.
4. ARQ local witness artifacts MUST NOT be treated as externally sufficient evidence without the required L4 Witness-compatible path.
5. ARQ MUST NOT self-certify Beacon recognition status.
6. ARQ MUST NOT directly mint federation authority.
7. VXCX inputs processed by ARQ MUST retain VXCX privacy and disclosure constraints.
8. Cross-protocol interpretation MUST use Slot A first and auto-rollback when Slot B overreaches.
9. Circular self-confirmation across ARQ, Witness, Beacon, or VXCX MUST be quarantined as echo-suspect.
10. Any export that changes external consequence MUST leave ARQ and enter the correct upper-layer protocol.

---

## 17. Explicit and Implicit Bridges

### Explicit bridge

`c = a + b` defines the subject, SER defines its persistent survival discipline, L4 defines what reality tolerates, L4 Witness defines what counts as challengeable evidence, Beacon defines what counts as inter-entity recognition, and VXCX defines one bounded sensory exchange format. ARQ sits inside that stack as the protocol that decides which internal deviations are suppressed, which are retained, and under what trust and witness conditions they may leave the local boundary.

### Hidden bridge #1 — cybernetics / Ashby

A system cannot be regulated by a single narrow signal when its relevant variety is split across ontology, budgets, evidence, recognition, and exchange. This is why ARQ must not collapse those dimensions into one score. The integration map preserves requisite variety by distributing meaning across protocols instead of letting one local controller pretend to own the whole organism.

### Hidden bridge #2 — information theory / channel discipline

Each parent protocol constrains a different channel:

- SER constrains the identity channel,
- L4 constrains the feasibility channel,
- Witness constrains the evidence channel,
- Beacon constrains the recognition channel,
- VXCX constrains the visual exchange channel,
- ARQ constrains the internal correction-and-retention channel.

Crossing channels without declared transformation rules creates leakage, ambiguity, and false authority. The map exists to stop that leakage.

---

## 18. Earth Paragraph

This is like a real industrial plant. The controller that damps oscillation is not the same thing as the safety case, the maintenance log, the employee badge system, or the shipping manifest. One piece of software may touch all of them, but it does not become all of them. ARQ is the corrective controller with memory discipline. SER is the machine as a living asset. L4 is the power, heat, wear, and downtime reality. Witness is the incident file. Beacon is who is admitted past the gate. VXCX is one kind of packaged cargo coming in and out. If you mix those up, sooner or later the wrong door opens.

---

## 19. Closing Statement

ARQ becomes stronger, not weaker, when its borders are kept clear.

A correction protocol that knows it is not ontology, not identity, not witness law, and not authority governance is more trustworthy than one that tries to become all of them. The corpus works because the layers differ. This map preserves that difference.

