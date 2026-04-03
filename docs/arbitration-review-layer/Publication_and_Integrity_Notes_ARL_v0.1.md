# Publication and Integrity Notes — ARL v0.1
## Publication-facing and integrity-facing notes for the ARL package

**Package:** Multi-Entity Arbitration / Review Layer v0.1  
**Short name:** ARL v0.1  
**Canonical home:** `sovereign-entity-recursion`  
**Author:** Ivan Kotov  
**Location:** Brussels  
**Year:** 2026  

---

## 1. Purpose

This document defines the minimum publication-facing and integrity-facing requirements
for the ARL package.

It answers four practical questions:

1. which artifacts must exist for the package to be publication-ready,
2. how the integrity contour of the package should be represented,
3. what minimum evidence is required to treat the package as a stable public object,
4. and which publication shortcuts must be avoided.

This document is publication-facing.
It does not replace the normative content of the package.

---

## 2. Publication principle

ARL v0.1 should not remain only a working text cluster.

To become a stable object in the public corpus, it must exist in a form that is:

- readable by humans,
- stable across time,
- checkable without private trust,
- citable as a package,
- and discoverable from the canonical repository path.

Publication is therefore not just "files exist".
Publication means:
- the package has a readable surface,
- the package has an integrity surface,
- and the package can be checked as an object rather than merely described.

---

## 3. Minimum Markdown package

Before any PDF or hash layer is created, the package MUST already contain the full canonical Markdown layer.

Minimum required Markdown artifacts:

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
- `Publication_and_Integrity_Notes_ARL_v0.1.md`

If this Markdown layer is incomplete, the package is not publication-ready.

---

## 4. PDF contour

### 4.1 Purpose of the PDF layer

The PDF layer exists to provide:
- a stable reading surface,
- a printable review surface,
- a frozen human-facing representation,
- and a publication-ready citation object.

Markdown remains the editable working surface.
PDF becomes the stable presentation surface.

### 4.2 Recommended PDF set

The following PDFs are recommended for ARL v0.1:

- `Executive_Summary_Arbitration_Review_Layer_v0.1.pdf`
- `Multi_Entity_Arbitration_Review_Layer_v0.1.pdf`
- `Normative_Terms_and_Definitions_ARL_v0.1.pdf`
- `Evidence_Admissibility_and_Standing_v0.1.pdf`
- `Freeze_Hold_Quarantine_Semantics_v0.1.pdf`
- `Decision_Outcomes_and_Appeal_Window_v0.1.pdf`
- `Conflict_Class_Taxonomy_v0.1.pdf`

Optional but useful PDFs:
- `DOC_MAP.pdf`
- `Repository_Integration_Notes_ARL_v0.1.pdf`
- `Publication_and_Integrity_Notes_ARL_v0.1.pdf`

### 4.3 PDF rule

The PDF layer must not silently diverge from the Markdown source.
If typography or layout is improved, content must remain materially unchanged.

If content is changed for publication,
the Markdown source must be updated first.

---

## 5. Integrity contour

### 5.1 Purpose

The integrity contour exists so that the package can be verified without narrative trust.

Instead of asking a reader to believe:
- that the files are the same,
- that the PDFs match the source,
- or that the package was not silently altered,

the integrity contour allows a reader to verify this through hashes.

### 5.2 Minimum integrity artifact

Recommended package-level integrity file:

`SHA256SUMS_arbitration_review_layer_v0.1.txt`

This manifest should contain SHA-256 hashes for:
- all canonical Markdown files,
- all canonical PDFs,
- and any package-facing index files included in the publication surface.

### 5.3 Naming discipline

The SHA file should use stable, explicit naming.
Avoid vague names such as:
- `hashes.txt`
- `checksums.txt`
- `sha.txt`

The name should clearly identify:
- the package,
- the version,
- and the artifact set.

---

## 6. Minimal integrity scope

At minimum, the following files should be covered by the SHA-256 manifest:

### 6.1 Markdown integrity set
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
- `Publication_and_Integrity_Notes_ARL_v0.1.md`

### 6.2 PDF integrity set
- `Executive_Summary_Arbitration_Review_Layer_v0.1.pdf`
- `Multi_Entity_Arbitration_Review_Layer_v0.1.pdf`
- `Normative_Terms_and_Definitions_ARL_v0.1.pdf`
- `Evidence_Admissibility_and_Standing_v0.1.pdf`
- `Freeze_Hold_Quarantine_Semantics_v0.1.pdf`
- `Decision_Outcomes_and_Appeal_Window_v0.1.pdf`
- `Conflict_Class_Taxonomy_v0.1.pdf`

Optional but recommended:
- `DOC_MAP.pdf`
- `Repository_Integration_Notes_ARL_v0.1.pdf`
- `Publication_and_Integrity_Notes_ARL_v0.1.pdf`

---

## 7. Publication-ready conditions

ARL v0.1 may be treated as publication-ready only if all of the following are true:

1. the full canonical Markdown package exists,
2. the canonical repository path is defined,
3. the package is discoverable from the default branch,
4. the core PDF layer exists,
5. the package-level SHA-256 manifest exists,
6. the package does not rely on oral explanation for interpretation,
7. the package has a visible package facade (`README`, `INDEX`, `DOC_MAP`),
8. the package has at least one stable human-facing entry object (`Executive Summary` PDF).

If these conditions are not met, publication may be premature even if the text is strong.

---

## 8. What counts as a stable public object

For ARL to function as a stable public object, the following must be simultaneously true:

- a reader can find it,
- a reader can read it,
- a reader can cite it,
- a reader can verify it,
- and a future reader can distinguish the working source from the frozen presentation.

Without all five, the package remains only partially public.

---

## 9. Anti-shortcut rules

The following publication shortcuts should be explicitly avoided.

### 9.1 PDF-only publication
Publishing only PDFs without the source Markdown weakens future maintenance
and makes controlled revision harder.

### 9.2 Markdown-only publication
Leaving the package only as Markdown weakens the frozen public surface
and makes formal review less stable.

### 9.3 Hashless publication
Publishing without a package-level hash manifest invites silent drift
and undermines the integrity surface.

### 9.4 Branch-only publication
If the package exists only in a non-default branch or via direct file link,
it is not properly discoverable.

### 9.5 Cross-repo duplication
If ARL is restated as competing normative summaries in multiple repositories,
publication creates ambiguity rather than clarity.

---

## 10. Publication sequence (recommended)

### 10.1 Stage 1 — Complete text package
Assemble and verify the Markdown layer.

### 10.2 Stage 2 — Generate PDFs
Render the canonical human-facing PDF set.

### 10.3 Stage 3 — Generate SHA-256 manifest
Hash all canonical Markdown and PDF artifacts.

### 10.4 Stage 4 — Surface package discoverability
Ensure the package is visible from the canonical repository entry path.

### 10.5 Stage 5 — Add cross-repo pointers
Only after the canonical package is stable should adjacent repositories receive short bridge pointers.

---

## 11. Minimal integrity contour

The minimum integrity contour for ARL v0.1 consists of:

- the canonical Markdown package,
- the canonical PDF set,
- the package SHA-256 manifest,
- visible repository entry points,
- and a stable canonical home.

Anything less may still be useful,
but it should not yet be described as a fully fixed publication object.

---

## 12. Future publication extensions

The following may be added later, but are not required for the first public package:

- package release notes,
- changelog entry,
- citation metadata,
- Zenodo-facing metadata,
- release asset bundle,
- repository-level publication snapshots.

These strengthen publication, but they are not prerequisites for the first fixed integrity contour.

---

## 13. Explicit bridge

**SER continuity ↔ L4 witness / freeze ↔ Arbitration / Review Layer**

---

## 14. Hidden bridges

### 14.1 DEA / EA standing
Publication should preserve the concise linkage between ARL standing logic and DEA / EA structure,
without duplicating the full DEA / EA corpus inside the package.

### 14.2 SER-FED anti-oligarchy
Publication must preserve the anti-capture orientation of the wider SER ecosystem,
so that arbitration appears as bounded review rather than silent sovereignty transfer.

---

## 15. Earth paragraph

A real warehouse operator does not call a shipment "official" because the boxes exist on the floor. It becomes official when the labels are attached, the manifest is filed, the seal is applied, and the ledger can be checked later by someone who was not there that day. Publication and integrity play the same role here: they turn a document cluster into a verifiable object that survives beyond the people who assembled it.

---

## 16. Status

Current ARL publication and integrity status:
- canonical Markdown package: assembled,
- package maps: assembled,
- integration notes: assembled,
- PDF contour: pending,
- SHA-256 manifest: pending,
- final canonical placement: pending,
- publication-ready state: not yet complete.
