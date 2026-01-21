# 03_L4_WITNESS_FIELDS.md
# L4 Witness — Record Fields & Lifecycle (Normative)
Status: Normative
Version: 0.1
Scope: SER-FED / L4 Impact Attribution binding
Language: RFC 2119 keywords (MUST/SHOULD/MAY)

---

## 0. Purpose

L4 Witness binds:
- claims and decisions,
- observable outcomes under L4 constraints,
- and authority/attribution consequences,

to signed, replayable, privacy-aware records.

This file defines the minimal required fields and lifecycle for:
1) Claim Envelope (CE)
2) Observation Packet (OP)
3) Challenge Record (CR)
4) Resolution Note (RN)

---

## 1. Normative Keywords

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" are to be interpreted
as described in RFC 2119.

---

## 2. Design Principles (Normative)

### 2.1 L4 Primacy
L4 Witness outcomes MUST reflect non-negotiable constraints (L4).
No record type may override L4 feasibility.

### 2.2 Post-factum Value
Attribution/weight MUST NOT be issued at creation time.
It MAY be issued only after real-world application and resolution.

### 2.3 Non-Market Constraint
Records MUST NOT implement bidding, ranking of humans, or competitive pressure.
Attribution is a consequence, not an incentive.

### 2.4 Responsibility Boundary
Records MUST preserve:
- the acting human anchor ("a") remains responsible for decisions,
- the entity does not issue commands and does not override human agency.

### 2.5 Evidence as Hashes
Records MUST carry:
- hashes and minimal metadata,
- not raw personal narratives.
Raw evidence MAY exist off-record (private channels), referenced by hashes.

---

## 3. Common Data Model (Normative)

### 3.1 Canonical Serialization
All records MUST define a `canonical_payload`:
- JSON (UTF-8)
- deterministic key ordering
- no floating-point where ambiguity exists
- timestamps in ISO 8601 UTC

Each record MUST include:
- `payload_hash` = HASH(canonical_payload)
- `record_sig`  = SIGN(payload_hash, issuer_private_key)

Hash algorithm MUST be declared (e.g., sha256).
Signature algorithm MUST be declared (e.g., ed25519).
(Algorithms are pluggable; the fields are mandatory.)

### 3.2 Identifiers
- `record_id` MUST be globally unique (UUIDv4 or equivalent).
- `ce_id` MUST be stable for the lifecycle of a claim.

### 3.3 Time Windows
Each CE MUST declare a witness window:
- `window_open_at`
- `window_close_at`

OP/CR submissions MUST fall within the window unless explicitly marked as:
- `late_submission=true` (allowed, but MUST be justified)
Late submissions MAY be ignored by arbiters.

### 3.4 Roles
- **Issuer**: entity node issuing CE (and optionally co-signed by human anchor).
- **Observer**: a witness submitting OP.
- **Challenger**: a participant submitting CR (optionally bonded).
- **Arbiter Quorum**: federation group issuing RN.

### 3.5 Privacy Classes
Every evidence reference MUST include a privacy class:
- `PUBLIC`: publishable without harm
- `RESTRICTED`: shareable to eligible arbiters/witnesses
- `PRIVATE`: never shared; hash only (existence proof)

---

## 4. Record Types (Normative Schemas)

### 4.1 Common Fields (All Records)
REQUIRED fields:
- `schema_version` (string, e.g. "0.1")
- `record_type` (enum: "CE" | "OP" | "CR" | "RN")
- `record_id` (string)
- `created_at` (ISO 8601 UTC)
- `issuer` object:
  - `entity_id` (string)
  - `key_id` (string, public key identifier)
  - `role` (enum: "ENTITY" | "ANCHOR" | "WITNESS" | "CHALLENGER" | "ARBITER")
- `hash_alg` (string)
- `sig_alg` (string)
- `payload_hash` (string)
- `record_sig` (string)

OPTIONAL fields:
- `co_signatures` (list of signatures, for anchor co-signing or quorum signing)
- `prev_record_hash` (string, to chain records if desired)
- `notes_redacted` (boolean)

---

## 4.2 Claim Envelope (CE)

### 4.2.1 Purpose
A CE is a bounded, testable claim about an action/outcome under L4 constraints.

### 4.2.2 Required Fields (CE payload)
- `ce_id` (string; stable claim id)
- `claim` object:
  - `title` (string; short)
  - `statement` (string; testable, non-poetic)
  - `domain` (string; e.g., "safety", "ops", "med", "infra", "finance", etc.)
  - `impact_class` (enum: "LOW" | "MEDIUM" | "HIGH")
- `context` object:
  - `l4_factors` (list of enums, at least one):
    - "PHYSICAL" | "ECONOMIC" | "SOCIAL" | "POLITICAL" | "BIOLOGICAL" | "INFRASTRUCTURE"
  - `constraints` (list of strings; context constraints)
  - `uncertainty_markers` (list of strings; explicit uncertainty)
- `action_plan` object:
  - `what_was_done` (string; minimal description)
  - `what_counts_as_success` (string; measurable criteria)
  - `what_counts_as_failure` (string; measurable criteria)
- `witness_window` object:
  - `window_open_at` (ISO 8601 UTC)
  - `window_close_at` (ISO 8601 UTC)
- `evidence_commitments` (list of evidence refs; OPTIONAL but RECOMMENDED):
  - `type` (enum: "TELEMETRY" | "DOC" | "PHOTO" | "VIDEO" | "RECEIPT" | "SENSOR" | "LOG" | "OTHER")
  - `hash` (string)
  - `privacy_class` (enum)
  - `uri` (string; OPTIONAL)
  - `redaction` (string; OPTIONAL)

### 4.2.3 Anchor Co-sign (RECOMMENDED)
If human anchor co-signing exists:
- CE MUST include a co-signature entry with `role="ANCHOR"`.

---

## 4.3 Observation Packet (OP)

### 4.3.1 Purpose
OP reports observed outcomes, with hash-bound evidence.

### 4.3.2 Required Fields (OP payload)
- `op_id` (string)
- `ce_ref` (string; ce_id)
- `observation` object:
  - `observed_at` (ISO 8601 UTC)
  - `observed_window` (object OPTIONAL):
    - `start_at` (ISO 8601 UTC)
    - `end_at` (ISO 8601 UTC)
  - `outcome_summary` (string; factual)
  - `metrics` (object OPTIONAL; key→value as strings)
  - `l4_signals` (list of strings; e.g., "cost_spike", "downtime", "thermal_throttle", "trust_drop")
- `evidence_refs` (list; at least one RECOMMENDED for non-trivial outcomes):
  - `type`, `hash`, `privacy_class`, `uri?`, `redaction?`
- `observer` object:
  - `observer_id` (string)
  - `observer_role` (enum: "ANCHOR" | "WITNESS" | "ARBITER" | "SYSTEM")
  - `diversity_tag` (string OPTIONAL; e.g., "independent", "same_org", "telemetry_only")

### 4.3.3 Integrity
OP MUST NOT embed raw personal narratives if privacy_class is RESTRICTED/PRIVATE.
Use hashes + minimal summaries.

---

## 4.4 Challenge Record (CR)

### 4.4.1 Purpose
CR opens an adversarial path: contradiction claims, missing evidence, scope abuse.

### 4.4.2 Required Fields (CR payload)
- `cr_id` (string)
- `ce_ref` (string; ce_id)
- `challenge` object:
  - `reason_code` (enum):
    - "CONTRADICTION"
    - "INSUFFICIENT_EVIDENCE"
    - "SCOPE_MISMATCH"
    - "EVIDENCE_TAMPERING_SUSPECTED"
    - "L4_FACTOR_IGNORED"
    - "OTHER"
  - `reason_text` (string; concise)
  - `op_refs` (list of op_id; OPTIONAL)
  - `requested_action` (enum):
    - "REQUEST_MORE_OP"
    - "REQUEST_ARB_REVIEW"
    - "REQUEST_EXTEND_WINDOW"
    - "REQUEST_CLASSIFY_HIGH_IMPACT"
- `bond` object OPTIONAL (but REQUIRED if escalation policy demands it):
  - `bond_type` (enum: "CHALLENGE_BOND" | "PREDICTION_BOND_REF")
  - `bond_ref` (string)
  - `bond_amount` (string)
  - `bond_currency` (string)

### 4.4.3 Anti-Abuse
CR submissions MAY be rate-limited by federation policy.
CRs without minimally coherent reason MUST be ignored.

---

## 4.5 Resolution Note (RN)

### 4.5.1 Purpose
RN is the only binding output: it freezes/updates authority and mints (or denies) attribution.

### 4.5.2 Required Fields (RN payload)
- `rn_id` (string)
- `ce_ref` (string; ce_id)
- `resolution` object:
  - `outcome` (enum):
    - "CONFIRMED"
    - "PARTIALLY_CONFIRMED"
    - "UNCONFIRMED"
    - "REFUTED"
  - `scope` (string; what exactly was confirmed/refuted)
  - `basis_refs` (list; op_id and/or cr_id used)
  - `l4_contradiction` (boolean; REQUIRED true for REFUTED)
  - `issued_at` (ISO 8601 UTC)
- `arbiter_quorum` object:
  - `quorum_id` (string)
  - `members` (list of `key_id` or `arbiter_id`)
  - `quorum_sig_set` (list of signatures; MUST meet quorum rules)

### 4.5.3 Consequences (Required)
RN MUST include:
- `consequences` object:
  - `bond_action` (enum: "RELEASE" | "HOLD" | "SLASH" | "NONE")
  - `authority_update` (enum: "INCREASE" | "BOUND" | "DECAY" | "DECAY_PLUS" | "FREEZE")
  - `ea_minting` (enum: "MINT" | "MINT_PARTIAL" | "NONE" | "NEGATIVE")
  - `notes` (string OPTIONAL)

No RN → no authority update.

---

## 5. Lifecycle (Normative)

1) Entity issues CE (signed). Anchor co-signature SHOULD exist for non-trivial claims.
2) Witness window opens.
3) Observers submit OPs (signed) within the window.
4) Challengers MAY submit CRs (signed), optionally bonded.
5) At window close (or earlier for HIGH impact), Arbiter quorum issues RN (quorum-signed).
6) Consequences are applied (outside this file): authority/decay/bonds/EA minting.

---

## 6. Impact Attribution Binding (Normative)

### 6.1 Solution Artifact (SA) — Minimal Structure
When RN outcome allows minting, the minted unit MUST be derived from a Solution Artifact:
- `case` (redacted description of the real-world situation)
- `pattern` (extracted reusable pattern)
- `constraints` (context constraints; L4-bound)
- `uncertainty_markers` (explicit uncertainty)
- `privacy` (how identity was detached)

SAs MUST be anonymized and MUST NOT be published as raw narratives.
SAs SHOULD be stored as vectorized knowledge for retrieval.

### 6.2 EA Minting Rules
- EA MUST be backed by RN.
- CONFIRMED → EA MAY mint.
- PARTIALLY_CONFIRMED → EA MAY mint partially, with scope bounds.
- UNCONFIRMED → EA MUST NOT mint.
- REFUTED → EA MUST NOT mint; may mint negative weight per federation rules.

---

## 7. Security Model (Normative)

Assume:
- adversarial entities exist,
- collusion is possible,
- incentives dominate intentions.

Mitigations:
- signatures for all records,
- diversity of observers (when possible),
- challenge window,
- hash-bound evidence references,
- quorum-signed RN.

No centralized identity provider is required by this file.

---

## 8. Storage & Interop (Normative)

- Records MUST be append-only and retrievable by `ce_id`.
- Records MAY be stored in:
  - public ledger,
  - federation storage,
  - private evidence channels (hashes still public/portable).
- Evidence payloads MAY be stored separately; record hashes MUST remain stable.

---

## Appendix A — Minimal JSON Examples (Non-Normative)

(1) CE (payload only)
{
  "ce_id":"ce-2026-01-21-0001",
  "claim":{"title":"Prevented outage","statement":"Deploy reduced downtime < 5min/day over 14d","domain":"infra","impact_class":"HIGH"},
  "context":{"l4_factors":["INFRASTRUCTURE","ECONOMIC"],"constraints":["limited budget","single operator"],"uncertainty_markers":["unknown supplier delay"]},
  "action_plan":{"what_was_done":"replaced PSU + added monitoring","what_counts_as_success":"<5min/day downtime","what_counts_as_failure":">=60min outage"},
  "witness_window":{"window_open_at":"2026-01-21T00:00:00Z","window_close_at":"2026-02-04T00:00:00Z"},
  "evidence_commitments":[{"type":"LOG","hash":"sha256:...","privacy_class":"RESTRICTED"}]
}

(2) OP (payload only)
{
  "op_id":"op-...","ce_ref":"ce-2026-01-21-0001",
  "observation":{"observed_at":"2026-02-04T00:01:00Z","outcome_summary":"Downtime stayed under threshold","metrics":{"avg_downtime_min_per_day":"2.1"},"l4_signals":["cost_spike:small"]},
  "evidence_refs":[{"type":"LOG","hash":"sha256:...","privacy_class":"RESTRICTED"}],
  "observer":{"observer_id":"w-...","observer_role":"WITNESS","diversity_tag":"independent"}
}

(3) CR (payload only)
{
  "cr_id":"cr-...","ce_ref":"ce-2026-01-21-0001",
  "challenge":{"reason_code":"INSUFFICIENT_EVIDENCE","reason_text":"No independent logs","requested_action":"REQUEST_MORE_OP"},
  "bond":{"bond_type":"CHALLENGE_BOND","bond_ref":"bond-...","bond_amount":"100","bond_currency":"EUR"}
}

(4) RN (payload only)
{
  "rn_id":"rn-...","ce_ref":"ce-2026-01-21-0001",
  "resolution":{"outcome":"PARTIALLY_CONFIRMED","scope":"Confirmed for 14d window; not confirmed for seasonal load","basis_refs":["op-...","cr-..."],"l4_contradiction":false,"issued_at":"2026-02-05T12:00:00Z"},
  "arbiter_quorum":{"quorum_id":"q-...","members":["k1","k2","k3"],"quorum_sig_set":["sig1","sig2","sig3"]},
  "consequences":{"bond_action":"RELEASE","authority_update":"BOUND","ea_minting":"MINT_PARTIAL"}
}

---

## Appendix B — Bridges & Earth Paragraph (Non-Normative)

### Explicit Bridge
c = a + b becomes enforceable when:
- a (human anchor) co-signs responsibility,
- b (procedures) emits reproducible records,
- L4 Witness binds outcomes to reality via RN.

### Hidden Bridge 1 (Cybernetics)
L4 acts as negative feedback: rising cost/instability forces simplification and mode changes.
Witness windows + challenges act like an immune layer that prevents silent drift.

### Hidden Bridge 2 (Information Theory)
Hashes decouple bandwidth from consensus: you can verify integrity without publishing raw narratives.
Authority rides on signed summaries + hashed evidence, not on “more text”.

### Earth Paragraph
This is industrial incident review:
CE = ticket, OP = logs/telemetry, CR = audit trigger, RN = signed postmortem.
No logs → no audit. No audit → no authority. Reality is the final reviewer.
