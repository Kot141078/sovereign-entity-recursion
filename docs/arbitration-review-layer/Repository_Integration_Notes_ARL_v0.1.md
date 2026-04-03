# Repository Integration Notes — ARL v0.1
## Integration-facing notes for canonical placement and discoverability

**Package:** Multi-Entity Arbitration / Review Layer v0.1  
**Short name:** ARL v0.1  
**Canonical home:** `sovereign-entity-recursion`  
**Author:** Ivan Kotov  
**Location:** Brussels  
**Year:** 2026  

---

## 1. Purpose

This document defines the intended repository-level integration strategy for the ARL package.

It exists to answer four practical questions:

1. where the package must live canonically,
2. how it should be surfaced inside the host repository,
3. how adjacent repositories should reference it without duplicating it,
4. and what minimum conditions must be satisfied before the package can be treated as integrated.

This file is integration-facing.
It does not replace the normative core.

---

## 2. Canonical repository rule

The canonical repository home of ARL v0.1 is:

`sovereign-entity-recursion`

ARL belongs here because it is a normative layer concerning:
- continuity,
- legitimacy,
- standing,
- review,
- dispute discipline,
- bounded authority,
- and witness-bound conflict resolution.

ARL is therefore closer to SER / SER-FED than to:
- AGI contextual framing,
- L4 operational notes alone,
- or executable code.

---

## 3. Canonical placement rule

### 3.1 Required path

Recommended canonical placement:

```text
docs/
  arbitration-review-layer/
```

### 3.2 Required package contents

The following files belong to the package:

- `README.md`
- `INDEX.md`
- `DOC_MAP.md`
- `Executive_Summary_Arbitration_Review_Layer_v0.1.md`
- `Multi_Entity_Arbitration_Review_Layer_v0.1.md`
- `Normative_Terms_and_Definitions_ARL_v0.1.md`
- `Evidence_Admissibility_and_Standing_v0.1.md`
- `Freeze_Hold_Quarantine_Semantics_v0.1.md`
- `Decision_Outcomes_and_Appeal_Window_v0.1.md`
- `Conflict_Class_Taxonomy_v0.1.md`
- `Cross_Repo_Pointers_ARL_v0.1.md`
- `Repository_Integration_Notes_ARL_v0.1.md`

### 3.3 Optional but strongly recommended package subdirectories

```text
pdf/
hashes/
```

The package should eventually produce:
- one PDF for each canonical Markdown artifact,
- one SHA-256 manifest for the package.

---

## 4. Discoverability rule

A package is not discoverable merely because it exists in a branch or by direct file link.

For ARL to be treated as properly integrated, an ordinary reader entering the default branch
must be able to find it without insider knowledge.

This means discoverability must be checked from the perspective of:
- a first-time human reader,
- a reviewer entering through the repo homepage,
- and a crawler reading the default branch only.

ARL must therefore be surfaced through visible entry documents,
not hidden as a silent subtree.

---

## 5. Required repository-level surfacing

### 5.1 README-level visibility
The repository README should contain a short visible pointer stating that
a bounded arbitration / review layer now exists in the SER ecosystem.

This pointer should not restate the whole package.
It should only indicate:
- that ARL exists,
- what it does at a high level,
- and where to find the canonical package.

### 5.2 INDEX / DOC_MAP / REPO_INDEX visibility
If the host repository uses any of the following:
- `INDEX.md`
- `DOC_MAP.md`
- `REPO_INDEX.md`
- equivalent package maps

then ARL should be listed there explicitly.

### 5.3 No hidden integration
It is not sufficient to:
- place files in a branch,
- store them only in `pdf/`,
- or expose them only through deep links.

The package must be visible from the ordinary reading path.

---

## 6. Adjacent repository reference rule

ARL should be referenced from adjacent repositories only through short canonical pointers.

### 6.1 `advanced-global-intelligence`
Role:
- context layer,
- framing layer,
- high-level stack coherence.

Permitted reference:
- a short statement that the stack now includes a bounded arbitration / review layer,
- a pointer to the canonical home in SER.

Not permitted:
- a duplicate mini-ARL package,
- a competing normative summary that drifts from SER.

### 6.2 `ester-reality-bound`
Role:
- freeze,
- quarantine,
- collision,
- witness,
- lawful re-entry semantics.

Permitted reference:
- a bridge note linking ARL to L4 freeze / witness / re-entry discipline.

Not permitted:
- relocating the arbitration layer into ERB as if ERB were its canonical home.

### 6.3 `ester-clean-code`
Role:
- implementation-facing future bridge,
- possible state machine / hook / event target.

Permitted reference:
- implementation-facing note only.

Not permitted:
- turning executable code into the canonical normative source.

---

## 7. Minimal integration proof

ARL v0.1 may be considered minimally integrated only if the following are all true:

1. the full Markdown package exists in the canonical path,
2. the repository default branch exposes at least one visible pointer to ARL,
3. `README.md` and `INDEX.md` inside the package are present,
4. package-facing map documents are present (`DOC_MAP`, `Repository Integration Notes`),
5. the package does not exist as competing normative copies in adjacent repositories.

Strongly recommended but not yet mandatory for minimal integration:
- PDFs,
- SHA-256 manifest,
- cross-repo pointer files committed in visible locations,
- release note or changelog mention.

---

## 8. Integration sequence (recommended)

### 8.1 Stage 1 — Text layer
Commit the Markdown package first.

Goal:
- canonical content exists,
- package structure exists,
- discoverability can be verified.

### 8.2 Stage 2 — Visibility layer
Update host-repo entry surfaces:
- README,
- INDEX,
- DOC_MAP,
- REPO_INDEX,
- MASTER_ENTRY if applicable.

Goal:
- default-branch readers can find the package.

### 8.3 Stage 3 — Artifact layer
Generate:
- PDFs,
- SHA-256 manifest,
- package-level integrity references.

Goal:
- the package becomes citable and checkable as an object.

### 8.4 Stage 4 — Cross-repo bridge layer
Add short canonical pointers in:
- AGI,
- ERB,
- ECC.

Goal:
- stack coherence without duplication.

---

## 9. Anti-fragmentation rule

ARL must not be integrated in a way that creates multiple quasi-canonical homes.

The following failure pattern must be avoided:

- normative core in one repository,
- stronger summary in a second repository,
- implementation semantics in a third repository,
- and no visible indication which version is final.

This produces ambiguity, not modularity.

The canonical rule is simple:

> one normative home,
> many short pointers,
> zero competing rulebooks.

---

## 10. Future implementation note

ARL may later require implementation-facing documents such as:
- judge node state model,
- witness event binding tables,
- freeze/re-entry state transitions,
- quorum behavior,
- recusal or anti-spam mechanics.

These do not belong in v0.1 integration notes unless they are required
for discoverability or placement.

The current document concerns repository integration only.

---

## 11. Explicit bridge

**SER continuity ↔ L4 witness / freeze ↔ Arbitration / Review Layer**

---

## 12. Hidden bridges

### 12.1 DEA / EA standing
ARL should remain linked to standing logic derived from DEA / EA,
but this linkage should remain concise and non-duplicative.

### 12.2 SER-FED anti-oligarchy
ARL integration must preserve the anti-capture logic of the wider SER ecosystem,
so that arbitration does not become a silent permanent power center.

---

## 13. Earth paragraph

On a real warehouse floor, the argument is not finished when someone writes the new rule on a sticky note and hides it in a drawer. It is finished when the procedure is placed in the official binder, the route signs are updated, and the next shift can find the same rule without asking around. Repository integration plays the same role here: it turns a document cluster into an operationally visible part of the system.

---

## 14. Status

Current status of ARL package integration:
- text package: assembled,
- terminology lock: assembled,
- package maps: assembled,
- repository placement: pending,
- discoverability checks: pending,
- PDF generation: pending,
- SHA-256 manifest: pending,
- cross-repo insertion: pending.
