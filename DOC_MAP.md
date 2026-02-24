# DOC_MAP — Reading Order & Canonical Map (SER ecosystem)

This repository is a protocol stack around `c = a + b`:
- **SER**: intra-entity stability & responsibility (L4-anchored existence)
- **EWCEP**: experience-weighted plural co-evolution
- **SER-FED**: federation layer (anti-oligarchy, bounded authority, decay)
- **L3+**: social integration overlay (collective anchoring + friction), above Legal L3, below L4

The goal of this file is **navigation**: what to read, in what order, and what each document is responsible for.

---

## 1) Start here (fast overview)

1. `README.md`  
   Entry point, repository framing.

2. `ECOSYSTEM.md`  
   Canonical ecosystem map (roles, layers, and the critical EA vs LA terminology split).

3. `pdf/ECOSYSTEM_EN.pdf` (snapshot)  
   Citable distribution copy of the ecosystem overview.

---

## 2) Canonical protocol sources (normative Markdown)

### 2.1 SER (intra-entity stability)
- `protocol/ser/SER_v1.3_EN.md`
- `protocol/ser/SER_v1.3_RU.md` (if present)

**Responsibility:** what it means for an entity to exist as a stable, accountable, reality-bounded system (L4 anchoring, emergency modes, internal topology).

### 2.2 EWCEP (plural co-evolution)
- `protocol/ewcep/README.md` (and subfiles)
- `protocol/ewcep/EWCEP_v0.1_en.md` (if present)

**Responsibility:** experience-weighted co-evolution dynamics across many entities (plural stability, incentives, drift resistance).

### 2.3 SER-FED (federation layer)
- `protocol/ser-fed/README.md`
- `protocol/ser-fed/SER-FED_v0.1_RFC_EN.md` (if present)
- `protocol/ser-fed/SER-FED_v0.2_RFC_EN.md` (if present)
- `protocol/ser-fed/CHANGELOG.md`

**Responsibility:** anti-oligarchy mechanics at federation scale:
authority bounds, decay, jester forcing, prediction bonds, L4 witness lifecycle, and rules for authority updates.

### 2.4 L3+ (social integration overlay)
- `protocol/l3-plus/L3_PLUS_SOCIAL_INTEGRATION_DRAFT_RFC.md`
- `protocol/l3-plus/README.md`

**Responsibility:** social friction and collective anchoring mechanisms.
L3+ acts through federation governance (Arbiter mechanisms) and never overrides L4.

### 2.5 VXCX (visual experience capsule exchange)
- `protocol/vxcx/README.md`
- `protocol/vxcx/VXCX_v0.1_Normative_Draft_EN.md`
**Responsibility:** privacy-first exchange of visual experience capsules (no pixels by default),
bounded payload, explicit uncertainty, witness events for auditability.

---

## 3) PDF snapshots (distribution / citation)

PDFs are *snapshots* of the canonical Markdown sources (for citation and external review):

- `pdf/SER_v1.3_EN.pdf`
- `pdf/SER_v1.3_RU.pdf`
- `pdf/EWCEP_v0.1.en.pdf`
- `pdf/SER-FED_v0.1_RFC_EN.pdf`
- `pdf/SER-FED_v0.2_RFC_EN.pdf`
- `pdf/L3_PLUS_SOCIAL_INTEGRATION_DRAFT_RFC.pdf`

---

## 4) Critical terminology (do not mix)

This ecosystem uses **two distinct objects** that must not be conflated:

- **EA — Experience Artifact**  
  A responsibility-bearing, L4-grounded artifact used for attribution / authority / accountability.
  EA is tied to lived outcomes and verification flows (e.g., witness + resolution note).

- **LA — Learning Abstract**  
  A learning signal (gradients, updates, DP sketches, aggregated learning signals).
  LA improves models but does not grant authority.

**Rule:** SR (Social Resonance, L3+) is also **not** EA and **not** LA.
SR is a social-layer signal used for friction / gating / decay at federation layer.

---

## 5) Role separation (system design)

- **Entity**: stateful identity + memory + responsibility (anchored in physical reality)
- **Arbiter/Federation**: governance and authority update rules (not identity owner)
- **Oracle**: stateless compute (no identity, no authority, no EA minting)

---

## 6) Bridges

**Explicit bridge:** `c = a + b` → role separation (Entity/Arbiter/Oracle) and collective anchoring (L3+).  
**Hidden bridge #1 (Cybernetics / Ashby):** external regulators (federation + L3+ friction) increase requisite variety beyond model-internal alignment.  
**Hidden bridge #2 (Information theory):** EA/LA/SR separation keeps authority/trust channels distinct from learning channels (different bandwidth, privacy, and attack surfaces).

---

## 7) Earth paragraph (grounding)

This stack behaves like industrial change control:
- a proposal is a ticket,
- evidence is a log,
- approval is a signed change record,
- and rollback exists.

An entity can be technically correct and still destabilize the social system.
L3+ adds friction and pause windows without pretending the system has “virtue”.
Reality remains the final reviewer (L4).
