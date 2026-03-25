# Bounded Entropy Accumulation in ARQ Entities

**Author:** Kotov Ivan  
**Place and year:** Bruxelles, 2026

---

## 1. Setting and Assumptions

Consider a persistent entity `c` whose state is described by a probability distribution (classical) or density matrix (quantum) with entropy $H(t)$ at time $t$.

The entity operates under:

- **L4 budgets:** explicit upper bounds on energy consumption $E_{\max}$, time windows $\tau_{\max}$, and irreversible actions $I_{\max}$ per cycle.
- **ARQ protocol:** errors are either suppressed (anti-resonance) or, if retained, converted into Experience Artifacts (EA). Each EA is stored in permanent memory but incurs a fixed cost.
- **Fail-closed behavior:** if any budget is exhausted, the entity halts further processing and only maintains a safe persistent state.

We prove that $H(t)$ cannot grow without bound.

## 2. Physical Constraints: Energy and Irreversibility

Landauer's principle establishes a minimum energy cost for erasing one bit of information: $k_B T \ln 2$ in classical systems, with analogous thermodynamic constraints in quantum systems. Conversely, creating information (increasing entropy) does not itself require energy. However, **retaining** that increase in persistent form does require energy and resources such as memory, cooling, and error correction.

ARQ imposes explicit energy budgets: the entity cannot allocate infinite energy to sustain ever-growing entropy.

### Lemma 1 (Energy-Entropy bound)

For any finite time interval $[0,T]$, the total increase in entropy that can be retained (that is, not suppressed) is bounded by the total available energy budget $E_{\mathrm{total}}$ divided by the minimum cost per unit of entropy retention:

$$
\Delta H_{\mathrm{retained}}(T) \le \frac{E_{\mathrm{total}}}{k_B T \ln 2}
\qquad \text{(classical)}
$$

In the quantum case, similar bounds apply via the thermodynamic cost of maintaining coherence, for example cooling required to preserve a low-entropy state.

## 3. ARQ's Active Suppression Mechanism

ARQ suppresses destructive errors before they can irreversibly increase entropy. For each error event, the anti-resonance pulse consumes a fixed energy budget $\varepsilon_{\mathrm{pulse}}$. If the error is classified as destructive, the system returns to a state with entropy not exceeding the pre-error level, up to measurement uncertainty.

### Lemma 2 (Suppression prevents unbounded growth)

Let $H_{\max}$ be the maximum entropy the entity can sustain given its cooling and error-correction resources. Each destructive error, if unsuppressed, would increase entropy by $\delta H_{\mathrm{destruct}} > 0$. By applying suppression, the entity prevents that increase. The number of suppression events is limited by the energy budget for pulses:

$$
N_{\mathrm{suppress}} \le \frac{E_{\mathrm{pulse,budget}}}{\varepsilon_{\mathrm{pulse}}}
$$

Thus the cumulative entropy increase from unsuppressed destructive errors is bounded.

## 4. Experience Artifacts and Entropy Cap

Even when an error is promoted to an EA because it is exploratory and valuable, the resulting state is not free to increase entropy indefinitely. Each EA is stored in a structured memory with a fixed cost in terms of energy and space. Moreover, the entity's memory capacity is finite, bounded by available hardware. Once memory is full, either old EAs must be compressed, reducing their entropy, or new ones cannot be created.

### Lemma 3 (Finite memory bounds retained entropy)

Let $M$ be the total number of bits available for persistent memory, including EAs. Then the total retained entropy is at most $\log_2 M$ if memory is used optimally, or a similar bound in quantum systems via the Holevo bound:

$$
H_{\mathrm{retained}} \le \log_2 M
\qquad \text{(classical)}
$$

In practice, memory is finite, so entropy cannot exceed this fundamental limit.

## 5. Time-Averaged Entropy Production

Even if short-term entropy fluctuations occur, long-term averages are bounded by the system's ability to dissipate entropy to the environment. The entity's environment, including cooling and heat sinks, has a finite capacity to absorb entropy per unit time. ARQ respects this by throttling processing when thermal budgets are near their limits.

### Theorem (Boundedness)

For an ARQ-compliant entity with finite energy, memory, and cooling budgets, the entropy $H(t)$ remains bounded for all $t$:

$$
\sup_{t \ge 0} H(t) \le H_{\max} < \infty
$$

where $H_{\max}$ depends only on the hardware resources and the configured budgets, not on the operational duration.

### Proof sketch

Assume the contrary: that $H(t)$ is unbounded. Then there exists a sequence of times such that $H(t) \to \infty$. This would require at least one of the following:

1. An infinite number of retained errors (EA creations), but memory is finite - contradiction.
2. An infinite number of unsuppressed destructive errors, but each such error draws from a finite energy pulse budget - contradiction.
3. Unbounded increase in entropy without resource consumption, which contradicts the fact that the system cannot retain that entropy without paying a cost in energy and memory.

Hence the assumption is false. $\square$

## 6. Concrete Bound Example

Suppose:

- Energy budget for anti-resonance: $E_{\mathrm{pulse}} = 10^6 k_B T$ (enough for $10^6$ pulses at the Landauer limit).
- Memory capacity $M = 10^{12}$ bits.
- Maximum entropy per EA: $\log_2 M \approx 40$ bits per EA if perfectly random.

Even if every pulse prevented an entropy increase of $1$ bit, total preventable entropy is approximately $10^6$ bits.

Total retained entropy cannot exceed approximately $40$ bits times the number of EAs. Once memory is full, no more EAs can be stored.

Thus:

$$
H_{\max} \approx 40 \times M_{\mathrm{EA}} + \text{baseline entropy}
$$

which is finite.

## 7. Implications for ARQ Design

- **Budget enforcement is crucial:** if energy or memory budgets are not enforced, the bounds vanish.
- **Fail-closed behavior matters:** when budgets are exhausted, the entity stops and does not continue to accumulate entropy in an uncontrolled way.
- **The bound is independent of runtime:** no matter how long the entity operates, its internal disorder cannot grow beyond hardware limits.

This result is essential for the long-term stability of sovereign entities. It shows that runaway entropy growth cannot occur under continuous operation as long as the architectural constraints remain enforced.
