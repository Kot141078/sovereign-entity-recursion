# ARQ_Classical_Boundedness_Theorem_v0.2
## Classical Boundedness Theorem for the ARQ v0.2 Supplement

**Status:** Draft / normative support document  
**Version:** 0.2-draft  
**Role:** classical boundedness, retention limits, backlog limits, claim discipline  
**Parent documents:** `ARQ_v0.2_Normative_Core.md`, `ARQ_System_Models_and_Assumptions_v0.2.md`, `ARQ_Notation_and_Sign_Conventions_v0.2.md`, `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.md`, `ARQ_Trust_and_Provenance_Profile_v0.2.md`  
**Parent corpus:** AGI / SER / L4 / L4 Witness / Beacon / VXCX  
**Author:** Ivan Kotov  
**Place / year:** Bruxelles, 2026

---

## 0. Abstract

This document states the classical boundedness results for ARQ under explicit model discipline.

The earlier ARQ boundedness intuition was directionally correct: a long-lived entity operating under L4 budgets cannot accumulate authoritative disorder without limit. But that intuition must be decomposed into distinct support claims rather than forced into one universal scalar formula.

This document therefore proves classical boundedness in three separate ways:

1. **authoritative persistent-state boundedness** under Model M1;
2. **commit-metered retained-entropy boundedness** under Model M2;
3. **pending/backlog boundedness** under Model M4.

It then gives a composite corollary for a classical ARQ controller operating inside a valid trust epoch.

The central discipline is simple:

> finite memory bounds authoritative state;  
> finite commit authority bounds retained novelty;  
> finite queue capacity bounds unresolved ambiguity.

Energy and cooling remain operationally important, but in the classical theorem they are used through calibrated commit and epoch assumptions, not as a universal metaphysical entropy meter.

---

## 1. Purpose

This document exists to answer one technical question:

> Under classical ARQ assumptions, what exactly is bounded, by which model, and with what proof shape?

It SHALL provide:

1. a theorem for finite authoritative persistent state;
2. a theorem for commit-metered retained entropy;
3. a theorem for finite pending backlog;
4. a composite corollary for classical ARQ runtime envelopes;
5. a discipline for what this theorem set does **not** claim.

This document is intentionally classical. Quantum finite-boundary results belong to a separate theorem document.

---

## 2. Scope

This document specifies classical boundedness claims for ARQ under the following imported models:

- **Model M1** — classical persistent-state model;
- **Model M2** — commit-metered retention model;
- **Model M3** — epoch-gated trust/control model;
- **Model M4** — online queue/backlog model.

This document does **not** define quantum entropy bounds, usable-entanglement bounds, or full thermodynamic lifetime bounds for arbitrary hardware stacks.

---

## 3. Non-Goals

This document does **not** attempt to:

- prove a universal hardware-independent law of entropy for all persistent entities;
- derive a single global `H_max` from Landauer’s principle alone;
- treat power draw, heat, and memory as one interchangeable scalar;
- bound arbitrary user input streams without a declared queue or retention boundary;
- infer boundedness for untrusted or invalid epochs;
- replace engineering calibration with poetry.

This is a theorem document about **declared classical ARQ models**, not a cosmology of disorder.

---

## 4. Normative Keywords

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, **MAY**, and **OPTIONAL** are to be interpreted as described in BCP 14.

---

## 5. Imported Symbols and Dependencies

This document imports notation and model discipline from the ARQ v0.2 companion set.

At minimum, the following imported symbols SHALL keep their canonical meanings:

- `X_t` — authoritative classical persistent state;
- `M_persist` — number of bits available for authoritative persistent state;
- `C_mode` — finite controller-mode set;
- `H(X)` — Shannon entropy in bits;
- `H_retained(T)` — retained authoritative entropy by horizon `T`;
- `H_pending(t)` — unresolved pending/backlog entropy at time `t`;
- `b_commit,min`, `b_commit,max` — minimum and maximum authoritative bits per commit under the declared profile;
- `e_commit,min` — minimum calibrated commit cost;
- `i_commit,min` — minimum irreversibility expenditure per commit, if that budget is used;
- `N_commit(T)` — number of successful commits by horizon `T`;
- `K` — pending queue capacity;
- `B_max` — maximum pending representation size per unresolved event.

This document depends on the system-model declarations in `ARQ_System_Models_and_Assumptions_v0.2.md`. No theorem herein SHALL be cited without the corresponding model identifier.

---

## 6. Model Carrier Table

| Result | Model carrier | What is bounded | What is **not** bounded by that result alone |
|---|---|---|---|
| Theorem 1 | M1 | authoritative persistent state entropy | number of operations or runtime duration |
| Theorem 2 | M2 | retained authoritative novelty via commits | whole-device thermodynamic disorder |
| Theorem 3 | M4 | unresolved online ambiguity / pending backlog | retained memory after promotion |
| Corollary 1 | M1 + M2 + M3 + M4 | composite classical ARQ runtime envelope in valid epochs | arbitrary invalid or undeclared deployments |

---

## 7. Theorem 1 — Authoritative Persistent-State Bound

### 7.1 Statement

**Theorem 1 (Finite authoritative persistent-state bound).**

Assume Model M1.

Let the authoritative classical persistent state at time `t` be

\[
X_t \in \{0,1\}^{M_{persist}} \times C_{mode},
\]

where:

- `M_persist < ∞` is the number of bits available for authoritative persistent state;
- `C_mode` is a finite controller-mode set.

Then for all `t`:

\[
H(X_t) \le M_{persist} + \log_2 |C_{mode}|.
\]

If `C_mode` is fixed and small, this is effectively:

\[
H(X_t) \le M_{persist} + O(1).
\]

### 7.2 Proof

The support of `X_t` contains at most

\[
2^{M_{persist}}\cdot |C_{mode}|
\]

possible states.

The Shannon entropy of a random variable supported on a finite set `Ω` is maximized by the uniform distribution on `Ω`, with value `log_2 |Ω|`. Therefore,

\[
H(X_t)
\le
\log_2\!\big(2^{M_{persist}}\cdot |C_{mode}|\big)
=
M_{persist} + \log_2 |C_{mode}|.
\]

Hence `H(X_t)` is uniformly bounded for all `t`. ∎

### 7.3 Interpretation

This theorem says exactly one thing:

> if authoritative classical state is finite, its Shannon entropy is finite.

It does **not** say how often state may change, how expensive change is, or how much unresolved ambiguity can exist in flight.

### 7.4 Correction note

If `M_persist` counts **bits**, then the correct upper bound is of order `M_persist`, **not** `log_2 M_persist`.

A `log_2 M` upper bound is valid only when `M` denotes the number of coarse-grained memory states, not the number of memory bits.

---

## 8. Theorem 2 — Commit-Metered Retained-Entropy Bound

### 8.1 Statement

**Theorem 2 (Commit-metered retained-entropy bound).**

Assume Model M2.

Let `H_retained(T)` denote the total authoritative entropy retained in committed ARQ artifacts by horizon `T`.

Assume:

1. every retained authoritative update is implemented by a declared commit primitive;
2. every successful commit contributes at most `b_commit,max` bits of retained authoritative content;
3. each successful commit consumes at least one bounded resource according to the declared profile, such as:
   - at least `b_commit,min > 0` bits of persistent-state headroom,
   - at least `e_commit,min > 0` calibrated commit cost,
   - at least `i_commit,min > 0` irreversibility expenditure, if such a budget is used.

Then the number of successful commits by horizon `T` is bounded by

\[
N_{commit}(T)
\le
\min\!
\left(
\left\lfloor \frac{M_{persist}}{b_{commit,min}} \right\rfloor,
\left\lfloor \frac{E_{commit}(T)}{e_{commit,min}} \right\rfloor,
\left\lfloor \frac{I_{max}(T)}{i_{commit,min}} \right\rfloor
\right),
\]

with unused terms omitted by profile.

Consequently,

\[
H_{retained}(T) - H_{retained}(0)
\le
N_{commit}(T)\cdot b_{commit,max},
\]

and in any case,

\[
H_{retained}(T) \le M_{persist}.
\]

### 8.2 Proof

Each successful commit consumes at least one bounded resource unit under the profile. Therefore the total number of successful commits is bounded by the smallest available resource budget divided by the corresponding per-commit minimum cost.

Since each retained authoritative commit contributes at most `b_commit,max` bits of retained authoritative content, the total retained contribution above the initial retained state satisfies

\[
H_{retained}(T)-H_{retained}(0)
\le
N_{commit}(T)\cdot b_{commit,max}.
\]

Because retained authoritative state is itself stored within finite persistent memory,

\[
H_{retained}(T) \le M_{persist}.
\]

Hence retained authoritative novelty cannot grow without bound. ∎

### 8.3 Interpretation

This theorem does **not** bound all information the system temporarily touches. It bounds only:

- what crosses an authoritative commit boundary,
- what becomes retained ARQ history,
- what can later influence memory authority under witness.

### 8.4 Landauer discipline

Theorem 2 intentionally does **not** state a universal bound of the form

\[
H_{retained}(T) \le \frac{E_{total}}{k_B T \ln 2}.
\]

Such a bound would require stronger assumptions than classical ARQ normally declares, including at minimum:

1. a specific irreversible commit mechanism;
2. a calibrated mapping between retained authoritative bits and physical dissipation;
3. a declared thermal operating regime;
4. a declared dissipation path;
5. a finite horizon or non-replenished energy budget relevant to the commit process.

Without those assumptions, energy gives a **rate / resource bound on commits**, not a universal abstract entropy oracle.

---

## 9. Theorem 3 — Pending / Backlog Bound

### 9.1 Statement

**Theorem 3 (Finite pending-backlog bound).**

Assume Model M4.

Let the ARQ implementation maintain an unresolved pending-event structure with capacity `K < ∞`, where each unresolved event occupies at most `B_max < ∞` bits of queue-accounted pending representation.

Then for all `t`:

\[
H_{pending}(t) \le K \cdot B_{max}.
\]

### 9.2 Proof

At time `t`, the pending structure contains at most `K` unresolved entries. Each entry contributes at most `B_max` bits of pending representation. Therefore the total pending representation is bounded by `K \cdot B_max` bits.

The Shannon entropy of a variable represented within at most `K \cdot B_max` bits is bounded by that many bits. Hence

\[
H_{pending}(t) \le K \cdot B_{max}.
\]

So unresolved online ambiguity cannot accumulate without bound inside the declared queue. ∎

### 9.3 Interpretation

This theorem is about **in-flight unresolved disturbance**, not authoritative retained memory.

It is the right theorem for claims such as:

- “the controller cannot accumulate unbounded unresolved ambiguity,”
- “observation windows are bounded,”
- “witness flooding cannot produce infinite pending state if the pending representation is finite and capped.”

### 9.4 Overflow consequence

If the queue reaches `K`, the implementation MUST follow its declared overflow semantics, such as:

- degrade new events to `log_only`,
- reject candidate promotion,
- evict only non-authoritative pending entries,
- reduce privilege,
- or fail closed if safe judgment is no longer credible.

This overflow rule is a safety consequence of the theorem, not an optional decoration.

---

## 10. Corollary 1 — Composite Classical ARQ Runtime Envelope

### 10.1 Statement

**Corollary 1 (Composite classical ARQ runtime bound in valid epochs).**

Assume Models M1, M2, M3, and M4.

Let a classical ARQ implementation operate inside a valid epoch `k`. Let its runtime envelope be represented by

\[
Y_t = (X_t, Q_t),
\]

where:

- `X_t` is the authoritative persistent state from Model M1;
- `Q_t` is the unresolved pending/backlog state from Model M4.

Then, during any valid epoch,

\[
H(Y_t)
\le
M_{persist} + \log_2 |C_{mode}| + K\cdot B_{max}.
\]

Moreover, the retained authoritative contribution remains commit-bounded as in Theorem 2.

### 10.2 Proof

By Theorem 1,

\[
H(X_t) \le M_{persist} + \log_2 |C_{mode}|.
\]

By Theorem 3,

\[
H_{pending}(t) \le K\cdot B_{max}.
\]

Treating `Y_t` as the declared classical runtime envelope consisting of authoritative persistent state and pending unresolved state, a loose bound is given by the sum of the component bounds:

\[
H(Y_t)
\le
M_{persist} + \log_2 |C_{mode}| + K\cdot B_{max}.
\]

By Theorem 2, any retained authoritative novelty remains bounded by commit authority and finite persistent memory.

Model M3 then restricts the validity of this envelope to valid epochs only: outside a valid epoch, normal ARQ authority is withdrawn and the system MUST degrade or fail closed. ∎

### 10.3 Meaning

This corollary gives the right classical reading of ARQ boundedness:

- **persistent authority is finite;**
- **retained novelty is finite;**
- **pending ambiguity is finite;**
- **normal authority is epoch-bounded.**

That is enough to block runaway classical ARQ disorder under declared assumptions.

---

## 11. What This Document Does **Not** Prove

This theorem set does **not** prove any of the following unless stronger assumptions are explicitly declared elsewhere:

1. one universal thermodynamic scalar bound for all classical deployments;
2. a whole-device heat/entropy theorem for arbitrary hardware;
3. boundedness of undeclared external logs treated as if they were “inside” authoritative memory;
4. boundedness under invalid or adversarially broken trust epochs;
5. boundedness of arbitrary user input streams without queueing, rejection, or commit discipline;
6. anything about quantum entropy or usable entanglement.

**Hard anti-overclaim rule:**
No document in the ARQ supplement SHALL cite this theorem set as if it proved a global physical law beyond Models M1–M4.

---

## 12. Engineering Consequences

### 12.1 Memory accounting is not optional

If the implementation cannot say what counts toward `M_persist`, then Theorems 1 and 2 are not applicable.

### 12.2 Commit calibration matters

If there is no declared commit primitive, then “retained novelty” collapses into narrative fog. Theorem 2 applies only where retention crosses an identifiable authority boundary.

### 12.3 Queue discipline matters

If pending ambiguity is unbounded in practice, then online ARQ stability is undefined in practice, regardless of elegant philosophy.

### 12.4 Epoch discipline matters

Trust loss does not merely lower confidence; it changes the admissible state set. ARQ is bounded in operation because invalid epochs remove promotion authority.

---

## 13. Proof Maintenance Discipline

### 13.1 Anti-echo rule

A revised proof claim SHALL NOT be promoted merely because it rephrases “finite resources imply boundedness” in prettier language.

A revision SHOULD be treated as theorem-progress only if it adds at least one of:

- a clearer model boundary;
- a corrected variable meaning;
- a stronger proof under the same assumptions;
- a weaker theorem with more honest assumptions;
- or a new explicit non-theorem limitation.

### 13.2 A/B-slot proof editing

Proof revisions SHOULD use:

- **Slot A** — current canonical theorem text;
- **Slot B** — proposed revision.

A revision may replace Slot A only if:

1. it preserves all valid earlier claims;
2. it reduces ambiguity or overclaim;
3. it does not silently strengthen assumptions;
4. it is reviewable against the model carrier table.

If a proposed revision increases elegance but reduces claim honesty, it MUST be rolled back automatically.

---

## 14. Bridges (required)

### Explicit bridge

ARQ boundedness in the classical regime is not one theorem but a stitched control surface:

- M1 bounds authoritative persistent state,
- M2 bounds retained novelty through commit authority,
- M4 bounds unresolved ambiguity in flight,
- M3 bounds the validity of normal operation through trust epochs.

Together they make the ARQ claim operational:

> continuity is bounded not by hope, but by memory authority, commit authority, queue capacity, and epoch validity.

### Hidden bridge 1 — Cybernetics / Ashby

A regulator must match the variety of the process it regulates. One scalar “entropy bound” is too poor a regulator for a system whose risks separate into persistent state, retention, backlog, and trust epoch. The decomposition into M1–M4 is not stylistic; it is requisite variety for honest control.

### Hidden bridge 2 — Information theory

Information enters a system in stages: represented, queued, committed, retained. Conflating those stages destroys accounting. The classical theorem set works only because it keeps `H(X_t)`, `H_pending(t)`, and `H_retained(T)` distinct.

---

## 15. Earth Paragraph

A real machine does not “accumulate entropy” in one poetic bucket. It has a disk that fills, a queue that backs up, a controller that loses authority when calibration or trust breaks, and commits that cost time, wear, and headroom. That is why the classical ARQ theorem is split: one bound for what is officially stored, one for what is still waiting in the hallway, and one for what is allowed to become history. If you mix those three, you do not get a deeper theorem; you just get accounting fraud.

---

## 16. Minimal Citation Map

This document is designed to be read together with:

- `ARQ_v0.2_Normative_Core.md`
- `ARQ_System_Models_and_Assumptions_v0.2.md`
- `ARQ_Notation_and_Sign_Conventions_v0.2.md`
- `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.md`
- `ARQ_Trust_and_Provenance_Profile_v0.2.md`
- `ARQ_Quantum_Boundary_Theorem_v0.2.md` (separate quantum theorem companion)

