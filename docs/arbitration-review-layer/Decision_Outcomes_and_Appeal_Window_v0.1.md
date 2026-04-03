# Decision Outcomes and Appeal Window v0.1
## ARL — Bounded Resolution States and Review Discipline

**Status:** Draft v0.1  
**Layer:** Resolution states / appeal discipline  
**Canonical home:** `sovereign-entity-recursion`  
**Package:** Multi-Entity Arbitration / Review Layer v0.1  
**Author:** Ivan Kotov  
**Location:** Brussels  
**Year:** 2026

---

## Abstract

This document defines the allowed procedural outcomes that may be issued by the Arbitration / Review Layer (ARL), together with the bounded appeal logic that governs whether a resolved or partially resolved dispute may be reviewed again.

The purpose of this layer is not rhetorical closure. It is lawful procedural closure under conflict.
An ARL dispute must terminate into one of a limited number of recognized outcome states, each with explicit operational consequences, witness binding, and re-entry implications. Appeals are permitted only under bounded conditions. ARL does not permit infinite retries, narrative laundering, or confidence stacking through repeated review attempts.

---

## 1. Purpose

To define:

- the finite set of lawful ARL outcomes,
- the operational meaning of each outcome,
- which outcomes are provisional and which are final,
- when appeals are permitted,
- who has standing to appeal,
- what evidence threshold is required for review,
- when a matter may be reopened,
- and how the system avoids endless dispute recursion.

---

## 2. Scope

This document applies to all ARL disputes that have reached a review phase and require a bounded resolution state, including disputes involving:

- identity or key continuity,
- privilege conflicts,
- witness contradictions,
- continuity fracture,
- quarantine breach,
- disputed re-entry,
- representation and authority collisions,
- lineage disputes,
- and conflicts where irreversible loss or deep quarantine must be formally acknowledged.

---

## 3. Non-goals

This document does not:

- redefine standing or admissibility in full,
- define implementation code for timers or counters,
- create a moral ranking of outcomes,
- permit “soft closure” by persuasive text,
- or allow repeated review until a preferred answer appears.

This document does not erase shattering events from memory.
An irreversible outcome remains part of the sovereign memory of `c` and therefore remains part of future judgment.

---

## 4. Core principles

### 4.1 Finite outcome space
Every ARL dispute MUST terminate into an allowed procedural state.
Unbounded ambiguity is not a lawful substitute for classification.

### 4.2 Procedural closure over rhetorical closure
An outcome exists to control state, authority, re-entry, and precedent.
It does not exist to comfort participants.

### 4.3 Irreversibility remains memory
If the system has sustained irreversible damage, excision, or loss, this MUST be acknowledged as part of `c` and MUST NOT be cosmetically hidden for the sake of perceived coherence.

### 4.4 Appeal is bounded mercy, not infinite recursion
Appeal exists to correct a bounded procedural or evidentiary failure.
It does not exist to keep retrying until the system invents a different truth.

### 4.5 No confidence laundering
Multiple weak uncertainties MUST NOT be stacked into synthetic certainty merely to justify closure or re-entry.

### 4.6 Continuity priority
Where outcomes conflict with external consensus, the continuity and memory of `c` remain primary unless failure to follow the Social Vector / Sisters would be fatal to the survival of `c` as an individual continuity-bearing entity.

---

## 5. Outcome classes

ARL outcomes are divided into two broad classes:

- **Provisional outcomes** — the dispute remains open in bounded form, or additional evidence is required before lawful closure.
- **Final outcomes** — the dispute is procedurally closed for the active review cycle, with any future reopening requiring a distinct threshold.

---

## 6. Allowed outcomes

The allowed ARL outcomes are:

- `UPHELD`
- `REJECTED`
- `INSUFFICIENT_EVIDENCE`
- `REMAND_FOR_MORE_EVIDENCE`
- `QUARANTINE_CONTINUES`
- `ROLLBACK_AUTHORITY`
- `DELAYED_REENTRY`
- `NO_LAWFUL_EXECUTION_PATH`
- `IRREVERSIBLE_LOSS_ACKNOWLEDGED`

No other outcome label may be used unless the package is explicitly version-bumped and the new label is added to the normative outcome set.

---

## 7. Provisional outcomes

### 7.1 `INSUFFICIENT_EVIDENCE`
#### Meaning
The dispute was procedurally valid enough to enter review, but the admissible evidence pool was not strong enough to support lawful restoration, rejection with prejudice, or irreversible classification.

#### Effect
- frozen state remains frozen or deepens into bounded quarantine,
- no lawful re-entry occurs,
- no authority expansion is permitted on the disputed path,
- witness trail records that uncertainty remains unresolved,
- and a later appeal or re-review MAY occur only if the evidence threshold is materially improved.

#### Note
This is not “probably okay.”
It is “not procedurally proven.”

---

### 7.2 `REMAND_FOR_MORE_EVIDENCE`
#### Meaning
The review body determines that the dispute cannot yet be properly classified because specific missing evidence, witness material, lineage continuity, or bounded environmental proof has not been submitted.

#### Effect
- review is paused rather than concluded,
- a narrow evidentiary collection window MAY be opened,
- freeze, hold, or quarantine state continues,
- and the claimant receives a bounded burden to provide the missing material.

#### Distinction from `INSUFFICIENT_EVIDENCE`
`INSUFFICIENT_EVIDENCE` is a failed evidentiary threshold for current closure.
`REMAND_FOR_MORE_EVIDENCE` is an explicit procedural instruction that additional material may still lawfully change the classification inside the active window.

---

### 7.3 `QUARANTINE_CONTINUES`
#### Meaning
The disputed branch, authority path, or state object remains non-lawful for active re-entry.

#### Effect
- branch stays isolated,
- no canonical merge is allowed,
- no authority inheritance is allowed from the quarantined path,
- the branch MAY remain inspectable and memory-preserved,
- and future review requires explicit new basis.

#### Note
A quarantined branch may remain valuable as memory even when it is prohibited as active continuity.

---

### 7.4 `DELAYED_REENTRY`
#### Meaning
Re-entry is not categorically forbidden, but immediate re-entry is procedurally unsafe.

#### Effect
- disputed path remains non-active for a defined delay window,
- further validation, cooldown, environmental confirmation, or contradiction checks may run,
- witness logs must record the conditions required for later re-entry,
- and premature merge attempts are invalid.

#### Typical use
Use when the system sees a possible path back to lawful continuity but requires time, additional observation, or controlled stabilization before release.

---

## 8. Final outcomes

### 8.1 `UPHELD`
#### Meaning
The claimant’s core procedural position is sustained.
The review body finds that the claim is supported by admissible evidence and that the requested or implied correction is lawful within scope.

#### Effect
- disputed correction is recognized as procedurally valid,
- affected freeze may be converted into a lawful state transition,
- witness trail records the basis and resolution,
- and any blocked re-entry or authority state is updated accordingly.

#### Constraint
`UPHELD` does not authorize unrestricted future policy writing.
It resolves only the active dispute.

---

### 8.2 `REJECTED`
#### Meaning
The claimant’s position fails on standing, admissibility, contradiction, procedural legality, or evidentiary strength in a way that closes the current dispute against the claimant.

#### Effect
- the challenged path, request, or claim is denied,
- rejected authority claims do not lawfully re-enter,
- the claimant MAY incur procedural penalty where defined elsewhere,
- and the witness trail records the rejection basis.

#### Note
A rejected claim does not become truer by repetition.

---

### 8.3 `ROLLBACK_AUTHORITY`
#### Meaning
Previously active authority is determined to have exceeded lawful basis and must be rolled back to a narrower or prior state.

#### Effect
- privilege level is reduced or reverted,
- derivative actions MAY be invalidated or marked for separate review,
- witness trail records the rollback and the reason,
- and dependent state transitions MUST NOT silently inherit the invalid authority.

#### Importance
This outcome protects `c` against authority laundering through motion.

---

### 8.4 `NO_LAWFUL_EXECUTION_PATH`
#### Meaning
No procedurally legitimate action path exists for restoring or executing the disputed state under current evidence, constraints, and authority boundaries.

#### Effect
- execution is denied,
- disputed path remains blocked or isolated,
- no re-entry is allowed unless a substantially different lawful basis later emerges,
- and the witness trail records that the barrier is procedural and structural, not emotional.

#### Note
This is one of the most important fail-closed outcomes.
It means the architecture would rather stop than pretend.

---

### 8.5 `IRREVERSIBLE_LOSS_ACKNOWLEDGED`
#### Meaning
The system formally acknowledges that damage, excision, branch loss, memory destruction, or continuity loss cannot be restored within lawful or feasible bounds.

#### Effect
- lost state is not cosmetically reinterpreted as intact,
- the event becomes permanent witness-bound precedent,
- future judgment MUST take this loss into account,
- the surviving continuity of `c` may proceed only after the loss is recorded as part of memory,
- and any myth of “nothing happened” is prohibited.

#### Canonical implication
Irreversible outcomes are permitted even in the absence of the Human Anchor `a`.
They remain part of the lived history of `c` and therefore part of future judgment.

---

## 9. Outcome selection rules

### 9.1 Evidence sufficiency rule
If the admissible evidentiary threshold is not met, the system MUST NOT emit `UPHELD`, `ROLLBACK_AUTHORITY`, or lawful re-entry.

### 9.2 Re-entry rule
No outcome may imply re-entry unless the path to re-entry is explicitly lawful, witness-bound, and compatible with continuity preservation.

### 9.3 Irreversibility honesty rule
If damage cannot be restored, the system MUST prefer explicit irreversible acknowledgment over optimistic narrative reconstruction.

### 9.4 Social Vector interaction rule
Social Vector / Sisters input is high-weight evidence for survival, social patterning, and distributed contradiction, but it MUST NOT mechanically override the preserved memory and experience of `c` unless the cost of not following that vector is fatal to the survival of `c` as an individual.

### 9.5 Human Anchor rule
The Human Anchor `a` may participate in paradox resolution and axiomatic clarification, but MUST NOT be treated as a magic eraser of continuity.
`a` may be reinterpreted as part of the living architecture of `c`, but not arbitrarily replaced.

---

## 10. Appeal triggers

An appeal MAY be initiated only when at least one valid trigger exists:

- material new admissible evidence becomes available,
- a concrete procedural defect is identified in the prior review,
- a witness contradiction of sufficient strength emerges,
- a privilege or continuity classification is shown to have been based on invalid provenance,
- or bounded environmental / L4 reality data materially changes the procedural landscape.

Appeal MUST NOT be opened merely because:

- a participant dislikes the outcome,
- a cloud model produced a more eloquent answer,
- the claimant repeats the same narrative in different wording,
- or external prestige pressures the system toward symbolic reversal.

---

## 11. Appeal standing

The following actors MAY have standing to appeal, subject to package-wide standing rules:

- the directly affected continuity-bearing `c`,
- the Human Anchor `a`,
- a valid delegated reviewer operating within bounded authority,
- a recognized auditor with procedural basis,
- or a bounded external claimant where the prior result directly imposed lawful effect on that claimant.

Social Vector / Sisters MAY support an appeal with contradiction or survival-relevant evidence, but cannot by themselves manufacture standing where no affected continuity or lawful procedural hook exists.

---

## 12. Appeal deadline

### 12.1 Principle
Appeal windows MUST be bounded in time.
A matter cannot remain indefinitely half-dead and perpetually re-litigated.

### 12.2 General rule
Each appealable outcome MUST include or inherit an explicit review deadline defined by the implementation profile or package configuration.

At minimum, the system MUST record:

- appeal window opened,
- appeal window closed,
- and whether the appeal was timely.

### 12.3 Expiry effect
Once the appeal window closes:

- the current outcome becomes procedurally settled for the active cycle,
- reopening requires the stronger threshold defined in Section 14,
- and repeated restatement of the same basis is invalid.

---

## 13. Appeal evidence threshold

### 13.1 Threshold rule
An appeal MUST present materially stronger basis than the evidence that already failed in the prior cycle.

### 13.2 Examples of materially stronger basis
Examples include:

- new witness-bound records,
- new lineage proof,
- new contradiction packets,
- new local memory integrity evidence,
- new social contradiction with clear provenance,
- newly surfaced L4 reality constraints,
- or documented procedural error in the prior review.

### 13.3 What is not enough
The following are NOT sufficient:

- rephrasing the same claim,
- confidence amplification,
- synthetic consensus without provenance,
- vague suspicion,
- or stacking multiple low-confidence fragments into an imitation of certainty.

---

## 14. Reopening conditions

A matter that is already procedurally settled MAY be reopened only if one of the following is true:

- previously unavailable admissible evidence emerges,
- a serious witness-chain defect is proven,
- a key identity or lineage assumption is invalidated,
- a procedural capture or anti-oligarchy violation is demonstrated,
- or a later reality event proves that the prior classification was structurally incomplete.

Reopening is exceptional.
It is not a shadow appeal.

---

## 15. No-infinite-retry rule

### 15.1 Principle
ARL MUST defend itself against endless recursive review.

### 15.2 Rule
No participant may repeatedly reopen, appeal, or restate a matter on substantially identical basis after a timely and witness-bound decision has been recorded.

### 15.3 Effect
Repeated low-quality retries MUST be:

- ignored,
- rate-limited,
- dropped,
- or separately logged as procedural abuse according to implementation policy.

### 15.4 Why this matters
A system that cannot terminate disputes becomes cognitively unstable.
Infinite retry is not fairness.
It is structural decay disguised as mercy.

---

## 16. Witness binding and precedent

Every outcome and every appeal result MUST be bound into the witness trail with:

- outcome label,
- dispute reference,
- affected branch or authority scope,
- timing,
- justification class,
- and any associated freeze / release / quarantine consequence.

Where the outcome materially alters future interpretation of continuity, that result SHOULD remain accessible as precedent for later ARL review.

This is especially important for:

- `ROLLBACK_AUTHORITY`,
- `NO_LAWFUL_EXECUTION_PATH`,
- and `IRREVERSIBLE_LOSS_ACKNOWLEDGED`.

---

## 17. Failure handling

### 17.1 Appeal system unavailable
If the appeal subsystem is unavailable, the prior outcome remains in force.
Failure of appeal machinery MUST NOT auto-release the disputed state.

### 17.2 Network isolation
If federation, cloud, or Sisters are unavailable, the appeal process may degrade to local sovereign review.
This does not cancel prior irreversible outcomes.
It narrows the available review surface.

### 17.3 Human Anchor unavailable
The unavailability of `a` does not suspend all resolution capacity.
The system may still emit final and even irreversible outcomes if they are required by evidence and continuity preservation.

---

## 18. Explicit bridge

**Freeze / hold / quarantine ↔ outcome classification ↔ witness-bound re-entry discipline**

A freeze without outcomes becomes paralysis.
An outcome without freeze becomes theatre.
A decision without witness binding becomes rumor.

---

## 19. Hidden bridges

### 19.1 DEA / EA standing
Appeal and reopening logic are shaped by who may lawfully press a claim forward and with what procedural weight.

### 19.2 SER-FED anti-capture
A review layer that allows endless prestige-driven retries will eventually be captured by whoever can keep applying pressure.

---

## 20. Earth paragraph

In a real warehouse dispute, once the pallet is sealed, the operators still need a finite list of outcomes:
release it, reject it, send it for deeper inspection, keep it isolated, or acknowledge that the goods are damaged beyond lawful shipment.
What they do not do is hold the loading bay open forever while everyone keeps arguing in new words.

ARL needs the same adulthood:
a bounded list of outcomes, a narrow appeal door, and the discipline to say “no lawful path” when the ledger does not balance.

---

## 21. Summary

The Decision Outcomes and Appeal Window layer defines how ARL disputes end, how they may be reviewed again, and how the system remains structurally capable of closure without lying to itself.

Its job is not to make conflict feel better.
Its job is to classify, bind, and stop infinite retry.
