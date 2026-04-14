# ARQ v0.2 Supplement — CHANGELOG
## Delta record for the ARQ v0.2 supplement package

**Status:** Draft / release changelog  
**Version:** 0.2-draft  
**Compared against:** ARQ v0.1 corpus and related early notes  
**Author:** Ivan Kotov  
**Place / year:** Bruxelles, 2026

---

## 0. Scope of this changelog

This file records the major structural and interpretive delta between:

- the earlier ARQ v0.1 material,
- and the ARQ v0.2 supplement package.

It is **not** a substitute for the normative documents.

Its job is narrower:

- state what was added,
- state what was corrected,
- state what changed in interpretation,
- and state what remained intentionally unchanged.

---

## 1. Added in v0.2

### 1.1 New package structure
Added a release-grade supplement package with separate documents for:

- normative core,
- system models and assumptions,
- notation and sign conventions,
- error valuation and anomaly scoring,
- EA lifecycle and witness binding,
- classical boundedness theorem,
- classical theorem proof companion,
- quantum boundary theorem,
- quantum theorem proof companion,
- capsule and witness schemas,
- classical implementation profiles,
- failure modes and safe degradation,
- integration map,
- test / audit / conformance matrix,
- and release-layer documents.

### 1.2 Release layer
Added:

- executive summary,
- repository README,
- doc map,
- changelog,
- SHA-256 manifest,
- Zenodo metadata draft.

---

## 2. Changed in v0.2

### 2.1 Normative separation
**Changed:** ARQ is no longer presented as one mixed document carrying core protocol, mathematics, proofs, and practical examples all at once.

**Now:**

- `ARQ_v0.2_Normative_Core.md` carries normative operational logic;
- proof and model claims live in companion documents;
- implementation and audit material live in separate files.

### 2.2 Explicit model discipline
**Changed:** system assumptions are now declared before boundedness and valuation claims are made.

**Now:** ARQ explicitly distinguishes between:

- classical persistent-state model,
- commit-metered retention model,
- epoch-gated trust/control model,
- queue/backlog model,
- fixed trusted quantum boundary model.

### 2.3 Stabilized notation
**Changed:** sign and symbol conventions are stabilized.

**Now:** the package explicitly separates:

- exploration-oriented entropy terms,
- ordering/coherence-oriented entropy terms,
- raw value,
- trust-adjusted value,
- anomaly score vs posterior probability,
- retained state vs pending queue state.

### 2.4 Trust-sensitive promotion
**Changed:** a high value score is no longer treated as sufficient for authoritative memory promotion.

**Now:** promotion requires a compound gate involving:

- trust validity,
- witness sufficiency,
- review survival,
- privilege legitimacy,
- and staged lifecycle advancement.

### 2.5 Lifecycle staging
**Changed:** the path from deviation to Experience Artifact is explicitly staged.

**Now:** ARQ uses states such as:

- `candidate_artifact`,
- `provisional_artifact`,
- `confirmed_EA`,
- `retired_EA`,
- `compacted_EA`.

### 2.6 Failure and degradation
**Changed:** failure is no longer only implied through “fail closed” language.

**Now:** failure modes and degradation states are explicitly modeled and mapped.

### 2.7 Conformance and auditability
**Changed:** implementation correctness is no longer left as an informal consequence.

**Now:** there is an explicit test, audit, and conformance matrix.

---

## 3. Corrected in v0.2

### 3.1 Classical boundedness interpretation
**Corrected:** classical boundedness claims now distinguish between:

- finite authoritative persistent state,
- bounded retained commits,
- bounded unresolved queue state,
- and trust-valid epoch operation.

**Practical consequence:** the earlier tendency to compress all boundedness into one overly broad formula is removed.

### 3.2 Memory-bound interpretation
**Corrected:** the supplement no longer casually treats all “memory bound” language as equivalent.

**Now:**

- memory state-space bound,
- retained artifact bound,
- and pending queue bound

are handled separately.

### 3.3 Quantum boundedness branch
**Corrected:** quantum boundedness is no longer mixed into the classical theorem as a vague thermodynamic analogy.

**Now:** a separate theorem states that internal entropy and usable entanglement are bounded by the dimension of the declared trusted quantum boundary.

### 3.4 Anomaly language
**Corrected:** “anomaly prior” is no longer allowed to float ambiguously between heuristic score and proper probability claim.

**Now:** ARQ distinguishes:

- operational anomaly score,
- and Bayesian posterior only in the explicitly Bayesian profile.

---

## 4. Clarified in v0.2

### 4.1 ARQ does not redefine ontology
Clarified that ARQ does **not** redefine `c = a + b`, sovereignty, or long-lived continuity. Those remain upstream in the broader corpus.

### 4.2 ARQ does not self-issue authority
Clarified that ARQ may emit bounded internal memory claims, but broader authority consequences remain outside ARQ and must pass through witness- and reality-bound paths.

### 4.3 ARQ and Beacon
Clarified that ARQ can emit continuity-relevant signals, but it is not an identity profile and does not replace Beacon.

### 4.4 ARQ and VXCX
Clarified that visual deviations may enter ARQ, but ARQ does not weaken privacy, export, disclosure, or capsule discipline defined in VXCX.

---

## 5. Not changed in v0.2

The following core convictions remain intentionally unchanged:

1. **Not every deviation is harmful.**  
   Some are exploratory and may matter.

2. **Not every exploratory deviation deserves memory.**  
   Authority remains rare.

3. **Boundaries, budgets, and witness remain central.**  
   ARQ stays reality-bound.

4. **Human responsibility remains structurally coupled.**  
   ARQ does not dissolve anchor responsibility.

5. **Fail-closed behavior remains essential.**  
   When trust or budgets collapse, authority must shrink rather than improvise.

---

## 6. Interpretive breaking changes

These are not “breaking” in file-format terms, but they are breaking in how the package should be read.

### 6.1 No more shortcut from score to EA
Earlier readings could still drift toward: “interesting high-scoring deviation -> experience.”

That shortcut is no longer valid.

### 6.2 No more one-theorem-for-everything reading
The package now insists that a theorem must name its model.

### 6.3 No more trust-by-narrative reading
Narrative coherence is not enough. Trust requires boundary validity, witness sufficiency, and promotion authority conditions.

### 6.4 No more “the queue doesn’t matter” reading
Online backlog is now explicitly part of boundedness and safety reasoning.

---

## 7. Migration note for repository maintainers

When upgrading a repository from ARQ v0.1-style material to the v0.2 supplement package:

1. retain the historical v0.1 material as earlier-stage documents;
2. treat v0.2 as the new canonical supplement layer;
3. update root README links and doc maps;
4. attach a hash manifest for the full supplement package;
5. avoid mixing v0.1 formulas into v0.2 docs without explicit note.

---

## 8. Closing note

The most important change is not cosmetic.

ARQ v0.2 stops assuming that a clever reader will reconstruct all the missing discipline automatically.

The package now says the quiet parts out loud.

---

## Bridges (required)

**Explicit bridge:** the changelog connects the early ARQ notes to the full AGI / SER / L4 discipline by showing how deviation handling was tightened until it matched the rest of the corpus: bounded, witnessed, non-mythological, and publishable.

**Hidden bridge #1 (Ashby / anti-fragile regulation):** the protocol had to gain more internal structure because the environment of interpretation got harsher. The change log is therefore not bookkeeping only; it is a record of increased regulatory variety in response to increased ambiguity.

**Hidden bridge #2 (information theory / correction of drift):** versioning is error correction for documentation. Without a delta record, readers silently mix old semantics and new semantics and produce interpretive corruption.

---

## Earth paragraph

Anyone who has rebuilt a machine knows the difference between “it mostly works” and “every hose, connector, and fuse is now labelled.” v0.2 is that second moment. The machine may not look more glamorous, but it is much harder to miswire.
