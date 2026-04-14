# ARQ_Classical_Boundedness_Theorem_pruve_v0.2
## Proof Companion for the Classical Boundedness Theorem in the ARQ v0.2 Supplement

**Status:** Draft / proof companion  
**Version:** 0.2-draft  
**Role:** detailed proofs, claim discipline, overclaim prevention  
**Parent documents:** `ARQ_v0.2_Normative_Core.md`, `ARQ_System_Models_and_Assumptions_v0.2.md`, `ARQ_Notation_and_Sign_Conventions_v0.2.md`, `ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2.md`, `ARQ_Trust_and_Provenance_Profile_v0.2.md`, `ARQ_Classical_Boundedness_Theorem_v0.2.md`  
**Parent corpus:** AGI / SER / L4 / L4 Witness / Beacon / VXCX  
**Author:** Ivan Kotov  
**Place / year:** Bruxelles, 2026

---

## 0. Abstract

This document is the proof companion to `ARQ_Classical_Boundedness_Theorem_v0.2.md`.

Its purpose is narrow and explicit: not to invent new theorem claims, but to make the already declared classical boundedness claims reviewable line by line. The companion therefore expands the proof shape behind four results:

1. finite authoritative persistent-state boundedness under Model M1;
2. commit-metered retained-entropy boundedness under Model M2;
3. pending/backlog boundedness under Model M4;
4. the composite runtime-envelope corollary under M1 + M2 + M3 + M4.

The practical point is simple:

> ARQ boundedness is not one mystical statement.  
> It is a stitched proof surface across memory, commit authority, queue capacity, and epoch validity.

This document also states what the proofs do **not** establish, so that later texts cannot silently upgrade a support theorem into a global physical law.

---

## 1. Purpose

This document answers one question:

> What are the detailed proof steps behind the classical boundedness claims already stated for ARQ v0.2?

It SHALL:

1. restate the exact model carriers needed for each proof;
2. provide explicit lemmas used by the theorem set;
3. give line-by-line proofs using only declared assumptions;
4. preserve anti-overclaim discipline;
5. provide a clean citation target for later audit, review, and correction.

This document SHALL NOT silently strengthen the assumptions made in the parent theorem document.

---

## 2. Scope

This proof companion is classical only.

It covers:

- Model M1 — classical persistent-state boundedness;
- Model M2 — commit-metered retained-entropy boundedness;
- Model M4 — pending/backlog boundedness;
- Model M3 only as an epoch-validity gate for the composite corollary.

It does **not** prove:

- any quantum entropy theorem;
- any usable-entanglement theorem;
- any global thermodynamic law for arbitrary ARQ deployments;
- any whole-device heat theorem;
- any claim outside declared model boundaries.

---

## 3. Imported Dependencies and Symbols

This document imports notation from the ARQ v0.2 companion set.

The following symbols SHALL retain their canonical meanings:

- `X_t` — authoritative classical persistent state at time `t`;
- `M_persist` — number of bits available for authoritative persistent state;
- `C_mode` — finite controller-mode set;
- `R_T` — retained authoritative state at horizon `T`;
- `H(X)` — Shannon entropy in bits;
- `H_retained(T)` — retained authoritative entropy by horizon `T`;
- `H_pending(t)` — unresolved pending/backlog entropy at time `t`;
- `N_commit(T)` — number of successful authoritative commits by horizon `T`;
- `b_commit,min`, `b_commit,max` — minimum and maximum authoritative bits per commit under the declared profile;
- `e_commit,min` — minimum calibrated commit cost;
- `i_commit,min` — minimum irreversibility expenditure per commit, if such a budget is used;
- `K` — maximum pending queue capacity;
- `B_max` — maximum pending representation size per unresolved event;
- `E_commit(T)` — cumulative commit-eligible energy/resource budget by horizon `T`;
- `I_max(T)` — cumulative irreversibility budget by horizon `T`.

All theorem references in this file are references to the parent document `ARQ_Classical_Boundedness_Theorem_v0.2.md`.

---

## 4. Proof Policy

### 4.1 Declared-model rule

A proof in this document is valid only relative to its declared model carrier.

### 4.2 No hidden reservoir rule

A proof SHALL NOT rely on an undeclared extra memory region, undeclared queue, undeclared trust epoch, or undeclared authority channel.

### 4.3 No symbol drift rule

If `M_persist` denotes a number of bits, then no step in the proof may silently reinterpret it as the number of coarse-grained states.

### 4.4 No poetic thermodynamics rule

A proof SHALL NOT invoke Landauer's principle as a universal entropy oracle unless the physical commit/dissipation assumptions needed for that invocation are explicitly declared.

---

## 5. Preliminary Lemmas

### 5.1 Lemma A — Maximum entropy on a finite support

Let `Y` be a discrete random variable with finite support `Ω`.
Then:

\[
H(Y) \le \log_2 |\Omega|.
\]

#### Proof

For a finite support of size `|Ω|`, Shannon entropy is maximized by the uniform distribution on `Ω`. Under the uniform distribution,

\[
H(Y)= -\sum_{y\in \Omega}\frac{1}{|\Omega|}\log_2\frac{1}{|\Omega|}=\log_2|\Omega|.
\]

No other distribution on the same finite support yields a larger entropy. ∎

---

### 5.2 Lemma B — Entropy of a bit-addressable finite memory register

Let `B` be a classical register containing exactly `m` bits. Then its support has size at most `2^m`, and therefore

\[
H(B) \le m.
\]

#### Proof

A classical `m`-bit register has at most `2^m` distinct bit patterns. Apply Lemma A:

\[
H(B) \le \log_2(2^m)=m.
\]

∎

---

### 5.3 Lemma C — Chain-rule upper bound for cumulative retained commits

Let a retained authoritative state evolve through a sequence of successful authoritative commits indexed by `j = 1,2,\dots,N`, and let the retained delta associated with commit `j` be represented by a random variable `\Delta_j`. Assume

\[
H(\Delta_j \mid \Delta_1,\dots,\Delta_{j-1},R_0) \le b_{commit,max}
\]

for every successful commit.

Then

\[
H(R_N) - H(R_0) \le N\cdot b_{commit,max}.
\]

#### Proof

Write the retained authoritative state after `N` commits as a function of the initial retained state and the sequence of committed deltas:

\[
R_N = f(R_0,\Delta_1,\dots,\Delta_N).
\]

By data processing,

\[
H(R_N \mid R_0) \le H(\Delta_1,\dots,\Delta_N \mid R_0).
\]

By the chain rule,

\[
H(\Delta_1,\dots,\Delta_N \mid R_0)
=
\sum_{j=1}^{N} H(\Delta_j \mid R_0,\Delta_1,\dots,\Delta_{j-1}).
\]

Each term is at most `b_commit,max`, hence

\[
H(\Delta_1,\dots,\Delta_N \mid R_0) \le N\cdot b_{commit,max}.
\]

Therefore,

\[
H(R_N \mid R_0) \le N\cdot b_{commit,max}.
\]

Using

\[
H(R_N) \le H(R_0) + H(R_N \mid R_0),
\]

we obtain

\[
H(R_N)-H(R_0) \le N\cdot b_{commit,max}.
\]

∎

---

### 5.4 Lemma D — Finite queue representation bound

Let a pending queue hold at most `K` unresolved entries and let each unresolved entry consume at most `B_max` bits of queue-accounted pending representation. Then the total pending representation is bounded by `K·B_max` bits, and therefore

\[
H_{pending}(t) \le K\cdot B_{max}.
\]

#### Proof

At time `t`, there are at most `K` queue slots. If each slot carries at most `B_max` bits of pending representation, then the total queue-accounted representation occupies at most `K·B_max` bits. Apply Lemma B. ∎

---

## 6. Detailed Proof of Theorem 1
## Finite Authoritative Persistent-State Bound

### 6.1 Statement

Assume Model M1.

Let

\[
X_t \in \{0,1\}^{M_{persist}} \times C_{mode},
\]

where `M_persist < ∞` and `C_mode` is finite.
Then for all `t`:

\[
H(X_t) \le M_{persist} + \log_2 |C_{mode}|.
\]

### 6.2 Proof

The support of `X_t` is a subset of

\[
\{0,1\}^{M_{persist}} \times C_{mode}.
\]

The cardinality of that carrier set is at most

\[
2^{M_{persist}}\cdot |C_{mode}|.
\]

Applying Lemma A,

\[
H(X_t)
\le
\log_2\!\big(2^{M_{persist}}\cdot |C_{mode}|\big)
=
M_{persist}+\log_2|C_{mode}|.
\]

Hence `H(X_t)` is uniformly bounded for all `t`. ∎

### 6.3 Why this proof is clean

The proof uses only:

- finiteness of the authoritative bit register;
- finiteness of the controller-mode set;
- the entropy maximum on a finite support.

It does **not** need:

- any energy argument;
- any queue argument;
- any thermodynamic assumption;
- any trust-epoch argument.

### 6.4 Correction note on the old `log2 M` error

If `M_persist` means “number of memory bits,” then the entropy upper bound is order `M_persist`, not `log_2 M_persist`.

The expression `\log_2 M` is valid only when `M` denotes the number of memory states, not the number of addressable bits.

---

## 7. Detailed Proof of Theorem 2
## Commit-Metered Retained-Entropy Bound

### 7.1 Statement

Assume Model M2.

Assume also:

1. every retained authoritative update crosses a declared commit boundary;
2. every successful authoritative commit contributes at most `b_commit,max` bits of retained authoritative content;
3. each successful authoritative commit consumes at least one bounded resource, such as:
   - at least `b_commit,min > 0` bits of persistent-state headroom,
   - at least `e_commit,min > 0` calibrated commit cost,
   - at least `i_commit,min > 0` irreversibility expenditure, if such a budget is used.

Then:

\[
N_{commit}(T)
\le
\min
\left(
\left\lfloor \frac{M_{persist}}{b_{commit,min}} \right\rfloor,
\left\lfloor \frac{E_{commit}(T)}{e_{commit,min}} \right\rfloor,
\left\lfloor \frac{I_{max}(T)}{i_{commit,min}} \right\rfloor
\right),
\]

with unused terms omitted by profile.

Moreover,

\[
H_{retained}(T)-H_{retained}(0)
\le
N_{commit}(T)\cdot b_{commit,max},
\]

and in any case

\[
H_{retained}(T) \le M_{persist}.
\]

### 7.2 Proof — step 1: commit count bound

Each successful authoritative commit consumes at least one declared bounded resource unit.

#### Memory-headroom route

If each successful commit consumes at least `b_commit,min` bits of persistent-state headroom, then the total number of such commits cannot exceed

\[
\left\lfloor \frac{M_{persist}}{b_{commit,min}} \right\rfloor.
\]

#### Calibrated-commit-cost route

If each successful commit consumes at least `e_commit,min` units of calibrated commit cost, then the total number of such commits by horizon `T` cannot exceed

\[
\left\lfloor \frac{E_{commit}(T)}{e_{commit,min}} \right\rfloor.
\]

#### Irreversibility-budget route

If each successful commit consumes at least `i_commit,min` units of irreversibility expenditure, then the total number of such commits by horizon `T` cannot exceed

\[
\left\lfloor \frac{I_{max}(T)}{i_{commit,min}} \right\rfloor.
\]

If more than one resource discipline is declared, the actual number of successful commits must satisfy all declared limits simultaneously. Therefore the number of successful commits is bounded by the smallest active bound:

\[
N_{commit}(T)
\le
\min
\left(
\left\lfloor \frac{M_{persist}}{b_{commit,min}} \right\rfloor,
\left\lfloor \frac{E_{commit}(T)}{e_{commit,min}} \right\rfloor,
\left\lfloor \frac{I_{max}(T)}{i_{commit,min}} \right\rfloor
\right).
\]

This proves the commit-count bound.

### 7.3 Proof — step 2: retained-entropy increment bound

Let the retained authoritative state at the commit horizon be `R_T`. Let the successful authoritative commits be indexed in order `j=1,...,N_commit(T)`. By assumption, each successful commit contributes at most `b_commit,max` bits of retained authoritative content. Therefore the conditional contribution of each commit to retained authoritative uncertainty is bounded by `b_commit,max`.

By Lemma C,

\[
H_{retained}(T)-H_{retained}(0)
\le
N_{commit}(T)\cdot b_{commit,max}.
\]

### 7.4 Proof — step 3: absolute retained-state ceiling

Retained authoritative state lives inside finite persistent memory. Therefore, regardless of how commits are counted,

\[
H_{retained}(T) \le M_{persist}
\]

by Lemma B applied to the retained authoritative bit-addressable memory carrier.

Hence retained authoritative novelty cannot grow without bound. ∎

### 7.5 Why this proof is narrower than the old Landauer-style line

The proof binds retention through:

- declared commit boundaries,
- per-commit maximum retained content,
- and bounded resource expenditure.

That is stronger engineering discipline than saying “entropy retention is bounded by energy” in the abstract.

### 7.6 What this proof does **not** prove

This proof does **not** justify the universal statement

\[
H_{retained}(T) \le \frac{E_{total}}{k_B T \ln 2}
\]

for arbitrary classical ARQ entities.

To justify that stronger physical claim, one would need additional assumptions, including at minimum:

1. a specific irreversible physical commit mechanism;
2. a calibrated map from retained authoritative bits to actual dissipative operations;
3. a declared thermal operating regime;
4. a declared dissipation path and non-replenished relevant budget;
5. a proof that every retained authoritative bit necessarily incurs that physical minimum cost in the model.

Without those assumptions, energy is a **resource bound on commits**, not a universal entropy oracle.

---

## 8. Detailed Proof of Theorem 3
## Finite Pending / Backlog Bound

### 8.1 Statement

Assume Model M4.

Let the ARQ implementation maintain an unresolved pending-event structure with capacity `K < ∞`, where each unresolved event occupies at most `B_max < ∞` bits of queue-accounted pending representation.
Then for all `t`:

\[
H_{pending}(t) \le K\cdot B_{max}.
\]

### 8.2 Proof

At any time `t`, the pending-event structure contains at most `K` unresolved entries by queue-capacity assumption.

For each unresolved entry, the maximum queue-accounted representation is at most `B_max` bits. Therefore the total queue-accounted representation size is bounded by

\[
K\cdot B_{max}
\]

bits.

Applying Lemma D gives

\[
H_{pending}(t) \le K\cdot B_{max}.
\]

Hence unresolved ambiguity cannot accumulate without bound inside the declared queue. ∎

### 8.3 Important reading discipline

This proof bounds only **declared pending representation**.
It does not automatically bound:

- arbitrary external log buffers,
- undeclared debugging traces,
- cached model states outside the declared queue,
- or any side channel not counted by the queue model.

If those exist and matter, they must be modeled separately.

---

## 9. Detailed Proof of Corollary 1
## Composite Classical ARQ Runtime Envelope

### 9.1 Statement

Assume Models M1, M2, M3, and M4.

Let the declared classical runtime envelope be

\[
Y_t=(X_t,Q_t),
\]

where:

- `X_t` is the authoritative persistent state from Model M1;
- `Q_t` is the pending/backlog state from Model M4.

Then, during a valid epoch,

\[
H(Y_t)
\le
M_{persist}+\log_2|C_{mode}|+K\cdot B_{max}.
\]

Also, retained authoritative novelty remains commit-bounded as in Theorem 2.

### 9.2 Proof

By the chain rule for Shannon entropy,

\[
H(Y_t)=H(X_t,Q_t)=H(X_t)+H(Q_t\mid X_t).
\]

Conditioning cannot increase entropy, so

\[
H(Q_t\mid X_t) \le H(Q_t).
\]

Therefore,

\[
H(Y_t) \le H(X_t)+H(Q_t).
\]

By Theorem 1,

\[
H(X_t) \le M_{persist}+\log_2|C_{mode}|.
\]

By Theorem 3,

\[
H(Q_t)=H_{pending}(t) \le K\cdot B_{max}.
\]

Adding the bounds yields

\[
H(Y_t)
\le
M_{persist}+\log_2|C_{mode}|+K\cdot B_{max}.
\]

By Theorem 2, retained authoritative novelty is separately bounded by commit authority and finite persistent memory.

Model M3 contributes the validity gate: these bounds are the operational ARQ bounds during a valid epoch. Outside a valid epoch, promotion authority is withdrawn and the implementation MUST degrade or fail closed according to the trust/profile rules. ∎

### 9.3 Why M3 enters only as a gate

M3 is not needed to prove the finite-support or finite-queue inequalities themselves.
It enters the corollary because ARQ runtime claims are claims about **admissible normal operation**, and admissible normal operation exists only inside a valid trust epoch.

---

## 10. Non-Theorem Limitation Table

| Tempting overclaim | Why it does not follow from this proof companion |
|---|---|
| “All classical ARQ entropy is bounded by energy alone.” | False without a declared physical commit mechanism and dissipation model. |
| “If memory is finite, the whole machine is automatically bounded in every respect.” | False; pending queues, side channels, and invalid epochs must be modeled separately. |
| “Cooling rate by itself gives a universal lifetime entropy bound.” | Not in this theorem set; cooling here matters through declared budgets and valid-epoch operation, not as a single magical scalar. |
| “The theorem applies even during invalid trust epochs.” | No; M3 explicitly restricts normal ARQ authority to valid epochs. |
| “Undeclared logs are automatically bounded because the authoritative state is bounded.” | No; undeclared storage is outside the theorem carrier until modeled. |

---

## 11. Reviewer Checklist

A reviewer checking a classical boundedness claim in ARQ SHOULD ask:

1. Which theorem is being invoked: persistent-state, retained-entropy, pending-backlog, or the composite corollary?
2. Which model carrier is declared?
3. Is `M_persist` measured in bits or in abstract memory states?
4. Is there a declared commit primitive?
5. Is there a declared queue with capacity `K` and maximum representation `B_max`?
6. Is the claim being made inside a valid epoch?
7. Is anyone trying to smuggle Landauer in as a universal theorem without a physical commit model?

If any of these answers is missing, the proof citation is too loose.

---

## 12. Proof Revision Discipline

### 12.1 Anti-echo rule

A revision SHALL NOT be accepted merely because it restates finite-memory boundedness in fancier words.

### 12.2 A/B-slot proof editing

Proof revisions SHOULD use:

- **Slot A** — current canonical proof text;
- **Slot B** — proposed revised proof text.

A Slot B revision may replace Slot A only if all of the following hold:

1. it preserves the valid earlier claim;
2. it makes the model carrier clearer;
3. it does not strengthen assumptions silently;
4. it reduces, rather than increases, thermodynamic overclaim;
5. it remains checkable against the theorem and notation docs.

### 12.3 Auto-rollback rule

If a proof revision improves elegance but weakens claim honesty, it MUST be rolled back automatically.

This is especially important around “energy therefore entropy” rhetoric, where overclaim often arrives wearing a nice suit.

---

## 13. Bridges (required)

### Explicit bridge

The parent theorem document states the boundedness claims; this proof companion makes them reviewable. Together they bind ARQ's classical boundedness to declared models rather than intuition.

### Hidden bridge 1 — SER / L4 / ARQ

SER says persistence must remain reality-bound; L4 says reality is non-negotiable; ARQ says retained novelty must cross a controlled authority boundary. The proof companion is where those three statements stop being slogans and become accounting.

### Hidden bridge 2 — L4 Witness / Trust profile / Information theory

Witness and trust do not increase the finite-support theorem by themselves, but they determine what counts as authoritative state, retained state, and valid operation. Information theory gives the entropy bound; witness and trust decide which bits are allowed to count.

---

## 14. Earth Paragraph (engineering / anatomy)

A body can only keep so much structured injury “in play” before it either heals, scars, or shuts a process down. A machine is similar: some state is already in the tissue, some is only in the bloodstream for a while, and some changes become scar tissue because they were committed into long-term structure. Classical ARQ boundedness works the same way. Persistent memory is the tissue, the queue is the bloodstream, the commit is the scar, and the valid epoch is the circulation that keeps the whole thing alive without lying about what is actually under control.

---

## 15. Closing Statement

This proof companion establishes a narrow but durable claim:

> In classical ARQ, boundedness is real when the system is modeled honestly.

Finite authoritative state, finite commit authority, finite pending representation, and valid trust epochs are enough to prove the classical boundedness results that ARQ actually needs.

What they are **not** is permission to wave a thermodynamic wand over every deployment and declare the matter closed.
