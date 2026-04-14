# ARQ_Quantum_Boundary_Theorem_v0.2
## Quantum Boundary Theorem for the ARQ v0.2 Supplement

**Status:** Draft / normative support document  
**Version:** 0.2-draft  
**Role:** quantum finite-boundary boundedness, usable-entanglement bound, epoch-qualified claim discipline  
**Parent documents:** `ARQ_v0.2_Normative_Core.md`, `ARQ_System_Models_and_Assumptions_v0.2.md`, `ARQ_Notation_and_Sign_Conventions_v0.2.md`, `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.md`, `ARQ_Trust_and_Provenance_Profile_v0.2.md`  
**Parent corpus:** AGI / SER / L4 / L4 Witness / Beacon / VXCX  
**Author:** Ivan Kotov  
**Place / year:** Bruxelles, 2026

---

## 0. Abstract

This document states the quantum boundedness results for ARQ under the **fixed trusted quantum boundary** model.

The earlier ARQ quantum note correctly distinguished two things:

- destructive entanglement with the uncontrolled environment,
- constructive entanglement that remains inside a trusted control boundary.

What was still missing was a clean theorem shape.

This document supplies that shape.

Its central claim is not thermodynamic and not mystical:

> if ARQ valuation is performed only inside a fixed finite-dimensional trusted quantum boundary, then both internal boundary entropy and usable entanglement are bounded by boundary dimension.

This is therefore a **finite-boundary theorem**, not an energy-budget theorem.

Energy, cooling, calibration drift, tomography cost, and controller latency remain operationally important, but they enter through epoch validity, estimation quality, and fail-closed transitions—not through the dimensional upper bound itself.

---

## 1. Purpose

This document exists to answer one technical question:

> Under quantum ARQ assumptions, what exactly is bounded by finite trusted-boundary dimension, and what is not?

It SHALL provide:

1. a theorem for entropy boundedness on the trusted quantum boundary;
2. a theorem for usable-entanglement boundedness inside that boundary;
3. a qubit-level corollary for practical ARQ architectures;
4. an epoch-qualified operational rule for when the theorem may be invoked;
5. a discipline for what this theorem set does **not** claim.

This document is intentionally quantum and boundary-specific. Classical persistent-state and commit-metered results belong to the classical boundedness documents.

---

## 2. Scope

This document specifies quantum boundedness claims for ARQ under the following imported models:

- **Model M5** — fixed trusted quantum boundary model;
- **Model M3** — epoch-gated trust/control model.

This document applies when:

- the trusted system register and trusted ancilla map are explicitly declared;
- valuation is performed only on states and correlations inside the declared trusted boundary;
- the active trust epoch remains valid.

This document does **not** define full thermodynamic lifetime bounds, arbitrary open-system disorder bounds, or hardware-independent guarantees of exploitability.

---

## 3. Non-Goals

This document does **not** attempt to:

- prove a universal quantum entropy law for all persistent entities;
- derive usable-entanglement ceilings from power draw or cooling alone;
- treat uncontrolled environment correlation as ARQ value;
- prove that bounded entanglement is therefore cheap to estimate;
- prove that every nonzero `E_use` is operationally useful;
- replace trust-profile invalidation logic with symbolic elegance.

A finite boundary is not a magic wand.

---

## 4. Normative Keywords

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, **MAY**, and **OPTIONAL** are to be interpreted as described in BCP 14.

---

## 5. Imported Symbols and Dependencies

This document imports notation and model discipline from the ARQ v0.2 companion set.

At minimum, the following imported symbols SHALL keep their canonical meanings:

- `\mathcal H_S` — system Hilbert space;
- `\mathcal H_A` — trusted ancilla Hilbert space;
- `\mathcal H_U` — uncontrolled environment Hilbert space;
- `\mathcal H_{SA} = \mathcal H_S \otimes \mathcal H_A` — trusted quantum boundary;
- `d_S = \dim(\mathcal H_S)`;
- `d_A = \dim(\mathcal H_A)`;
- `d_{SA} = \dim(\mathcal H_{SA})`;
- `\rho(t)` — density operator of the full quantum or hybrid system;
- `\rho_{SA}(t)` — reduced state on the trusted quantum boundary;
- `\rho_S(t)` — reduced state on the system register;
- `S(\rho)` — von Neumann entropy in bits;
- `E_use(\rho)` — usable entanglement inside the trusted boundary;
- `e_k` — active trust / calibration epoch identifier.

This document depends on:

- `ARQ_System_Models_and_Assumptions_v0.2.md` for the meaning of Model M5 and M3;
- `ARQ_Notation_and_Sign_Conventions_v0.2.md` for entropy and entanglement symbols;
- `ARQ_Trust_and_Provenance_Profile_v0.2.md` for epoch validity and fail-closed conditions;
- `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.md` for how `E_use` enters valuation.

No theorem herein SHALL be cited without the corresponding model identifiers.

---

## 6. Model Carrier Table

| Result | Model carrier | What is bounded | What is **not** bounded by that result alone |
|---|---|---|---|
| Theorem 1 | M5 | internal entropy of the trusted quantum boundary | runtime, energy spend, or estimation cost |
| Theorem 2 | M5 | usable entanglement inside the trusted boundary | exploitability under drift, latency, or low trust |
| Corollary 1 | M5 | qubit-level explicit ceilings | validity after boundary expansion or epoch break |
| Corollary 2 | M3 + M5 | when the theorem may authorize ARQ valuation | behavior outside valid trust epochs |

---

## 7. Declared Setting

### 7.1 Total Hilbert space

The total Hilbert space is

\[
\mathcal H = \mathcal H_{SA} \otimes \mathcal H_U,
\]

with

\[
\mathcal H_{SA} = \mathcal H_S \otimes \mathcal H_A,
\]

where:

- `S` = system register of interest,
- `A` = trusted ancilla boundary,
- `U` = uncontrolled environment.

### 7.2 Reduced trusted-boundary state

The reduced state on the trusted quantum boundary is

\[
\rho_{SA}(t)=\operatorname{Tr}_U\,\rho(t).
\]

The reduced state on the system register is

\[
\rho_S(t)=\operatorname{Tr}_{AU}\,\rho(t).
\]

### 7.3 Admissible ancilla subsets

Let `\mathfrak A` be the declared family of admissible trusted ancilla subsets.

For each `A' \in \mathfrak A`, the induced bipartite state is

\[
\rho_{S:A'}(t).
\]

### 7.4 Epoch-qualified assumption

All theorem invocations in this document are valid only during a trust-valid epoch `e_k` under Model M3.

If the active epoch is invalidated, or if the trusted ancilla map changes without a new valid epoch, the theorem MAY remain mathematically true for the physical boundary actually present, but it SHALL NOT be used as an ARQ authority claim until the new boundary is explicitly declared and attested.

---

## 8. Theorem 1 — Trusted-Boundary Entropy Bound

### 8.1 Statement

**Theorem 1 (Trusted-boundary entropy bound).**

Assume Model M5.

Let

\[
d_{SA}=\dim(\mathcal H_{SA})<\infty,
\]

and let `\rho_{SA}(t)` be the reduced state on the trusted quantum boundary.

Then, for all `t` during a valid epoch,

\[
0 \le S(\rho_{SA}(t)) \le \log_2 d_{SA}.
\]

Likewise, for the reduced system state `\rho_S(t)`,

\[
0 \le S(\rho_S(t)) \le \log_2 d_S.
\]

### 8.2 Proof

The operator `\rho_{SA}(t)` is a density operator on a finite-dimensional Hilbert space of dimension `d_{SA}`. Let its eigenvalues be `\lambda_1,\dots,\lambda_r`, where `r \le d_{SA}` and

\[
\lambda_i \ge 0,
\qquad
\sum_i \lambda_i = 1.
\]

By definition,

\[
S(\rho_{SA}) = -\sum_i \lambda_i \log_2 \lambda_i.
\]

This is the Shannon entropy of a probability distribution supported on at most `d_{SA}` outcomes. Such entropy is maximized by the uniform distribution, giving

\[
S(\rho_{SA}) \le \log_2 d_{SA}.
\]

The lower bound `S(\rho_{SA}) \ge 0` is standard for von Neumann entropy.

The same argument applies to `\rho_S(t)`, which acts on `\mathcal H_S` of finite dimension `d_S`, hence

\[
0 \le S(\rho_S(t)) \le \log_2 d_S.
\]

Therefore both entropies are bounded by finite boundary dimension. ∎

### 8.3 Interpretation

The theorem says exactly this:

> if ARQ speaks only about the reduced state inside a fixed finite trusted quantum boundary, the amount of internal von Neumann entropy it can attribute there is finite.

It does **not** yet say whether that entropy is useful, harmful, or even measurable at reasonable cost.

---

## 9. Theorem 2 — Usable-Entanglement Dimension Bound

### 9.1 Definition carried by the theorem

For this document, usable entanglement is defined as

\[
E_{use}(\rho_{SA}(t)) = \max_{A'\in\mathfrak A} E\big(\rho_{S:A'}(t)\big),
\]

where:

- `\mathfrak A` is the declared family of admissible trusted ancilla subsets;
- `E` is the entanglement monotone chosen by the active ARQ quantum profile;
- only correlations **inside** the trusted boundary are admissible.

### 9.2 Statement

**Theorem 2 (Usable-entanglement dimension bound).**

Assume Model M5 and a fixed valid epoch.

Let `\mathfrak A` be finite and admissible.

Then `E_{use}(\rho_{SA}(t))` is bounded by a constant depending only on trusted-boundary dimensions and the chosen monotone profile.

In particular:

1. if the profile uses **logarithmic negativity**
   \[
   E_N(\rho)=\log_2 \|\rho^{T_B}\|_1,
   \]
   then
   \[
   E_{use}(\rho_{SA}(t)) \le \min(\log_2 d_S,\log_2 d_A);
   \]

2. if the profile uses **negativity**
   \[
   N(\rho)=\frac{\|\rho^{T_B}\|_1-1}{2},
   \]
   then
   \[
   E_{use}(\rho_{SA}(t)) \le \frac{\min(d_S,d_A)-1}{2}.
   \]

Hence usable entanglement inside the trusted boundary cannot grow without bound as long as the boundary remains fixed and finite-dimensional.

### 9.3 Proof

Take any admissible `A'\in\mathfrak A` and write

\[
r = \min(d_S,d_{A'}).
\]

Because `d_{A'} \le d_A`, we have `r \le \min(d_S,d_A)`.

#### 9.3.1 Logarithmic negativity case

For a pure bipartite state with Schmidt coefficients `\{\mu_i\}_{i=1}^r`, one has

\[
\|\rho^{T_B}\|_1 = \left(\sum_{i=1}^{r} \sqrt{\mu_i}\right)^2.
\]

By Cauchy–Schwarz,

\[
\left(\sum_{i=1}^{r} \sqrt{\mu_i}\right)^2
\le
r\left(\sum_{i=1}^{r} \mu_i\right)
=
r.
\]

Therefore, for pure states,

\[
E_N(\rho) = \log_2 \|\rho^{T_B}\|_1 \le \log_2 r.
\]

For mixed states, the trace norm is convex, so the same upper bound remains valid:

\[
E_N(\rho_{S:A'}) \le \log_2 r \le \min(\log_2 d_S,\log_2 d_A).
\]

Taking the maximum over all admissible `A'` preserves the bound, hence

\[
E_{use}(\rho_{SA}(t)) \le \min(\log_2 d_S,\log_2 d_A).
\]

#### 9.3.2 Negativity case

Using

\[
N(\rho)=\frac{\|\rho^{T_B}\|_1-1}{2},
\]

and the same bound `\|\rho^{T_B}\|_1 \le r`, we obtain

\[
N(\rho_{S:A'}) \le \frac{r-1}{2} \le \frac{\min(d_S,d_A)-1}{2}.
\]

Again, maximizing over admissible `A'` preserves finiteness and gives

\[
E_{use}(\rho_{SA}(t)) \le \frac{\min(d_S,d_A)-1}{2}.
\]

Thus usable entanglement is bounded solely by trusted-boundary dimensions and the chosen monotone profile. ∎

### 9.4 Interpretation

This theorem says exactly one thing:

> inside a finite trusted quantum boundary, usable entanglement is a bounded resource.

It does **not** imply that the bound is reachable on real hardware, that tomography is cheap, or that every nonzero `E_use` is worth promotion.

---

## 10. Corollary 1 — Qubit Architecture Bound

### 10.1 Statement

Assume the trusted system register contains `n` qubits and the trusted ancilla boundary contains `m` qubits.

Then

\[
d_S = 2^n,
\qquad
d_A = 2^m,
\qquad
d_{SA}=2^{n+m}.
\]

Therefore, during a valid epoch,

\[
S(\rho_{SA}(t)) \le n+m,
\]

\[
S(\rho_S(t)) \le n,
\]

and, if logarithmic negativity is used,

\[
E_{use}(\rho_{SA}(t)) \le \min(n,m)
\quad \text{ebits}.
\]

### 10.2 Interpretation

For finite qubit architectures, internal trusted-boundary entropy and usable entanglement cannot diverge with runtime unless the trusted boundary itself is redefined or enlarged.

---

## 11. Corollary 2 — Epoch-Qualified ARQ Authority

### 11.1 Statement

Assume Models M3 and M5.

If any of the following occur:

- trusted ancilla map changes;
- boundary declaration changes;
- controller calibration invalidates the active epoch;
- attestation, witness, or boundary-validity requirements fail;

then quantum ARQ valuation MAY continue only after one of the following:

1. a new valid epoch explicitly re-declares the trusted boundary; or
2. the system degrades to a non-promoting safe mode that does not claim new boundary-qualified value.

### 11.2 Interpretation

The dimensional bound is mathematical. Promotion authority is operational.

A system SHALL NOT say:

> “some finite boundary existed once, therefore this current event is still promotion-eligible.”

Boundary-qualified authority expires with the epoch assumptions that made the boundary trustworthy.

---

## 12. Operational Meaning for ARQ

This theorem set has four practical consequences.

### 12.1 Quantum ARQ is not allowed to value “entanglement somewhere”

Only correlation inside the declared trusted boundary counts toward `E_use`.

Anything entangled only with the uncontrolled environment is outside the admissible value domain.

### 12.2 Boundary size is a hard ceiling on quantum ARQ claims

A profile with `n` system qubits and `m` trusted ancilla qubits has a fixed maximum claim ceiling for internal entropy and usable entanglement.

It MAY claim less. It SHALL NOT claim more.

### 12.3 Energy and cooling remain operational gates

Even though the theorem is dimension-based rather than energy-based, ARQ still needs power, calibration, timing, and thermal headroom to:

- prepare states,
- maintain coherence,
- perform syndrome or witness operations,
- estimate `E_use`,
- and complete review windows.

The theorem bounds the **resource size**. It does not waive the **resource cost**.

### 12.4 Fail-closed remains mandatory

If the trusted quantum boundary is no longer demonstrably valid, the system SHALL reduce authority or fail closed rather than continue quantum promotion on narrative confidence.

---

## 13. Non-Theorem Limitation Table

| Tempting overclaim | Why it is invalid |
|---|---|
| “Finite energy alone gives the quantum bound here.” | Not in this theorem. The bound comes from finite boundary dimension. |
| “Because entropy is bounded, valuable correlation is easy to preserve.” | Preservation cost is separate from dimensional boundedness. |
| “Any observed entanglement contributes to `E_use`.” | False. Only admissible inside-boundary correlation counts. |
| “This theorem proves long-lived coherence on real hardware.” | False. It proves ceilings, not sustained performance. |
| “A previously valid boundary keeps authorizing later events after drift.” | False under ARQ trust discipline. Epoch validity still governs authority. |
| “Tomography or shadow estimates automatically inherit theorem certainty.” | No. Estimation error and calibration validity remain separate audit questions. |

---

## 14. Audit Requirements for Quantum-Boundary Claims

Any implementation claiming this theorem profile SHOULD be able to disclose, at minimum:

1. the declared `\mathcal H_S`, `\mathcal H_A`, and boundary identifier;
2. the active epoch identifier `e_k`;
3. the trusted ancilla map for that epoch;
4. the entanglement monotone profile used for `E_use`;
5. the state-estimation method class used, such as tomography, shadow estimation, witness operators, or bounded proxy;
6. the witness record linking the event to that epoch and boundary;
7. any invalidation event that interrupted the boundary assumptions.

A verifier MUST be able to distinguish:

- “dimensionally bounded in principle,”
- from “operationally admissible for ARQ promotion in this epoch.”

---

## 15. A/B Slots and Safe Self-Edit with Auto-Rollback

### 15.1 Purpose

Quantum-boundary reasoning is especially vulnerable to prestige drift: the symbol can remain finite while the declared trusted set quietly expands.

ARQ therefore SHALL support a safe self-edit discipline for quantum-boundary profiles.

### 15.2 Slot semantics

A conformant implementation SHOULD distinguish:

- **Slot A** — last-known-good trusted-boundary declaration currently allowed to support real ARQ valuation;
- **Slot B** — candidate boundary refinement, candidate ancilla-map change, or candidate entanglement-profile update.

### 15.3 Hard rule

Slot B MUST NOT authorize promotion, threshold widening, or stronger quantum-value claims while it remains shadow-only.

### 15.4 Auto-rollback rule

If Slot B produces any of the following relative to Slot A beyond declared tolerance:

- unexplained increase in declared trusted ancilla scope;
- quantum-value inflation without corresponding witness/attestation support;
- boundary/profile mismatch with replayed records;
- contradiction with known-good qubit-count ceilings;
- silent reclassification of environment-correlation as `E_use`;

then the system MUST automatically roll back to Slot A and emit a witnessed rollback record.

### 15.5 Promotion of Slot B

A candidate quantum-boundary refinement MAY replace Slot A only if:

1. the review window completes;
2. required authority approves it;
3. the replacement is witnessed;
4. rollback path remains available.

---

## 16. Minimum Normative Statements

1. A quantum ARQ implementation SHALL declare its trusted quantum boundary explicitly.
2. Internal trusted-boundary entropy SHALL be treated as bounded by `\log_2 d_{SA}`.
3. Local system entropy SHALL be treated as bounded by `\log_2 d_S`.
4. `E_use` SHALL count only admissible correlations inside the trusted boundary.
5. The chosen entanglement monotone profile SHALL be declared.
6. Boundary expansion or trusted-ancilla-map change SHALL require epoch renewal or explicit recalibration.
7. The theorem in this document SHALL NOT be cited as an energy-budget theorem.
8. A valid dimensional bound SHALL NOT by itself authorize promotion; trust and witness conditions still apply.
9. If the trusted boundary cannot be verified for the active epoch, quantum promotion authority SHALL degrade or fail closed.
10. Shadow boundary refinements SHALL NOT widen real promotion authority while in Slot B.

---

## 17. Explicit and Hidden Bridges

### 17.1 Explicit bridge

ARQ’s quantum branch becomes disciplined only when three things meet at once:

- `c = a + b` supplies accountable authority and procedures,
- the trusted quantum boundary supplies a finite admissible state space,
- and witness / trust logic binds promoted value claims to an epoch-qualified, challengeable trail.

### 17.2 Hidden bridge #1 — SER / survival under boundary loss

SER distinguishes survival from ambition. This theorem fits that physiology: when the trusted boundary is no longer valid, the entity is not invited to improvise larger meaning from smaller evidence. It must narrow authority or stop.

### 17.3 Hidden bridge #2 — L4 Witness / proof bandwidth

L4 Witness compresses accountability into signed, replayable records. This theorem does something similar for quantum claims: it compresses the maximum claim size into finite boundary dimensions rather than narrative enthusiasm. The question is not “how impressive did the event look,” but “what was the largest admissible controlled space in that epoch?”

### 17.4 Hidden bridge #3 — Beacon / bounded identity continuity

Beacon requires challengeable continuity rather than theatrical sameness. Quantum ARQ inherits the same discipline: the boundary that generated a value claim must remain identifiable, finite, and epoch-bound, or the claim no longer carries the same authority.

---

## 18. Earth Paragraph

In plain engineering terms, this is a room-size theorem. If your quantum rack has 12 system qubits and 4 trusted ancillas in the valid box, then the box is the box. You do not get to count the hallway, the warm cables, the drifting readout chain, and the ambient crosstalk as “extra intelligence” just because they participated in the mess. The theorem says: measure what is inside the declared cabinet, not what the whole room happened to shake.

---

## 19. Closing Statement

Quantum ARQ does not need infinite mystery. It needs a declared box.

Once that box is finite, two rude but useful facts follow:

- the entropy inside it is bounded,
- and the usable entanglement inside it is bounded.

That does not solve calibration, drift, or exploitation cost.
But it does remove one dangerous illusion:

> no quantum ARQ entity gets to claim unbounded value from a finite trusted boundary.

That is enough to turn the quantum branch from metaphor into protocol discipline.
