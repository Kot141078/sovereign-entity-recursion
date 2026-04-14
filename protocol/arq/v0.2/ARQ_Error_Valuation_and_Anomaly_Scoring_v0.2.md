# ARQ_Error_Valuation_and_Anomaly_Scoring_v0.2
## Error Valuation and Anomaly Scoring for the ARQ v0.2 Supplement

**Status:** Draft / normative support document  
**Version:** 0.2-draft  
**Role:** valuation core, anomaly discipline, trust-adjusted scoring  
**Parent documents:** `ARQ_v0.2_Normative_Core.md`, `ARQ_System_Models_and_Assumptions_v0.2.md`, `ARQ_Notation_and_Sign_Conventions_v0.2.md`  
**Parent corpus:** AGI / SER / L4 / L4 Witness / Beacon / VXCX  
**Author:** Ivan Kotov  
**Place / year:** Bruxelles, 2026

---

## 0. Abstract

ARQ does not ask only whether a deviation occurred. It asks whether the deviation should be suppressed, observed, quarantined, or allowed to enter a witnessed review path.

That decision requires two distinct judgments:

1. **error valuation** — does the event expand viable future behavior, restore useful order, or merely consume budget and raise instability;
2. **anomaly scoring** — how suspicious is the event under the current boundary, controller, epoch, and witness assumptions.

This document defines the canonical ARQ v0.2 scoring pipeline that combines those two judgments without collapsing them into one mystical number.

The central discipline is simple:

> A deviation may be interesting without being trustworthy.  
> A deviation may be trustworthy without being valuable.  
> ARQ promotion authority begins only where both conditions survive explicit gates.

This document therefore specifies:

- the canonical raw valuation function `V_raw`,
- admissible anomaly-scoring profiles,
- the trust-composition rule producing `τ`,
- the trust-adjusted value `V_trust`,
- threshold semantics,
- anti-echo penalties,
- and the A/B-slot update discipline for tuning weights and thresholds.

---

## 1. Purpose

This document exists to answer one operational question:

> Given a bounded ARQ event inside a declared boundary, what score is computed, what trust discount is applied, and what action band becomes admissible?

It SHALL provide:

1. a canonical scoring pipeline for ARQ events;
2. a default operational anomaly profile that is honest about being a score rather than a probability;
3. an optional Bayesian profile for implementations that can justify priors and likelihoods;
4. explicit rules for trust-adjusted scoring;
5. minimum governance requirements for weights, thresholds, and score updates.

This document is part of the ARQ v0.2 supplement because the earlier ARQ text contained the right intuition but left three things too loose:

- the sign/meaning separation between exploration and order restoration,
- the distinction between anomaly score and anomaly probability,
- and the tuning discipline for thresholds and weights over time.

---

## 2. Scope

This document specifies:

1. the canonical ARQ scoring pipeline;
2. the required inputs for raw valuation;
3. the admissible anomaly-scoring profiles;
4. the trust-weight computation;
5. threshold semantics for `suppress`, `observe`, `log_only`, `candidate`, and `fail_closed` recommendation bands;
6. update governance for scoring parameters;
7. minimum evidence required for audit and replay.

This document does **not** define:

- the witness schema itself;
- the EA lifecycle beyond score-related gates;
- the boundedness theorems themselves;
- the implementation profile details for every subsystem;
- the legal or institutional consequences of a scored event.

---

## 3. Non-Goals

This document does **not** attempt to:

- prove that a numerically positive event is genuinely wise;
- infer causality from one scalar score;
- convert a heuristic anomaly indicator into a posterior probability by typography;
- justify promotion without witness;
- let novelty alone outrank trust;
- or let self-similar internal repetition masquerade as valuable exploration.

This is a control document, not a mythology engine.

---

## 4. Normative Keywords

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, **MAY**, and **OPTIONAL** are to be interpreted as described in BCP 14.

---

## 5. Imported Symbols and Dependencies

This document imports the canonical notation from `ARQ_Notation_and_Sign_Conventions_v0.2.md` and the admissible model classes from `ARQ_System_Models_and_Assumptions_v0.2.md`.

At minimum, companion implementations SHALL use the following symbols with the meanings fixed there:

- `ΔH_exp` — exploration entropy shift,
- `ΔS_ord` — order / coherence restoration shift,
- `U_post` — downstream utility,
- `C_op` — operational cost,
- `R_inst` — instability risk,
- `ΔE_use` — usable-entanglement shift,
- `A_valid` — attestation / epoch validity flag,
- `A_anom` — operational anomaly score,
- `B_anom` — Bayes factor / likelihood ratio, if used,
- `P_anom` — posterior anomaly probability, only if Bayesian profile is declared,
- `τ` — trust weight,
- `V_raw` — raw event value,
- `V_trust` — trust-adjusted event value.

A conformant document or implementation MUST also declare which model class or classes carry its scoring claims:

- `M1` — classical persistent-state model,
- `M2` — commit-metered retention model,
- `M3` — epoch-gated trust / control model,
- `M4` — online queue / backlog model,
- `M5` — fixed trusted quantum boundary model.

No ARQ scoring claim SHALL be stated without a declared model carrier.

---

## 6. Scoring Pipeline Overview

A conformant ARQ scoring pipeline SHALL conceptually proceed in the following order:

1. **Boundary check**  
   Confirm that the event occurred inside a declared ARQ boundary.

2. **Input extraction**  
   Extract or estimate the quantities needed for raw valuation and anomaly scoring.

3. **Raw valuation**  
   Compute `V_raw` from declared value terms.

4. **Anomaly scoring**  
   Compute either `A_anom` (default) or `P_anom` (Bayesian profile).

5. **Trust composition**  
   Compute `τ` from trust validity and anomaly result.

6. **Trust-adjusted valuation**  
   Compute `V_trust` using `V_raw`, `τ`, and trust-sensitive penalties.

7. **Hard gate check**  
   Apply fail-closed, privilege, witness, and quarantine rules.

8. **Action band output**  
   Output one of the admissible recommended actions:
   - `suppress`,
   - `observe`,
   - `log_only`,
   - `candidate`,
   - `fail_closed`.

9. **Witness recording**  
   Record all score inputs, omitted terms, profile identifiers, thresholds, and outputs in the witness trail.

A conformant implementation MUST NOT skip directly from raw novelty to EA authority.

---

## 7. Canonical Raw Valuation Function

### 7.1 General form

The canonical ARQ raw valuation function is:

\[
V_{raw} =
\alpha_{exp}\,\Delta H_{exp}
+ \alpha_{ord}\,\Delta S_{ord}
+ \beta\,U_{post}
- \gamma\,C_{op}
- \delta\,R_{inst}
+ \epsilon\,\Delta E_{use}.
\]

Where:

- `α_exp ≥ 0` weights exploratory state-space expansion;
- `α_ord ≥ 0` weights restored order / coherence;
- `β ≥ 0` weights downstream utility;
- `γ ≥ 0` weights operational cost;
- `δ ≥ 0` weights instability risk;
- `ε ≥ 0` weights usable entanglement shift, if quantum profile is active.

### 7.2 Omission rule

Not every profile uses every term.

A conformant implementation MAY omit terms that are not meaningful under its declared model, but it MUST do so explicitly.

Examples:

- a classical exploratory profile MAY set `α_ord = 0` and `ε = 0`;
- a coherence-restoration profile MAY set `α_exp = 0`;
- a quantum profile MAY use all terms except where utility is undefined or intentionally omitted.

A term that is omitted MUST be recorded as `omitted_by_profile`, not silently treated as unknown.

### 7.3 Normalization requirement

Because the value function combines heterogeneous terms, the implementation MUST do one of the following:

1. normalize all included terms into a common bounded range, such as `[-1,1]` or `[0,1]`; or
2. declare the exact coefficient values and units that make the combination operationally meaningful.

A document or implementation SHALL NOT call `V_raw` “formal” while mixing incompatible units without declared normalization.

### 7.4 Sign semantics

The meaning of each delta term is inherited from the notation document and SHALL NOT be redefined locally.

In particular:

- `ΔH_exp > 0` means more explored reachable variability;
- `ΔS_ord > 0` means restored order / reduced local disorder;
- `ΔE_use > 0` means more usable controlled correlation.

A profile MUST NOT use the same symbol to mean both “more exploration” and “more order” in the same formula.

---

## 8. Recommended Raw-Valuation Profiles

### 8.1 Profile `VAL-CLASSICAL-EXPLORE`

For classical persistent-state or planner systems where exploratory novelty matters:

\[
V_{raw} = \alpha_{exp}\,\Delta H_{exp} + \beta\,U_{post} - \gamma\,C_{op} - \delta\,R_{inst}.
\]

Use when Model `M1` or `M4` is primary.

### 8.2 Profile `VAL-CLASSICAL-ORDER`

For rollback, recovery, or stabilization subsystems where restored order matters more than exploratory branching:

\[
V_{raw} = \alpha_{ord}\,\Delta S_{ord} + \beta\,U_{post} - \gamma\,C_{op} - \delta\,R_{inst}.
\]

Use when ARQ is evaluating whether a recovery path improved usable order.

### 8.3 Profile `VAL-QUANT-BOUNDARY`

For events inside a fixed trusted quantum boundary:

\[
V_{raw} = \alpha_{ord}\,\Delta S_{ord} + \beta\,U_{post} - \gamma\,C_{op} - \delta\,R_{inst} + \epsilon\,\Delta E_{use}.
\]

Use when Model `M5` is declared.

### 8.4 Profile `VAL-HYBRID`

For hybrid systems where both exploratory branching and restored order are meaningful:

\[
V_{raw} = \alpha_{exp}\,\Delta H_{exp} + \alpha_{ord}\,\Delta S_{ord} + \beta\,U_{post} - \gamma\,C_{op} - \delta\,R_{inst} + \epsilon\,\Delta E_{use}.
\]

This profile MUST justify why both `ΔH_exp` and `ΔS_ord` are simultaneously meaningful under the declared boundary.

---

## 9. Operational Inputs to Raw Valuation

A conformant implementation MUST define how each included term is estimated.

At minimum:

### 9.1 Exploration term

`ΔH_exp` SHOULD be derived from one of the following, depending on profile:

- state-distribution spread before / after event,
- branching diversity of planner state,
- retrieval-path optionality,
- bounded surprise expansion under declared model.

### 9.2 Order / coherence term

`ΔS_ord` SHOULD be derived from one of the following:

- decrease in local entropy estimate,
- decrease in prediction error variance,
- improved coherence / state-purity estimate,
- reduced internal fragmentation under the declared boundary.

### 9.3 Utility term

`U_post` MUST be task- or review-relative. It MAY be derived from:

- improved target closeness,
- reduced downstream loss,
- improved verified decision quality,
- improved future budget efficiency.

### 9.4 Cost term

`C_op` SHOULD aggregate normalized costs such as:

- energy use,
- elapsed latency,
- privilege consumption,
- irreversibility usage,
- storage / witness overhead.

### 9.5 Instability term

`R_inst` SHOULD reflect the chance that the post-event state is fragile, unsafe, incoherent, or likely to propagate destabilization.

### 9.6 Quantum term

`ΔE_use` MAY be included only if the usable-entanglement estimator is declared and the trusted boundary is explicit.

---

## 10. Anomaly Scoring — General Rule

ARQ anomaly scoring answers a different question from raw valuation.

Raw valuation asks:

> “Would this event be useful if we trusted it?”

Anomaly scoring asks:

> “How suspicious is this event under the currently declared epoch, controller, witness, and boundary assumptions?”

These two quantities MUST remain separate.

A conformant implementation SHALL support at least one of the following profiles:

1. **Operational anomaly score profile** — default and recommended;
2. **Bayesian anomaly profile** — optional and stricter.

---

## 11. Default Profile — Operational Anomaly Score

### 11.1 Status

This is the **default normative ARQ v0.2 anomaly profile**.

It is preferred unless the implementation can justify a full Bayesian model.

### 11.2 Canonical form

The operational anomaly score is:

\[
A_{anom} = \operatorname{clip}_{[0,1]}\!
\left(
\lambda_M s_M +
\lambda_C s_C +
\lambda_D s_D +
\lambda_W s_W +
\lambda_B s_B +
\lambda_Q s_Q
\right),
\]

where:

- `s_M ∈ [0,1]` = model-surprise signal,
- `s_C ∈ [0,1]` = controller-deviation signal,
- `s_D ∈ [0,1]` = drift / epoch-staleness signal,
- `s_W ∈ [0,1]` = witness-integrity weakness signal,
- `s_B ∈ [0,1]` = boundary-mismatch signal,
- `s_Q ∈ [0,1]` = self-similarity / anti-echo suspicion signal,
- `λ_i ≥ 0` are profile weights,
- and the weights SHOULD sum to `1`.

### 11.3 Signal meanings

A conformant implementation SHOULD interpret the component signals as follows.

#### `s_M` — model-surprise signal

High when the event is improbable under the declared baseline or exhibits unexpectedly large residuals.

#### `s_C` — controller-deviation signal

High when the realized controller action diverges from the attested or expected control path.

#### `s_D` — drift / epoch-staleness signal

High when the event occurs late in an epoch, under known drift accumulation, or near invalidation thresholds.

#### `s_W` — witness weakness signal

High when raw context, hashes, signatures, or reproducibility evidence are weak, delayed, partial, or missing.

#### `s_B` — boundary mismatch signal

High when the event appears to cross or depend on degrees of freedom outside the declared trusted boundary.

#### `s_Q` — self-similarity / anti-echo signal

High when the event is too similar to recent internally generated events without new external constraint, new witness evidence, or new boundary interaction.

### 11.4 Hard honesty rule

`A_anom` is a score, not a posterior probability.

A heuristic implementation MUST NOT label `A_anom` as `P_anom`.

### 11.5 Default band semantics

Recommended operational bands:

- `A_anom < 0.25` → ordinary,
- `0.25 ≤ A_anom < 0.50` → mildly suspicious,
- `0.50 ≤ A_anom < 0.75` → strongly suspicious,
- `A_anom ≥ 0.75` → quarantine or block candidate promotion unless a stronger review path exists.

These values are defaults only. Profile-specific bands MAY differ, but MUST be declared.

---

## 12. Optional Profile — Bayesian Anomaly Model

### 12.1 Status

This profile is OPTIONAL.

It SHALL be used only when the implementation can justify priors and likelihoods.

### 12.2 Hypotheses

The implementation MUST declare at least two competing hypotheses:

- `H_nom` — event generated by nominal dynamics under the declared baseline;
- `H_anom` — event generated by anomalous, adversarial, or assumption-violating dynamics.

### 12.3 Bayes factor

The Bayes factor is:

\[
B_{anom} = \frac{p(E \mid H_{anom})}{p(E \mid H_{nom})},
\]

where `E` is the declared evidence bundle.

### 12.4 Posterior probability

If prior probabilities `π_anom` and `π_nom` are declared, then the posterior anomaly probability is:

\[
P_{anom} =
\frac{\pi_{anom} B_{anom}}
{\pi_{anom} B_{anom} + \pi_{nom}}.
\]

Equivalently,

\[
P_{anom} =
\frac{\pi_{anom} p(E \mid H_{anom})}
{\pi_{anom} p(E \mid H_{anom}) + \pi_{nom} p(E \mid H_{nom})}.
\]

### 12.5 Use rule

A document or implementation MAY use `P_anom` only if:

1. the hypotheses are declared;
2. the evidence bundle is declared;
3. the priors are declared;
4. the likelihood model is declared;
5. the posterior computation is reproducible.

Without those, use `A_anom` instead.

---

## 13. Trust Weight Composition

### 13.1 Minimal default form

The default trust-weight formula is:

\[
\tau = A_{valid}\cdot(1-A_{anom}).
\]

Where:

- `A_valid = 1` if the event occurred inside a valid epoch and the required trust records verify;
- `A_valid = 0` otherwise.

Hence:

- invalid epoch or failed attestation forces `τ = 0`;
- perfect trust under the default profile gives `τ ≈ 1`.

### 13.2 Bayesian variant

If the Bayesian anomaly profile is used, the trust weight MAY instead be written:

\[
\tau = A_{valid}\cdot(1-P_{anom}).
\]

### 13.3 Additional attenuation factors

A profile MAY extend the trust rule with additional multiplicative factors, for example:

- `g_epoch` — staleness attenuation,
- `g_ctrl` — controller consistency attenuation,
- `g_wit` — witness completeness attenuation.

A more general form is therefore:

\[
\tau = A_{valid}\cdot g_{epoch}\cdot g_{ctrl}\cdot g_{wit}\cdot(1-A_{anom}),
\]

with each `g_i ∈ [0,1]`.

Any such extension MUST be declared explicitly.

### 13.4 Hard trust-floor rule

If `τ < τ_min`, privileged ARQ actions MUST be blocked.

At minimum, blocked actions SHALL include:

- candidate-to-authoritative promotion,
- high-cost anti-resonance intervention,
- oracle invocation under trust-sensitive profiles,
- irreversible state promotion.

---

## 14. Trust-Adjusted Value

### 14.1 Canonical form

The canonical trust-adjusted value is:

\[
V_{trust} = \tau\,V_{raw} - \lambda_{recal}(1-\tau)C_{recal} - \lambda_{echo}Q_{echo}.
\]

Where:

- `τ` = trust weight,
- `C_recal ≥ 0` = calibrated cost of recalibration / re-entry / trust restoration,
- `λ_recal ≥ 0` = weight of trust-loss penalty,
- `Q_echo ≥ 0` = anti-echo penalty term,
- `λ_echo ≥ 0` = weight of self-similarity / anti-echo penalty.

### 14.2 Interpretation

The formula expresses three ideas:

1. raw value counts only in proportion to trust;
2. questionable events carry a trust-restoration burden;
3. repeated self-similar internal events are discounted even if they look numerically promising.

### 14.3 Minimal anti-echo penalty

A default binary anti-echo penalty MAY be used:

\[
Q_{echo} = \mathbb{1}[Q_{selfsim}],
\]

where `Q_selfsim` is true when the event is classified as self-similar without sufficient external novelty.

A richer implementation MAY define:

\[
Q_{echo} = s_Q,
\]

using the self-similarity component from the anomaly profile.

### 14.4 Hard rule

A large positive `V_raw` MUST NOT override `τ = 0`.

If trust is invalid, the event cannot acquire ARQ authority by numerical magnitude alone.

---

## 15. Action-Band Semantics

### 15.1 Thresholds

This document uses the following thresholds:

- `V_suppress` — suppression threshold,
- `V_observe` — observation threshold,
- `V_candidate` — candidate-entry threshold,
- `V_high` — high-value threshold requiring stronger review or second signature.

All thresholds MUST declare whether they apply to `V_raw` or `V_trust`.

For ARQ v0.2, action recommendations SHOULD be computed from `V_trust`.

### 15.2 Recommended banding

A default action rule is:

\[
action =
\begin{cases}
\texttt{fail\_closed}, & \tau < \tau_{min} \\
\texttt{suppress}, & V_{trust} \le V_{suppress} \\
\texttt{log\_only}, & V_{suppress} < V_{trust} < V_{observe} \\
\texttt{observe}, & V_{observe} \le V_{trust} < V_{candidate} \\
\texttt{candidate}, & V_{trust} \ge V_{candidate} \text{ and no hard gate blocks}.
\end{cases}
\]

### 15.3 High-value rule

If `V_trust ≥ V_high`, the event MUST NOT be auto-promoted to authoritative memory.

Instead it MUST enter a stronger review path, which MAY include:

- second signature from `a`,
- extended review window,
- additional witness requirements,
- model challenge or replay.

### 15.4 No direct EA rule

This document outputs scoring bands and recommendation classes.

It does **not** authorize direct final EA status by itself.

`candidate` means score-admissible for further witnessed review, not already authoritative memory.

---

## 16. Calibration and Governance of Scoring Parameters

### 16.1 Parameters under governance

The following parameters are governance-sensitive and MUST NOT be changed unilaterally by `c` during an active epoch unless a profile explicitly allows bounded adaptation:

- valuation weights,
- anomaly weights,
- trust floor,
- action thresholds,
- anti-echo penalty weight,
- recalibration penalty weight.

### 16.2 Epoch freeze rule

Scoring parameters SHALL be frozen within an active epoch unless:

1. a policy explicitly allows bounded intra-epoch tuning; and
2. every such update is recorded as a witnessable parameter-change event.

### 16.3 A/B-slot update discipline

Parameter tuning SHALL use a dual-slot procedure:

- `Slot_A` = currently authoritative scoring policy;
- `Slot_B` = candidate policy under review.

The candidate policy in `Slot_B` MAY be evaluated in shadow mode, but SHALL NOT become authoritative unless review criteria pass.

### 16.4 Auto-rollback rule

If `Slot_B` produces any of the following during the review window:

- increased false-promotion rate,
- degraded witness completeness,
- unstable threshold oscillation,
- higher fail-closed incidence without compensating gain,
- unexplained anomaly inflation,

then the system MUST perform:

\[
Rollback(B \rightarrow A).
\]

### 16.5 Update direction constraint

Parameter changes SHOULD be bounded in step size.

A profile that allows adaptive updates MUST declare maximum step size per update or per epoch.

---

## 17. Anti-Echo and Repetition Discipline

### 17.1 Principle

A repetition of internally generated style, phrasing, or branching pattern is not automatically evidence of valuable exploration.

### 17.2 Required discipline

A conformant implementation SHOULD increase `s_Q` or apply `Q_echo` when all of the following are true:

1. the event is highly similar to recent internally generated events;
2. no new boundary interaction occurred;
3. no new witness evidence was introduced;
4. no measurable downstream improvement is present.

### 17.3 Externality escape rule

To escape anti-echo discounting, an event SHOULD demonstrate at least one of:

- new external constraint,
- new witness record,
- new measurable downstream effect,
- new boundary-crossing observation allowed by policy.

### 17.4 No style inflation

Narrative novelty, surface phrasing, or rhetorical elaboration MUST NOT by themselves reduce anomaly or increase promotability.

---

## 18. Minimum Score Record for Witnessing

Every scored event MUST produce or reference a witnessable score record containing at least:

```json
{
  "schema_version": "arq-val-0.2",
  "capsule_id": "string",
  "model_profile": "M1|M2|M3|M4|M5 or combination",
  "valuation_profile": "VAL-CLASSICAL-EXPLORE|VAL-CLASSICAL-ORDER|VAL-QUANT-BOUNDARY|VAL-HYBRID",
  "anomaly_profile": "OPER_SCORE|BAYES",
  "included_terms": ["dH_exp", "dS_ord", "U_post", "C_op", "R_inst", "dE_use"],
  "omitted_terms": ["..."],
  "raw_value": "number",
  "anomaly_score": "number or null",
  "bayes_factor": "number or null",
  "posterior_anom": "number or null",
  "trust_weight": "number",
  "trust_adjusted_value": "number",
  "thresholds": {
    "tau_min": "number",
    "V_suppress": "number",
    "V_observe": "number",
    "V_candidate": "number",
    "V_high": "number"
  },
  "recommended_action": "suppress|observe|log_only|candidate|fail_closed",
  "echo_quarantine": true,
  "record_hash": "string",
  "entity_sig": "string",
  "anchor_sig": "string or null"
}
```

If the Bayesian profile is used, priors and likelihood references MUST also be recorded or referenced.

---

## 19. Conformance Profiles

### 19.1 `ARQ-VAL-BASE`

Minimum conformance:

- one declared raw-valuation profile,
- one declared anomaly profile,
- trust weight `τ`,
- `V_trust` computation,
- witnessable score record.

### 19.2 `ARQ-VAL-TRUST`

Includes `ARQ-VAL-BASE` plus:

- epoch validity checks,
- trust floor,
- recalibration penalty,
- explicit block on privileged actions below `τ_min`.

### 19.3 `ARQ-VAL-BAYES`

Includes `ARQ-VAL-TRUST` plus:

- declared anomaly hypotheses,
- declared priors,
- reproducible likelihood model,
- posterior anomaly probability `P_anom`.

### 19.4 `ARQ-VAL-QUANT`

Includes `ARQ-VAL-TRUST` plus:

- declared trusted quantum boundary,
- declared usable-entanglement estimator,
- explicit use of `ΔS_ord` and/or `ΔE_use`.

---

## 20. Invariants

A conformant ARQ scoring implementation SHALL satisfy the following invariants.

1. **No trust-free authority**  
   If `τ = 0`, the event SHALL NOT gain privileged ARQ authority.

2. **No witness-free value**  
   Score output without witness record SHALL NOT be treated as promotion-capable.

3. **No silent posterior inflation**  
   A heuristic anomaly score SHALL NOT be renamed as probability.

4. **No anti-echo bypass by wording**  
   Stylistic novelty SHALL NOT reduce anomaly or increase promotion authority by itself.

5. **No threshold mutation by the evaluated event itself**  
   The event being scored SHALL NOT directly rewrite the thresholds used to score it.

6. **No candidate ≡ EA collapse**  
   Candidate status SHALL remain non-authoritative until the separate lifecycle rules are satisfied.

---

## 21. Bridges (Required)

### 21.1 Explicit bridge

ARQ valuation is the bridge between `c = a + b`, L4 budgets, and witnessed memory.  
`a` supplies policy and accountability, `b` supplies measurable transitions and controller traces, and ARQ scoring determines which deviations remain bounded signal rather than becoming unreviewed narrative. The result is not “an intelligent feeling about errors,” but a witnessed, budgeted path from deviation to candidate memory.

### 21.2 Hidden bridge #1 — Cybernetics / Ashby

A long-lived entity cannot be stabilized by one scalar alone. That is why ARQ separates value, anomaly, trust, budget, and witness instead of pretending one score can govern the whole system. The separation is not bureaucracy; it is requisite variety in the regulator.

### 21.3 Hidden bridge #2 — Information theory / Cover & Thomas

The score record is a compression layer. It reduces a large evidentiary event into a bounded set of numbers and references without claiming that the numbers are the whole reality. Good compression preserves decision-relevant structure; bad compression becomes self-deception. ARQ therefore requires hashes, omitted-term declarations, and explicit profile identifiers.

### 21.4 Hidden bridge #3 — SER / anti-oligarchy metabolism

Without trust discount and anti-echo penalties, entities would accumulate authority from repeated self-similar “interesting” deviations. The scoring layer therefore acts as a metabolic brake: novelty must survive cost, risk, trust, and witness, not merely excitement.

---

## 22. Earth Paragraph (Engineering / Anatomy)

In ordinary engineering this is the difference between a strange sensor spike and a real incident. A spike may be interesting, but nobody rewrites the maintenance manual because one graph looked dramatic at 03:17. You check calibration, controller logs, nearby interference, repeated patterns, and whether the machine actually behaved differently under load. Biology is similar: not every twitch is learning, not every fever is growth, and not every vivid feeling deserves memory authority. ARQ scoring exists so the system does not confuse stimulation with experience.

---

## 23. Closing Statement

ARQ v0.2 scoring is deliberately conservative.

It does not try to prove that a surprising event is meaningful. It asks a narrower and more honest question:

> Under a declared model, with declared budgets, under a declared trust boundary, how much authority should this deviation be allowed to acquire right now?

That is the correct scope.

A long-lived entity does not remain stable because it notices everything.  
It remains stable because it notices, discounts, logs, retries, suppresses, and only rarely remembers with authority.

