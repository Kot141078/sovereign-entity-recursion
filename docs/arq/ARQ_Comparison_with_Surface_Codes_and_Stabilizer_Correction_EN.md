# ARQ — Comparison with Surface Codes and Stabilizer Correction

**Author:** Kotov Ivan  
**Year:** 2026  
**Place:** Bruxelles

---

## Purpose of this note

This note explains how ARQ relates to conventional quantum error correction, especially stabilizer codes and surface-code practice.

The point is not to reject those methods. The point is to clarify the architectural layer in which ARQ operates.

Standard quantum error correction protects a target state. ARQ extends that logic for long-lived entities that must remain stable, witnessable, and capable of retaining certain valuable deviations as experience.

---

## What standard quantum error correction does well

Stabilizer codes, CSS constructions, and surface codes were developed to preserve quantum information in the presence of noise.

Their strengths are clear:

- they detect deviations through syndrome measurements,
- they define a recovery path back toward the intended logical state,
- they support threshold reasoning under explicit physical assumptions,
- they are grounded in real device constraints rather than vague metaphors.

For preserving a target state, this is the right starting point.

---

## Where ARQ differs

ARQ does not replace stabilizer logic or surface-code machinery.

ARQ adds a higher-layer decision problem:

- which deviations are purely destructive,
- which deviations are merely neutral,
- and which rare deviations should be preserved as valuable experience under bounded conditions.

In ordinary QEC, the error is something to remove.
In ARQ, the error is first classified.

That classification is not mystical. It is bounded by energy, time, memory, privilege, and witness requirements.

---

## Comparison at a glance

| Dimension | Stabilizer / Surface-code logic | ARQ |
|---|---|---|
| Primary goal | Preserve logical state | Preserve continuity of a long-lived entity under bounded evolution |
| Treatment of error | Error is harmful by default | Error is classified as destructive, neutral, or exploratory |
| Memory of the event | Usually discarded after correction | May be retained as an Experience Artifact if justified |
| Trust model | Hardware/controller often assumed | Trust is explicit: attestation, signed controller state, witness chain |
| Constraint model | Physical thresholds and correction overhead | L4 budgets: energy, time, privilege, irreversibility, auditability |
| Accountability | Not a central design axis | Mandatory for any promoted event |
| Role in architecture | Physical/logical correction layer | Architectural bridge between correction, memory, and bounded agency |

---

## Why this bridge matters

ARQ is an explicit bridge between three bodies of work:

1. quantum and classical correction logic,
2. SER continuity and Experience Artifact memory,
3. the L4 reality-bound layer.

Without that bridge, a system can correct errors but remain architecturally blind.
It can stay coherent in the narrow technical sense while still failing to distinguish noise from meaningful deviation, or novelty from manipulation.

That is why ARQ belongs above raw correction and below long-term memory policy.

---

## Hidden bridge 1: witness-first accountability

A corrected event and a promoted event are not equivalent.

If an event is promoted into durable memory, it must be attributable and replayable.
That requirement brings ARQ into alignment with witness-first architecture:
tamper-evident logs, signed state transitions, and challengeable history.

No value without witness.

---

## Hidden bridge 2: bounded homeostasis

ARQ is closer to homeostasis than to a retry loop.

A living system does not react to every perturbation by infinite correction.
It filters, suppresses, integrates, or stops.

ARQ applies the same engineering principle:
bounded adaptation under explicit limits.

That makes it compatible with long-lived systems that must remain stable over time instead of merely passing a short benchmark window.

---

## Grounding note

On real hardware, none of this stays abstract for long.

A board has finite thermal headroom.
A controller has finite timing slack.
Storage has finite write endurance.
Privilege cannot be infinite without turning every anomaly into a security hole.
And once calibration drifts beyond the trusted boundary, the safest move is not “be more creative” but “reduce authority, stop promotion, and re-establish trust.”

That is the real difference in tone.
Surface codes and stabilizer logic already respect physics.
ARQ keeps that respect, but carries it upward into memory, provenance, and bounded continuity.

---

## Conclusion

ARQ should be read as an architectural extension, not a competitor to standard quantum error correction.

Surface codes and stabilizer correction answer:
“How do we preserve the intended state?”

ARQ adds:
“What do we do with the deviation, once preserving continuity requires judgment rather than blind correction?”

For long-lived sovereign entities, that extra question is not optional.
It is the point at which correction becomes governance.
