# ARQ_Notation_and_Sign_Conventions_v0.2
## Canonical Notation and Sign Conventions for the ARQ v0.2 Supplement

**Status:** Draft / normative support document  
**Version:** 0.2-draft  
**Role:** notation discipline, sign semantics, anti-ambiguity layer  
**Parent documents:** `ARQ_v0.2_Normative_Core.md`, `ARQ_System_Models_and_Assumptions_v0.2.md`  
**Parent corpus:** AGI / SER / L4 / L4 Witness / Beacon / VXCX  
**Author:** Ivan Kotov  
**Place / year:** Bruxelles, 2026

---

## 0. Purpose

ARQ uses the language of entropy, coherence, utility, cost, trust, witness, and—optionally—usable entanglement. Those terms are not interchangeable.

This document establishes the **canonical notation and sign conventions** for the ARQ v0.2 supplement. Its purpose is simple:

> a symbol must say one thing, with one sign meaning, inside one declared model boundary.

Without that discipline, the same quantity may appear once as an exploration signal, once as a coherence signal, and once as a pseudo-probability. That destroys auditability.

This document therefore fixes:

- the canonical symbols used by ARQ;
- the meaning of positive and negative sign for each delta term;
- the distinction between classical, quantum, trust, and witness quantities;
- the reserved names for raw value, trust-adjusted value, anomaly score, and posterior probability;
- the minimum notation rules that all ARQ v0.2 companion documents SHALL follow.

---

## 1. Scope

This document specifies:

1. the canonical symbols for ARQ reasoning;
2. the sign convention for entropy-, coherence-, and entanglement-related deltas;
3. the naming rules for trust and anomaly quantities;
4. the minimum notation block required by ARQ companion documents;
5. prohibited ambiguities and overloaded legacy usages.

This document does **not** define the value function weights themselves, the witness schema itself, or the proof content of any theorem. It defines the notation used to state them.

---

## 2. Non-Goals

This document does **not** attempt to:

- collapse classical and quantum state into one universal object;
- declare one sign convention to be metaphysically superior;
- turn a heuristic anomaly score into a probability by typography alone;
- replace model declarations from `ARQ_System_Models_and_Assumptions_v0.2.md`;
- rescue an unclear theorem by notational ornament.

This document exists to remove ambiguity, not to decorate it.

---

## 3. Normative Keywords

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, **MAY**, and **OPTIONAL** are to be interpreted as described in BCP 14.

---

## 4. General Notation Discipline

### 4.1 One symbol, one meaning

Within the ARQ v0.2 supplement, a symbol SHALL have exactly one declared meaning per document.

If a document imports a legacy symbol with a different meaning, it MUST provide an explicit mapping at first use.

### 4.2 Symbol reuse across models

A symbol MAY be reused across documents only if:

1. the model class is the same, and
2. the semantics are unchanged.

Otherwise a new symbol or an explicit subscript MUST be introduced.

### 4.3 Narrative prose does not override notation

If narrative text and symbolic definition disagree, the symbolic definition SHALL take precedence unless explicitly marked as non-normative commentary.

### 4.4 Model declaration requirement

Any theorem, bound, or valuation formula in the ARQ supplement MUST identify the system model that carries it, using the model identifiers from `ARQ_System_Models_and_Assumptions_v0.2.md`.

### 4.5 Sign declaration requirement

Any delta quantity in ARQ MUST be introduced with a sign sentence of the form:

> “Positive means … ; negative means … .”

No delta term SHALL be used without such a declaration.

---

## 5. Time, Epoch, and Event Indexing

### 5.1 Continuous time

- `t` = continuous or wall-clock time, as appropriate for the document.
- Time stamps in witnessable records MUST be ISO 8601 with timezone.

### 5.2 Epoch index

- `k` = calibration / trust epoch index.
- `e_k` = epoch identifier for epoch `k`.

### 5.3 Event index

- `n` = ARQ event index within a witness chain.
- `cap_n` = the `n`-th ARQ capsule.

### 5.4 Pre / post notation

For any event-local state transition:

- `pre` = state immediately before the event under the declared boundary;
- `post` = state immediately after the event under the declared boundary.

Documents SHALL NOT use `before`, `after`, `old`, `new`, `initial`, `final` interchangeably when `pre` and `post` are already defined.

---

## 6. Canonical State Symbols

### 6.1 Classical authoritative persistent state

- `X_t` = authoritative classical persistent state at time `t`.
- `M_persist` = number of bits available for authoritative persistent state.
- `C_mode` = finite controller mode set.

If Model M1 is used, the authoritative state space is written as:

\[
X_t \in \{0,1\}^{M_{persist}} \times C_{mode}.
\]

### 6.2 Quantum / hybrid state

- `\rho(t)` = density operator of the declared quantum or hybrid system.
- `\rho_{SA}(t)` = reduced density operator on the trusted quantum boundary.
- `\rho_S(t)` = reduced state on the system register of interest.
- `\rho_U(t)` = reduced state on the uncontrolled environment, if needed.

### 6.3 Expected and observed references

- `x_exp`, `\rho_exp` = expected state or reference state inside the declared model.
- `x_obs`, `\rho_obs` = observed state or state estimate inside the declared model.

When raw state is too large or private to embed directly, a document MAY use:

- `ref_exp` = compact reference to expected state;
- `ref_obs` = compact reference to observed state.

---

## 7. Boundary and Dimension Symbols

### 7.1 Declared boundary

- `B_decl` = declared ARQ operational boundary.
- `B_trust` = trusted sub-boundary inside which attribution and valuation are allowed.
- `B_U` = uncontrolled environment or outside-of-boundary region.

### 7.2 Quantum Hilbert spaces

- `\mathcal H_S` = system Hilbert space.
- `\mathcal H_A` = trusted ancilla Hilbert space.
- `\mathcal H_U` = uncontrolled environment Hilbert space.
- `\mathcal H_{SA} = \mathcal H_S \otimes \mathcal H_A` = trusted quantum boundary.

### 7.3 Dimensions

- `d_S = \dim(\mathcal H_S)`
- `d_A = \dim(\mathcal H_A)`
- `d_{SA} = \dim(\mathcal H_{SA})`

These dimensions SHALL be used in quantum boundedness statements rather than vague phrases such as “finite hardware” unless the theorem is explicitly non-formal.

---

## 8. Entropy, Information, and Related Measures

### 8.1 Classical entropy

- `H(X)` = Shannon entropy of a classical state or distribution `X`.

All classical entropy values in ARQ SHALL be measured in **bits** unless a document explicitly states another base.

### 8.2 Quantum entropy

- `S(\rho)` = von Neumann entropy of density operator `\rho`.

All quantum entropy values in ARQ SHALL be measured in **bits**, i.e. using `\log_2`.

### 8.3 Mutual information

- `I(X;Y)` = mutual information between classical random variables `X` and `Y`.
- `I(A:B)` = quantum or classical mutual information, only if the document defines which version is used.

No document SHALL use `I` without specifying whether it is classical or quantum mutual information when ambiguity exists.

### 8.4 Relative entropy / divergence

- `D_{KL}(P\|Q)` = Kullback–Leibler divergence for classical distributions.
- `D(\rho\|\sigma)` = quantum relative entropy, if used.

Relative entropy quantities SHALL NOT be called “distance” without qualification.

---

## 9. Canonical Delta Terms and Their Signs

This section is critical.

ARQ uses **two different entropy-direction intuitions**, and they MUST NOT be merged silently.

### 9.1 Exploration entropy shift

The canonical exploration delta is:

\[
\Delta H_{exp} = H(post) - H(pre).
\]

**Sign meaning:**

- `\Delta H_exp > 0` = post-state carries **more uncertainty / more reachable variability / more explored state space** than pre-state.
- `\Delta H_exp < 0` = post-state is **more compressed / more settled / less variable** than pre-state.

Use `\Delta H_exp` when ARQ is evaluating **novelty, optionality, branching, or exploration** in a classical or abstract state-space sense.

### 9.2 Order / coherence restoration delta

The canonical order/coherence delta is:

\[
\Delta S_{ord} = S(pre) - S(post).
\]

**Sign meaning:**

- `\Delta S_ord > 0` = post-state is **more ordered / more coherent / less locally entropic** than pre-state.
- `\Delta S_ord < 0` = post-state is **less ordered / less coherent / more locally entropic** than pre-state.

Use `\Delta S_ord` when ARQ is evaluating **restored coherence, order recovery, or reduction of local disorder**, especially in quantum or hybrid settings.

### 9.3 Hard anti-conflation rule

`\Delta H_exp` and `\Delta S_ord` SHALL NOT be denoted by the same bare symbol in the same document.

A document MUST NOT write `\Delta H` in one section with exploration meaning and `\Delta S` in another section with coherence-restoration meaning unless both are explicitly mapped in a notation preamble.

### 9.4 Retained-entropy quantity

If a document speaks specifically about entropy retained in authoritative persistent state, it SHALL use:

\[
H_{retained}
\]

or

\[
\Delta H_{retained}(T).
\]

This symbol is reserved for **retained authoritative memory content**, not for temporary queue state, controller heat, or whole-device thermodynamic disorder.

### 9.5 Pending / queue entropy quantity

If a document speaks about unresolved online event backlog, it SHOULD use:

\[
H_{pending}(t).
\]

This quantity is distinct from `H_retained` and MUST NOT be mixed with it.

---

## 10. Utility, Cost, Risk, and Value Symbols

### 10.1 Utility

- `U_post` or `U(post)` = downstream utility of the post-state inside the declared task frame.

A document MUST define whether utility is:

- task-relative,
- policy-relative,
- or review-window-relative.

### 10.2 Operational cost

- `C_op` = operational cost term.

If cost is normalized, the document SHOULD state:

\[
C_{op} \in [0,1].
\]

If cost is not normalized, the document MUST state its units and normalization rule before combining it with other terms.

### 10.3 Stability / instability risk

- `R_inst` = instability risk term.

`R_inst` is reserved for **risk of destabilization, incoherence, fragility, or unsafe propagation**, not legal or reputational risk unless explicitly extended.

### 10.4 Usable entanglement

- `E_use(\rho)` = usable entanglement inside the trusted quantum boundary.
- `\Delta E_{use} = E_{use}(post) - E_{use}(pre)`.

**Sign meaning:**

- `\Delta E_use > 0` = the event increased usable controlled correlation.
- `\Delta E_use < 0` = the event reduced usable controlled correlation.

The alias `Eusable` MAY appear only as a legacy mapping and SHOULD be replaced by `E_use` in v0.2 documents.

### 10.5 Raw valuation

- `V_raw` = value of an event before trust adjustment.

Canonical generic form:

\[
V_{raw} = f(\Delta H_{exp}, \Delta S_{ord}, U_{post}, C_{op}, R_{inst}, \Delta E_{use}; \theta)
\]

where `\theta` denotes policy parameters.

No document is required to use all terms. But missing terms MUST be omitted explicitly rather than silently set to zero.

### 10.6 Trust-adjusted valuation

- `V_trust` = trust-adjusted event value used for operational classification.

The legacy notation `V'` MAY be used only if the document explicitly declares:

> `V' := V_trust`.

In new ARQ v0.2 documents, `V_trust` is preferred.

### 10.7 Thresholds

- `V_promote` = threshold above which promotion path becomes admissible.
- `V_suppress` = threshold below which suppression path becomes admissible.
- `V_high` = threshold above which second-signature or special review path is required.

Thresholds SHALL NOT be used without identifying whether they apply to `V_raw` or `V_trust`.

---

## 11. Trust, Anomaly, and Posterior Notation

This section closes a major ambiguity from earlier drafts.

### 11.1 Attestation validity flag

- `A_valid \in \{0,1\}` = attestation / epoch validity indicator.

`A_valid = 1` means the event occurred inside a valid trust epoch and the required signatures verify.

### 11.2 Operational anomaly score

- `A_anom \in [0,1]` = normalized operational anomaly score.

**Sign meaning:**

- `A_anom = 0` = event looks fully ordinary under the declared baseline;
- `A_anom = 1` = event is maximally suspicious under the declared baseline.

`A_anom` is the **preferred ARQ v0.2 symbol** for the operational anomaly quantity unless a fully specified Bayesian model is used.

### 11.3 Bayes factor / likelihood ratio

- `B_anom` = Bayes factor or likelihood ratio comparing anomaly and nominal hypotheses.

A document MAY use `B_anom`, but only if the compared hypotheses are explicitly declared.

### 11.4 Posterior probability (reserved)

- `P_anom` = posterior probability of anomaly.

**Reserved rule:**
`P_anom` SHALL be used only if the document declares:

1. prior probabilities,
2. likelihood model,
3. evidence model,
4. and the mapping from evidence to posterior.

A heuristic score MUST NOT be written as `P_anom` merely because it lies in `[0,1]`.

### 11.5 Trust weight

- `\tau \in [0,1]` = trust weight applied to event authority or event value.

A canonical minimal operational form is:

\[
\tau = A_{valid}\cdot(1-A_{anom}).
\]

If a document uses a different trust composition, it MUST state the exact formula.

### 11.6 Trust floor

- `\tau_{min}` = minimum trust threshold below which privileged ARQ actions are blocked.

### 11.7 Invalidation event

- `I_{epoch}` = epoch invalidation event.

When invalidation occurs, the document SHOULD speak of **epoch invalidation** or **trust invalidation**, not of “entropy collapse,” unless a physical model is explicitly in use.

---

## 12. Witness, Hash, and Signature Symbols

### 12.1 Hash symbols

- `h_prev` = hash of the preceding witness record.
- `h_cap` = hash of the current capsule payload.
- `h_att` = hash of the attestation report bound to the active epoch.
- `h_ctrl` = hash of controller-state log record.

### 12.2 Signature symbols

- `sig_c` = signature by entity `c`.
- `sig_a` = signature by human anchor `a` or designated delegate.
- `sig_q` = quorum or arbiter signature set, if used.

### 12.3 Witness linkage symbols

- `w_ref` = witness reference pointer.
- `epoch_ref` = explicit reference to active epoch.
- `chain_ref` = reference to the current append-only chain context.

No document SHALL describe a record as “witnessed” if it lacks a reproducible link to `h_prev` or equivalent chain continuity.

---

## 13. Lifecycle and Status Labels

The following labels are canonical for ARQ v0.2 lifecycle descriptions.

### 13.1 Event-stage labels

- `detected`
- `classified`
- `suppressed`
- `observed`
- `candidate`
- `provisional`
- `promoted`
- `rejected`
- `log_only`
- `fail_closed`
- `quarantined`

### 13.2 Memory-authority labels

- `candidate_artifact` = not yet authoritative memory.
- `provisional_artifact` = passed first review but still subject to bounded confirmation.
- `confirmed_EA` = authoritative Experience Artifact.
- `retired_EA` = historical artifact no longer active in authority weighting.

**Hard rule:**
A `candidate_artifact` SHALL NOT be called an EA.

### 13.3 Learning vs experience labels

- `LA` = Learning Abstract.
- `EA` = Experience Artifact.

These terms SHALL NOT be used interchangeably.

---

## 14. A/B Slots, Quarantine, and Rollback Symbols

### 14.1 Canonical slots

- `Slot_A` = last-known-good canonical state / policy / notation / threshold set.
- `Slot_B` = candidate refinement under review.

### 14.2 Rollback operator

- `Rollback(B \rightarrow A)` = automatic reversion from candidate slot to canonical slot after failed review.

### 14.3 Quarantine label

- `Q_selfsim` = self-similarity quarantine label for anti-echo enforcement.

A document that introduces A/B slot logic SHOULD use these labels rather than inventing synonyms such as “main / temp”, “gold / test”, or “old / new”.

---

## 15. Units, Normalization, and Base Conventions

### 15.1 Entropy units

All entropy quantities in ARQ v0.2 SHALL be expressed in **bits** unless explicitly stated otherwise.

### 15.2 Time units

- Witnessed timestamps: ISO 8601 with timezone.
- Operational latency budgets: declared engineering units (`ms`, `s`, etc.).

### 15.3 Cost normalization

If `C_op` is aggregated from heterogeneous resources such as energy, time, and privilege, the document MUST declare either:

1. how each component is normalized, or
2. the exact units and weighting rule.

### 15.4 Utility normalization

If `U_post` is combined additively with entropy- or cost-terms, the document MUST declare either:

- explicit normalization into a shared range, or
- coefficient values that restore dimensional consistency.

### 15.5 Mixed-unit prohibition

A document SHALL NOT add terms of incompatible units while describing the result as “formal” unless it also defines the normalization or weighting that makes the combination legitimate.

---

## 16. Legacy Mapping Table

This table exists to stabilize transition from v0.1 language.

| Legacy expression | Canonical v0.2 form | Rule |
|---|---|---|
| `ΔH = H(post)-H(pre)` | `ΔH_exp` | Use for exploration / optionality |
| `ΔS = S(pre)-S(post)` | `ΔS_ord` | Use for restored order / coherence |
| `Eusable` | `E_use` | Legacy alias only |
| `V'` | `V_trust` | Declare mapping on first use |
| heuristic `P_anom` in `[0,1]` | `A_anom` | Use `P_anom` only under explicit Bayesian model |
| “valuable error” before review | `candidate_artifact` or `provisional_artifact` | Not yet EA |

No ARQ v0.2 document SHALL import a legacy term without either adopting the canonical form or citing this mapping.

---

## 17. Minimum Notation Block Required in Companion Documents

Every ARQ v0.2 companion document that introduces formulas MUST include, near the beginning, a minimal notation block stating at least:

1. which system model(s) are active;
2. whether it uses `H`, `S`, or both;
3. which delta convention is active (`ΔH_exp`, `ΔS_ord`, `ΔE_use`, etc.);
4. whether anomaly is represented as `A_anom`, `B_anom`, or `P_anom`;
5. whether value is `V_raw` or `V_trust`.

A document that omits this block SHOULD be treated as draft-internal rather than canonical.

---

## 18. Prohibited Ambiguities

The following are explicitly prohibited in canonical ARQ v0.2 text.

### 18.1 Bare `ΔH` with mixed meanings

A document MUST NOT use bare `ΔH` to mean “more exploration” in one place and “more order” in another.

### 18.2 Heuristic score labeled as probability

A heuristic anomaly quantity MUST NOT be labeled `P_anom` unless a posterior model is actually declared.

### 18.3 “Entropy” without boundary

A document MUST NOT say simply “the entropy of the entity” unless it declares whether that means:

- authoritative classical persistent state,
- trusted quantum boundary,
- retained authoritative memory,
- pending unresolved queue,
- or physical thermodynamic whole-device entropy.

### 18.4 EA before review

A record SHALL NOT be called an EA before it passes the declared ARQ promotion path.

### 18.5 Trusted boundary = whole world

In quantum or hybrid ARQ, the trusted boundary SHALL NOT be silently extended to include uncontrolled environment, external instrumentation, or undeclared ancillas.

---

## 19. Relationship to Parent Corpus

This notation layer aligns with the broader corpus as follows:

- with **SER**, it preserves the distinction between authoritative memory and mere operational flux;
- with **L4**, it forces every quantity to live inside a declared resource and boundary frame;
- with **L4 Witness**, it distinguishes state, evidence, and attribution symbols rather than collapsing them into narrative;
- with **Beacon**, it preserves the difference between continuity signals and performance theatre;
- with **VXCX**, it respects bounded payloads and explicit uncertainty markers.

Notation is not external to architecture. It is part of boundary discipline.

---

## 20. Bridges (required)

### Explicit bridge

`c = a + b` becomes operationally stable only if the terms used to describe `b` do not silently mutate across documents. ARQ notation therefore binds state, value, trust, witness, and memory promotion into one declared symbol system.

### Hidden bridge #1 (Cybernetics / Ashby)

A regulator cannot remain stable if its own signals are overloaded. Requisite variety applies not only to sensors and actuators, but also to symbols: if one sign means two opposite things, the controller loses control before the hardware does.

### Hidden bridge #2 (Information Theory / Cover & Thomas)

A notation system is a coding system. Good notation preserves semantic distinguishability under bounded bandwidth. ARQ therefore compresses meaning into explicit symbol roles—entropy, anomaly, witness, trust—rather than letting prose blur them into one channel.

---

## 21. Earth Paragraph (engineering)

This is the same problem as a wiring diagram or a control board. If one terminal is labeled “+” in one page and “return” in the next, sooner or later someone will not write a paper—they will burn a board. In anatomy it is similar: heart rate, oxygen saturation, and blood pressure all describe “how the patient is doing,” but they are not the same signal and cannot share one unlabeled axis. ARQ notation exists for the same earthy reason: when a system starts shaking, the symbols must still point to the right organ.

---

## 22. Closing Statement

ARQ is allowed to be ambitious. It is not allowed to be vague.

The point of this document is therefore modest and severe:

> if a symbol enters the ARQ supplement, it must keep its job.

