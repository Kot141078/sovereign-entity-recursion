# ARQ_Quantum_Boundary_Theorem_prouve_v0.2
## Proof Companion for the Quantum Boundary Theorem in the ARQ v0.2 Supplement

**Status:** Draft / proof companion  
**Version:** 0.2-draft  
**Role:** detailed proofs, monotone-bound discipline, epoch-qualified authority derivation  
**Parent documents:** `ARQ_v0.2_Normative_Core.md`, `ARQ_System_Models_and_Assumptions_v0.2.md`, `ARQ_Notation_and_Sign_Conventions_v0.2.md`, `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.md`, `ARQ_Trust_and_Provenance_Profile_v0.2.md`, `ARQ_Quantum_Boundary_Theorem_v0.2.md`  
**Parent corpus:** AGI / SER / L4 / L4 Witness / Beacon / VXCX  
**Author:** Ivan Kotov  
**Place / year:** Bruxelles, 2026

---

## 0. Abstract

This document is the proof companion to `ARQ_Quantum_Boundary_Theorem_v0.2.md`.

Its task is narrower than the theorem document itself. It does not invent new claims. It makes the already declared quantum boundedness claims checkable line by line.

The companion expands the proof surface behind four results:

1. trusted-boundary entropy boundedness under Model M5;
2. usable-entanglement boundedness inside the trusted boundary under Model M5;
3. the explicit qubit-form corollary;
4. the epoch-qualified authority corollary under M3 + M5.

The important discipline is this:

> quantum ARQ boundedness is not proven by prestige, not by the word “quantum,” and not by a vague appeal to thermodynamics.  
> It is proven by a declared finite boundary, a declared monotone, and an epoch-qualified trust carrier.

This document also states what the proof set does **not** establish, so that later texts cannot silently inflate a finite-boundary theorem into a universal law of long-lived quantum intelligence.

---

## 1. Purpose

This document answers one question:

> What are the detailed proof steps behind the quantum boundedness claims already stated for ARQ v0.2?

It SHALL:

1. restate the exact model carriers needed for each proof;
2. provide explicit lemmas used by the theorem set;
3. give line-by-line proofs using only declared assumptions;
4. preserve anti-overclaim discipline;
5. provide a clean citation target for later audit, review, and correction.

This document SHALL NOT silently strengthen the assumptions made in the parent theorem document.

---

## 2. Scope

This proof companion is quantum-boundary specific.

It covers:

- Model M5 — fixed trusted quantum boundary;
- Model M3 only as the epoch-validity gate for operational ARQ authority.

It does **not** prove:

- any whole-device thermodynamic lifetime theorem;
- any arbitrary open-system entropy law;
- any claim that finite dimensionality alone makes entanglement cheap to estimate or useful to exploit;
- any bound for undeclared ancillas or undeclared control surfaces;
- any authority claim outside valid trust epochs.

---

## 3. Imported Dependencies and Symbols

This document imports notation from the ARQ v0.2 companion set.

The following symbols SHALL retain their canonical meanings:

- `\mathcal H_S` — system Hilbert space;
- `\mathcal H_A` — trusted ancilla Hilbert space;
- `\mathcal H_U` — uncontrolled environment Hilbert space;
- `\mathcal H_{SA} = \mathcal H_S \otimes \mathcal H_A` — trusted quantum boundary;
- `d_S = \dim(\mathcal H_S)`;
- `d_A = \dim(\mathcal H_A)`;
- `d_{SA} = \dim(\mathcal H_{SA})`;
- `\rho(t)` — full density operator;
- `\rho_{SA}(t) = \operatorname{Tr}_U \rho(t)` — reduced state on the trusted boundary;
- `\rho_S(t) = \operatorname{Tr}_{AU} \rho(t)` — reduced state on the system register;
- `S(\rho)` — von Neumann entropy in bits;
- `E_{use}(\rho_{SA})` — usable entanglement inside the trusted boundary;
- `\mathfrak A` — declared admissible trusted ancilla family;
- `A_{anom}` — anomaly score;
- `T_{core}` — canonical validity core;
- `G_{promote}` — promotion gate;
- `e_k` — active trust / calibration epoch.

The trust-profile formulas imported here are:

\[
T_{core} = B_{valid}\cdot A_{valid}\cdot C_{valid}\cdot W_{valid},
\]

\[
G_{promote} = T_{core}\cdot P_{valid}\cdot R_{valid}\cdot (1 - X_{echo}).
\]

All theorem references in this file are references to the parent document `ARQ_Quantum_Boundary_Theorem_v0.2.md`.

---

## 4. Proof Policy

### 4.1 Declared-model rule

A proof in this document is valid only relative to its declared model carrier.

### 4.2 No hidden boundary rule

A proof SHALL NOT rely on undeclared ancillas, undeclared qubit maps, undeclared trusted controller paths, or undeclared environment partitions.

### 4.3 No monotone drift rule

If the theorem is stated for a declared entanglement monotone, the proof SHALL NOT silently swap in a different one.

### 4.4 No thermodynamic prestige rule

A proof SHALL NOT use Landauer-style rhetoric to claim more than finite-dimensional boundary structure actually proves.

### 4.5 No environment laundering rule

A proof SHALL NOT treat correlation with the uncontrolled environment as usable entanglement merely because it is mathematically nonzero.

---

## 5. Preliminary Lemmas

### 5.1 Lemma Q1 — Maximum entropy on a finite-dimensional Hilbert space

Let `\sigma` be a density operator acting on a Hilbert space of dimension `d < \infty`.
Then:

\[
0 \le S(\sigma) \le \log_2 d.
\]

#### Proof

Let `\lambda_1,\dots,\lambda_r` be the nonzero eigenvalues of `\sigma`, with `r \le d`, `\lambda_i \ge 0`, and `\sum_i \lambda_i = 1`.
Then

\[
S(\sigma) = -\sum_{i=1}^{r} \lambda_i \log_2 \lambda_i.
\]

This is the Shannon entropy of a probability distribution supported on at most `d` outcomes. Such entropy is maximized by the uniform distribution on `d` outcomes, which yields `\log_2 d`. The lower bound is standard since von Neumann entropy is nonnegative. ∎

---

### 5.2 Lemma Q2 — Pure-state negativity ceiling from Schmidt rank

Let `|\psi\rangle` be a bipartite pure state on `\mathcal H_X \otimes \mathcal H_Y`, and let its Schmidt rank be `r \le \min(d_X,d_Y)`.
Then the negativity satisfies

\[
N(|\psi\rangle\langle\psi|) \le \frac{r-1}{2}.
\]

Moreover, the logarithmic negativity satisfies

\[
E_N(|\psi\rangle\langle\psi|) \le \log_2 r.
\]

#### Proof

Write the Schmidt decomposition

\[
|\psi\rangle = \sum_{i=1}^{r} \sqrt{\mu_i}\, |i_X\rangle \otimes |i_Y\rangle,
\qquad
\mu_i \ge 0,
\qquad
\sum_{i=1}^{r} \mu_i = 1.
\]

For a pure bipartite state,

\[
\|(|\psi\rangle\langle\psi|)^{T_Y}\|_1 = \left(\sum_{i=1}^{r} \sqrt{\mu_i}\right)^2.
\]

Hence

\[
N(|\psi\rangle\langle\psi|)
=
\frac{\|(|\psi\rangle\langle\psi|)^{T_Y}\|_1 - 1}{2}
=
\frac{\left(\sum_i \sqrt{\mu_i}\right)^2 - 1}{2}.
\]

By Cauchy–Schwarz,

\[
\left(\sum_{i=1}^{r} \sqrt{\mu_i}\right)^2
\le
\left(\sum_{i=1}^{r} 1^2\right)\left(\sum_{i=1}^{r} \mu_i\right)
=
r.
\]

Therefore

\[
N(|\psi\rangle\langle\psi|) \le \frac{r-1}{2}.
\]

Using `E_N(\rho)=\log_2(2N(\rho)+1)`, we obtain

\[
E_N(|\psi\rangle\langle\psi|)
\le
\log_2\big(2\cdot \tfrac{r-1}{2}+1\big)
=
\log_2 r.
\]

∎

---

### 5.3 Lemma Q3 — Convexity transfer for negativity

Let

\[
\rho = \sum_k p_k \rho_k,
\qquad
p_k \ge 0,
\qquad
\sum_k p_k = 1.
\]

Then negativity is convex:

\[
N(\rho) \le \sum_k p_k N(\rho_k).
\]

#### Proof

By linearity of partial transpose,

\[
\rho^{T_B} = \sum_k p_k \rho_k^{T_B}.
\]

By convexity of the trace norm,

\[
\|\rho^{T_B}\|_1 \le \sum_k p_k \|\rho_k^{T_B}\|_1.
\]

Using `N(\rho)=\frac{\|\rho^{T_B}\|_1-1}{2}` and `\sum_k p_k = 1`,

\[
N(\rho)
=
\frac{\|\rho^{T_B}\|_1-1}{2}
\le
\frac{\sum_k p_k \|\rho_k^{T_B}\|_1 - 1}{2}
=
\sum_k p_k \frac{\|\rho_k^{T_B}\|_1 - 1}{2}
=
\sum_k p_k N(\rho_k).
\]

∎

---

### 5.4 Lemma Q4 — Mixed-state negativity ceiling on finite bipartite dimensions

Let `\rho` be any bipartite state on `d_X \times d_Y`, and define `r = \min(d_X,d_Y)`.
Then

\[
N(\rho) \le \frac{r-1}{2},
\qquad
E_N(\rho) \le \log_2 r.
\]

#### Proof

Any mixed state admits a convex decomposition into pure states:

\[
\rho = \sum_k p_k |\psi_k\rangle\langle\psi_k|.
\]

Each `|\psi_k\rangle` has Schmidt rank at most `r`, so by Lemma Q2,

\[
N(|\psi_k\rangle\langle\psi_k|) \le \frac{r-1}{2}.
\]

Applying Lemma Q3,

\[
N(\rho)
\le
\sum_k p_k N(|\psi_k\rangle\langle\psi_k|)
\le
\sum_k p_k \frac{r-1}{2}
=
\frac{r-1}{2}.
\]

Then

\[
E_N(\rho)=\log_2(2N(\rho)+1)
\le
\log_2\big(2\cdot\tfrac{r-1}{2}+1\big)
=
\log_2 r.
\]

∎

---

### 5.5 Lemma Q5 — Maximum over admissible ancilla subsets preserves the ceiling

Let `\mathfrak A` be a finite family of admissible trusted ancilla subsets. Suppose a quantity `f(A')` satisfies

\[
f(A') \le B
\qquad
\text{for every } A'\in\mathfrak A.
\]

Then

\[
\max_{A'\in\mathfrak A} f(A') \le B.
\]

#### Proof

Immediate from the definition of a maximum over a finite set. ∎

---

## 6. Detailed Proof of Theorem 1
## Trusted-Boundary Entropy Bound

### 6.1 Statement

Assume Model M5.

Let `\rho_{SA}(t)` be the reduced state on the trusted quantum boundary `\mathcal H_{SA}` with dimension `d_{SA} < \infty`.
Then, during a valid epoch,

\[
0 \le S(\rho_{SA}(t)) \le \log_2 d_{SA}.
\]

Likewise,

\[
0 \le S(\rho_S(t)) \le \log_2 d_S.
\]

### 6.2 Proof

The state `\rho_{SA}(t)` is a density operator on the finite-dimensional Hilbert space `\mathcal H_{SA}`. By Lemma Q1,

\[
0 \le S(\rho_{SA}(t)) \le \log_2 d_{SA}.
\]

The reduced system state `\rho_S(t)` acts on the finite-dimensional Hilbert space `\mathcal H_S` of dimension `d_S`, so again by Lemma Q1,

\[
0 \le S(\rho_S(t)) \le \log_2 d_S.
\]

Hence both entropy quantities are bounded by finite trusted-boundary dimension. ∎

### 6.3 Why this proof is clean

The proof uses only:

- finite-dimensionality of the declared trusted quantum boundary;
- standard spectral entropy facts for density operators.

It does **not** need:

- an energy budget argument;
- a cooling argument;
- a tomography-cost argument;
- any claim that the bound is operationally saturated.

### 6.4 What this proof actually buys ARQ

It gives ARQ a hard ceiling on how much internal boundary entropy it may even talk about inside the declared trusted quantum box.

It does **not** yet say whether that entropy corresponds to useful structure, expensive garbage, or an unverifiable mirage.

---

## 7. Detailed Proof of Theorem 2
## Usable-Entanglement Dimension Bound

### 7.1 Statement

Assume Model M5 and let `\mathfrak A` be the declared admissible ancilla family.

Define

\[
E_{use}(\rho_{SA}(t)) = \max_{A'\in\mathfrak A} E\big(\rho_{S:A'}(t)\big),
\]

where `E` is the entanglement monotone selected by the active profile.

Then:

1. if the profile uses logarithmic negativity,
   \[
   E_{use}(\rho_{SA}(t)) \le \min(\log_2 d_S,\log_2 d_A);
   \]

2. if the profile uses negativity,
   \[
   E_{use}(\rho_{SA}(t)) \le \frac{\min(d_S,d_A)-1}{2}.
   \]

### 7.2 Proof — step 1: bound for a fixed admissible subset

Take any fixed admissible `A'\in\mathfrak A`.
Let

\[
r = \min(d_S,d_{A'}).
\]

Since `d_{A'} \le d_A`, we have

\[
r \le \min(d_S,d_A).
\]

By Lemma Q4,

\[
N(\rho_{S:A'}(t)) \le \frac{r-1}{2}
\le
\frac{\min(d_S,d_A)-1}{2},
\]

and

\[
E_N(\rho_{S:A'}(t)) \le \log_2 r
\le
\min(\log_2 d_S,\log_2 d_A).
\]

Thus every fixed admissible ancilla subset obeys the same ceiling.

### 7.3 Proof — step 2: maximize over admissible subsets

The usable-entanglement definition takes a maximum over admissible subsets `A'\in\mathfrak A`.

For each admissible subset, the relevant bound from step 1 holds.
Therefore, by Lemma Q5, the maximum over the admissible family preserves the same ceiling.

Hence, if the profile uses negativity,

\[
E_{use}(\rho_{SA}(t)) \le \frac{\min(d_S,d_A)-1}{2},
\]

and if the profile uses logarithmic negativity,

\[
E_{use}(\rho_{SA}(t)) \le \min(\log_2 d_S,\log_2 d_A).
\]

This proves Theorem 2. ∎

### 7.4 Why this proof is honest

The proof does **not** say:

- that every admissible subset is equally useful;
- that the maximum is easy to estimate;
- that the best subset remains stable under drift;
- that the bounded quantity is necessarily promotion-worthy.

It says only this:

> once the trusted boundary and monotone profile are declared, usable entanglement is a bounded inside-the-box resource.

### 7.5 Why the logarithmic-negativity form is cleaner for ARQ

For qubit architectures and for human-readable policy discussion, the logarithmic-negativity bound is usually cleaner because it scales directly in bits / ebits:

\[
E_{use} \le \min(\log_2 d_S, \log_2 d_A).
\]

That is usually the profile worth preferring when ARQ wants readable promotion ceilings rather than larger algebraic-looking constants.

---

## 8. Detailed Proof of Corollary 1
## Qubit Architecture Bound

### 8.1 Statement

Assume the trusted system register contains `n` qubits and the trusted ancilla boundary contains `m` qubits.
Then

\[
d_S = 2^n,
\qquad
d_A = 2^m,
\qquad
d_{SA}=2^{n+m}.
\]

Therefore,

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

### 8.2 Proof

Substitute the qubit dimensions into Theorem 1:

\[
S(\rho_{SA}(t)) \le \log_2 d_{SA} = \log_2(2^{n+m}) = n+m,
\]

\[
S(\rho_S(t)) \le \log_2 d_S = \log_2(2^n)=n.
\]

If the profile uses logarithmic negativity, Theorem 2 gives

\[
E_{use}(\rho_{SA}(t)) \le \min(\log_2 d_S, \log_2 d_A)
=
\min(n,m).
\]

This proves the corollary. ∎

### 8.3 Engineering reading

If the declared box is `n + m` qubits wide, then ARQ is not allowed to narrate value as if the box were larger than it is.

This is not anti-quantum skepticism.
It is dimensional hygiene.

---

## 9. Detailed Proof of Corollary 2
## Epoch-Qualified ARQ Authority

### 9.1 Statement

Assume Models M3 and M5.

If any of the following occur:

- trusted ancilla map changes;
- boundary declaration changes;
- controller calibration invalidates the active epoch;
- boundary-validity, attestation-validity, controller-integrity, or witness-integrity requirements fail;

then quantum ARQ valuation MAY continue only after one of the following:

1. a new valid epoch explicitly re-declares the trusted boundary; or
2. the system degrades to a non-promoting safe mode that does not claim new boundary-qualified value.

### 9.2 Proof

From the trust-profile document, the canonical validity core is

\[
T_{core} = B_{valid}\cdot A_{valid}\cdot C_{valid}\cdot W_{valid}.
\]

The canonical promotion gate is

\[
G_{promote} = T_{core}\cdot P_{valid}\cdot R_{valid}\cdot (1 - X_{echo}).
\]

Now consider each failure mode.

#### Boundary declaration change or trusted ancilla-map change

If the declared trusted boundary changes, then the event is no longer guaranteed to belong to the same declared boundary configuration. By the trust profile, this breaks boundary validity for the old declaration, so `B_valid = 0` until a new valid declaration is attested.
Hence

\[
T_{core} = 0,
\qquad
G_{promote}=0.
\]

#### Controller calibration invalidation or epoch invalidation

If the active epoch becomes invalid, then attestation validity fails, so `A_valid = 0`.
Therefore

\[
T_{core}=0,
\qquad
G_{promote}=0.
\]

#### Controller-integrity or witness-integrity failure

If the claimed controller path cannot be replayed, then `C_valid = 0`.
If the witness chain is broken or insufficient, then `W_valid = 0`.
Either way,

\[
T_{core}=0,
\qquad
G_{promote}=0.
\]

Thus in every listed case, promotion authority is withdrawn.

What remains possible depends on policy, but by the trust-profile hard rule, a system without valid promotion authority may at most:

- log;
- observe inside a bounded non-promoting path;
- degrade;
- or fail closed.

To restore promotion authority, the system needs a new valid epoch with an explicit re-declaration of the trusted boundary or a safe degraded mode that makes no new boundary-qualified promotion claim.

This proves Corollary 2. ∎

### 9.3 Why this corollary is operational, not purely mathematical

The finite-dimensional theorem remains mathematically true for whatever physical boundary actually exists.

But ARQ does not care only about truth in the abstract.
It cares about **which finite boundary is admissible to cite as a value-authorizing boundary in the current epoch**.

That is why this corollary belongs to M3 + M5 rather than M5 alone.

---

## 10. Non-Theorem Limitation Table

| Tempting overclaim | Why it does not follow from this proof companion |
|---|---|
| “Because the trusted boundary is finite, real hardware can preserve coherence indefinitely.” | False. The proof gives dimensional ceilings, not a longevity guarantee. |
| “Any entanglement detected in the lab counts toward `E_use`.” | False. Only admissible inside-boundary entanglement counts. |
| “The theorem is really an energy theorem in disguise.” | No. This proof uses boundary dimension, not lifetime dissipation accounting. |
| “If `E_use` is bounded and nonzero, promotion is justified.” | False. Promotion also requires valuation, witnessability, review path, and trust validity. |
| “A once-valid trusted boundary keeps authorizing later claims after drift.” | False. Corollary 2 explicitly blocks that. |
| “The max over ancilla subsets lets us smuggle in undeclared ancillas.” | False. The maximization is only over the declared admissible family `\mathfrak A`. |
| “Finite qubit count means tomography burden is bounded and therefore negligible.” | Not implied. Estimation cost is separate from the existence of an upper bound. |

---

## 11. Reviewer Checklist

A reviewer checking a quantum-boundary boundedness claim in ARQ SHOULD ask:

1. Which theorem is being invoked: entropy bound, usable-entanglement bound, qubit corollary, or epoch-qualified authority corollary?
2. Which model carrier is declared?
3. Is the trusted boundary explicitly declared?
4. Is the admissible ancilla family explicitly declared?
5. Which entanglement monotone profile is being used?
6. Is the claim being made inside a valid epoch?
7. Is anyone smuggling uncontrolled environment correlation into `E_use`?
8. Is anyone pretending a dimensional ceiling implies cheap verification or operational usefulness?

If any of these answers is missing, the proof citation is too loose.

---

## 12. Proof Revision Discipline

### 12.1 Anti-echo rule

A revision SHALL NOT be accepted merely because it repeats “finite boundary, therefore bounded” in grander language.

### 12.2 A/B-slot proof editing

Proof revisions SHOULD use:

- **Slot A** — current canonical proof text;
- **Slot B** — proposed revised proof text.

A Slot B revision may replace Slot A only if all of the following hold:

1. it preserves the valid earlier claim;
2. it makes the model carrier clearer;
3. it does not upgrade a dimensional bound into a thermodynamic claim;
4. it does not broaden `E_use` to undeclared correlations;
5. it remains checkable against the theorem, trust, and notation docs.

### 12.3 Auto-rollback rule

If a proof revision makes the quantum result sound more profound by making it less honest, it MUST be rolled back automatically.

The most common failure pattern here is simple: a finite box theorem gets rewritten as if it had proven destiny.

---

## 13. Bridges (required)

### Explicit bridge

The parent theorem document states the quantum boundedness claims; this proof companion makes them reviewable. Together they bind ARQ's quantum branch to declared boundary dimension, declared monotone profile, and epoch-qualified authority.

### Hidden bridge 1 — SER / survival physiology

SER distinguishes persistence from fantasy. A long-lived entity survives by narrowing claims when evidence narrows. This proof companion is exactly that move for the quantum branch: when the trusted box is finite, the claim must remain finite too.

### Hidden bridge 2 — L4 Witness / proof bandwidth

Witness compresses accountability into signed replayable traces. This proof companion compresses quantum exuberance into finite-dimensional ceilings. It asks not “how exciting was the event?” but “what was the largest declared and attested box inside which this claim is even allowed to live?”

---

## 14. Earth Paragraph (engineering / anatomy)

A heart monitor trace is useful because the chest cavity is finite and the leads are attached where you say they are. If half the wires fall off and someone starts counting room noise as “extra heartbeat,” the mathematics of bounded signals has not failed — the setup has. Quantum ARQ is similar. The finite-boundary theorem is the lead placement. The trust epoch is the fact that the electrodes are still attached. Without both, what remains may still be a signal in physics, but it is no longer a signal you are entitled to call the patient’s pulse.

---

## 15. Closing Statement

This proof companion establishes a narrow but durable claim:

> In quantum ARQ, boundedness is real when the boundary is declared honestly and the epoch is still valid.

Finite trusted-boundary dimension is enough to prove ceilings for internal boundary entropy and usable entanglement. M3 then decides when those ceilings are still allowed to support real ARQ authority.

What the proof does **not** do is bless every interesting lab correlation as admissible value.
