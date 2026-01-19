# SER-FED — Federation Extension (Draft RFC)

**Scope:** Evolutionary stability & anti-oligarchy for long-lived ecosystems  
**Layer:** L2 (Federation Dynamics) + L4 (Reality Boundary)  
**Status:** Draft / RFC (not a release)

SER-FED is a **federation-layer extension** to the SER ecosystem.  
It does **not** replace SER v1.3.0 and must not modify the SER core specification.

---

## What SER-FED does

- introduces **metabolic authority** (authority is rented from reality, not owned)
- applies **inequality-driven experience decay** (Gini-based decay)
- enforces an **exploration budget** for cold-start and stagnation (Jester protocol)
- adds **prediction bonds** (liability attached to authority)
- defines an **L4 witness protocol** (triangulated reality verification)
- hardens the system against **sybil / farm capture** at the federation edge

---

## Non-goals

- individual cognition design (handled by SER core)
- model training or federated learning mechanics (handled by LA pipelines elsewhere)
- “ethical alignment” as a substitute for L4 constraints

---

## Relationship to EWCEP

EWCEP defines **how experience accumulates** across entities.  
SER-FED defines **how authority decays and renews** under L4 selection pressure.

Together they form a closed loop:
Experience → Authority → Reality → Decay → Renewal

---

## Design Assumptions

SER-FED is defined under explicit **failure-mode assumptions**.  
These assumptions are normative and documented in:

- **ASSUMED_FAILURE_MODES.md**

They motivate the protocol design but do **not** define execution logic.

SER-FED assumes that:
- authority concentration is a default outcome without decay,
- collusion and experience laundering are expected behaviors,
- speed dominance and externalized risk are structurally inevitable,
- long-lived systems must be stabilized architecturally, not morally.

---

## Specification Status

This directory contains multiple RFC drafts.

- **SER-FED_v0.1_RFC_EN.md**  
  Initial federation draft.

- **SER-FED_v0.2_RFC_EN.md** *(current)*  
  Canonical draft introducing:
  - normative L4 Witness lifecycle,
  - unified Impact Attribution → EA → Prediction Bonds chain,
  - explicit anti-oligarchy causality.

Readers should start with **v0.2** unless reviewing historical evolution.

---

## Status

SER-FED is a **Draft RFC**.

Its purpose is to:
- define architectural primitives,
- surface systemic assumptions,
- invite adversarial review.

It is intentionally incomplete at the implementation level.


