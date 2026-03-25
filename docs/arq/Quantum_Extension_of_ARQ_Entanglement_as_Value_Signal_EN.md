# Quantum Extension of ARQ: Entanglement as a Value Signal

**Technical Note**  
**Author:** Kotov Ivan  
**Place and date:** Bruxelles, 2026

---

## Abstract

This note extends ARQ into a quantum setting, where an error event is not evaluated only as damage, but as a state transition that may either destroy or create future computational value. The central idea is to distinguish between **destructive entanglement** with an uncontrolled environment and **constructive entanglement** with trusted ancillas that remain inside the controllable boundary of the system. The valuation function is therefore enriched with a term that measures the change in **usable entanglement**, allowing some apparent errors to be reclassified as valuable experience artifacts rather than pure loss.

The bridge is simple but important: in classical ARQ, a deviation is judged by what it costs and what it teaches; in the quantum extension, that judgment must also account for whether the deviation creates recoverable quantum correlation.

---

## 1. State Representation

Let the entity $c$ be associated with a density matrix $\rho$ over a composite Hilbert space

$$
\mathcal{H} = \mathcal{H}_S \otimes \mathcal{H}_E,
$$

where:

- $\mathcal{H}_S$ is the system of interest, such as a quantum memory or cognitive register;
- $\mathcal{H}_E$ is the environment, including noise sources, measurement apparatus, and ancillas outside the trusted control boundary.

In quantum error correction, a pure state is fragile and a mixed state carries uncertainty. ARQ interprets an error event as a transition

$$
\rho_{\mathrm{pre}} \longrightarrow \rho_{\mathrm{post}}.
$$

The event is not judged only by immediate fidelity loss. It is judged by what kind of correlation structure exists after the transition, and whether that structure can still be used.

---

## 2. Entanglement as a Resource

The von Neumann entropy of the reduced system state measures how strongly the system is correlated with the rest of the world:

$$
S(\rho_S) = -\operatorname{Tr}(\rho_S \log \rho_S),
\qquad
\rho_S = \operatorname{Tr}_E(\rho).
$$

Low $S(\rho_S)$ indicates a state close to purity, hence high coherence and stronger potential for quantum advantage. High $S(\rho_S)$ indicates stronger entanglement with external degrees of freedom and usually signals decoherence.

But not all entanglement is harmful.

### Destructive entanglement

Entanglement is **destructive** when it binds the system to an uncontrolled environment and cannot be later harnessed. In that case, the system loses coherent agency without gaining a recoverable computational path.

### Constructive entanglement

Entanglement is **constructive** when it involves trusted ancillas or controllable subsystems that remain within the operational boundary of the entity. In that case, what first appears to be an error may actually open a new path for teleportation, syndrome extraction, measurement-based computation, or future inference.

The distinction is therefore not metaphysical but operational: the same physical correlation can be either loss or resource depending on whether the correlated degrees of freedom remain under control.

---

## 3. Measuring Error Value via Entanglement

We extend the ARQ value function with a term that captures the change in usable entanglement:

$$
V = \alpha \, \Delta S
  + \beta \, U(\rho_{\mathrm{post}})
  - \gamma \, C
  - \delta \, R
  + \varepsilon \, \Delta E_{\mathrm{usable}}.
$$

Here,

$$
\Delta E_{\mathrm{usable}}
= E_{\mathrm{usable}}(\rho_{\mathrm{post}})
- E_{\mathrm{usable}}(\rho_{\mathrm{pre}}),
$$

and we define

$$
\Delta S = S\!\left(\rho_S^{\mathrm{pre}}\right) - S\!\left(\rho_S^{\mathrm{post}}\right).
$$

With this sign convention, $\Delta S > 0$ means the system became more ordered or more coherent, while $\Delta S < 0$ means local entropy increased.

A suitable entanglement monotone for $E_{\mathrm{usable}}$ may be:

- **Negativity** for bipartite systems:

$$
\mathcal{N}(\rho) = \frac{\left\|\rho^{T_B}\right\|_1 - 1}{2};
$$

- **Logarithmic negativity**:

$$
E_N(\rho) = \log_2 \left\|\rho^{T_B}\right\|_1.
$$

For multipartite systems, one may instead use tangle, robustness, or a geometric entanglement measure.

### Interpretation

- If an event increases $E_{\mathrm{usable}}$, for example by creating a Bell pair with a trusted ancilla, the event may be valuable even when local entropy rises.
- If an event only increases uncontrolled entanglement with the environment, then $E_{\mathrm{usable}}$ stays unchanged or decreases, and the event is destructive.

This lets ARQ avoid a crude rule such as “all errors are bad.” In a quantum setting, some deviations are expensive noise, while others are accidental discoveries.

---

## 4. Practical Computation of $E_{\mathrm{usable}}$

Assume the quantum entity has a known set of trusted ancillas $\mathcal{A}_{\mathrm{trusted}}$. Then a practical definition is

$$
E_{\mathrm{usable}}(\rho)
=
\max_{A \subseteq \mathcal{A}_{\mathrm{trusted}}}
\mathcal{N}\!\left(\rho_{S A}\right),
$$

where $\rho_{SA}$ is the reduced state over the system together with a chosen subset of trusted ancillas. The maximisation over subsets captures the best quantum advantage that can still be extracted from the controlled part of the architecture.

In practice, full tomography may be too expensive, so one often uses approximations:

- concurrence on selected qubit pairs,
- fidelity with Bell states,
- witness operators tailored to the expected circuit family,
- compressed sensing or shadow tomography for larger systems.

This is already a hidden control-theoretic boundary: the valuation depends not on abstract entanglement alone, but on which subsystems remain reachable, calibratable, and economically measurable.

---

## 5. Anti-Resonance in Quantum Systems

Anti-resonance pulses, including dynamical decoupling schemes, aim to disentangle the system from the uncontrolled environment without destroying constructive entanglement inside the trusted set.

If a pulse sequence is represented by a unitary $U_{\mathrm{pulse}}$, then

$$
\rho_{\mathrm{after}}
=
U_{\mathrm{pulse}}\, \rho_{\mathrm{before}}\, U_{\mathrm{pulse}}^{\dagger}.
$$

The optimisation target is not simply to minimise entropy at any cost. The real objective is

$$
\text{minimise } S(\rho_S)
\qquad \text{while preserving or increasing} \qquad
E_{\mathrm{usable}}.
$$

This becomes a constrained offline optimisation problem for a known noise model, device topology, and trusted-ancilla map. In other words, the pulse sequence should cut the bad correlations and spare the good ones.

---

## 6. Example: Bell Pair Creation as a Valuable Error

Suppose the pre-event state is a product state

$$
\rho_{\mathrm{pre}} = |0\rangle\langle 0| \otimes \sigma_{\mathrm{ancilla}},
$$

and an accidental cross-resonance interaction turns it into

$$
\rho_{\mathrm{post}} = |\Phi^+\rangle\langle \Phi^+|,
$$

where $|\Phi^+\rangle$ is a Bell state between the system qubit and a trusted ancilla.

Then:

- the reduced system entropy increases from $0$ to $1$ bit, so $\Delta S < 0$ under the convention above;
- the total state is still pure, but the local subsystem is now maximally entangled with a trusted resource partner;
- $E_{\mathrm{usable}}$ jumps from $0$ to $1$ when logarithmic negativity is used;
- if the Bell pair is later consumed for teleportation, entanglement swapping, or superdense coding, then $U(\rho_{\mathrm{post}})$ is high.

Hence the overall value

$$
V = \alpha \Delta S + \beta U(\rho_{\mathrm{post}}) - \gamma C - \delta R + \varepsilon \Delta E_{\mathrm{usable}}
$$

can still become positive. Under that condition, the event is promoted from “mere error” to an **Experience Artifact**: something the entity should remember, replay, and stabilise deliberately next time.

---

## 7. Security and Witnessing

Every quantum error event that changes $E_{\mathrm{usable}}$ should be recorded in a tamper-evident witness trail. The log should include at least:

1. pre- and post-event state estimates, obtained through tomography, shadows, or compressed sensing;
2. the pulse sequence or recovery operation that was applied, if any;
3. the computed value of $E_{\mathrm{usable}}$ before and after the event;
4. the valuation output $V$ together with the chosen coefficients and device assumptions;
5. signatures or attestation artifacts from a trusted execution boundary, when the quantum hardware exposes such a feature.

This gives the theory an audit spine. A “valuable error” cannot remain a mystical claim; it must be replayable, challengeable, and attributable.

---

## 8. Operational Grounding

Real hardware is rude, and that is healthy.

On NISQ devices, state tomography scales badly, calibration drifts, pulse schedules leak into each other, and the line between trusted ancilla and environment may move with temperature, crosstalk, or firmware updates. Because of that, $E_{\mathrm{usable}}$ should be treated as a bounded engineering estimate rather than a divine quantity. The physically relevant question is not “is there entanglement somewhere?” but “can this exact hardware stack reproduce, verify, and exploit it before noise, time, and cost erase the advantage?”

That grounding matters for ARQ. A correlation that exists only on paper has little value. A correlation that survives measurement budget, control latency, and verification cost is another story entirely.

---

## Closing Note

The quantum extension of ARQ reframes error valuation from a purely destructive model into a resource-aware one. In this view, an error is not judged only by deviation from the intended path, but by whether it damages recoverable structure or accidentally creates it. Entanglement becomes a value signal precisely when it remains inside a controlled and witnessable boundary.
