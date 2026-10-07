# Final Branch Review — PRD Professionalisation
**Reviewed:** 2026-09-16
**Diff:** 6 commits, 4 files (index.md, DECISIONS.md new, UI_PRD.md, Development.md)
**Verdict:** FINDINGS

---

## Review Checklist Results

### 1. [ASSUMPTION] tags — all cite D-IDs?
PASS. Every [ASSUMPTION] in UI_PRD.md and index.md carries a D-ID:
D-023 (dark theme rows), D-024 (breakpoints section + table), D-026 (navigation),
D-027 (badge text color — appears twice, in 1.1 and 2.1, consistent), D-028 (button radius),
D-020 (font fallback — see F-004 below for a minor issue with this one).

### 2. [REF] tags — all cite D-IDs?
PASS. All [REF] tags cite valid D-IDs:
D-021 (light theme), D-022 (status colors), D-029 (touch target + button height),
D-030 (spacing and grid — appears in UI_PRD.md and index.md).

### 3. DECISIONS.md covers every D-ID cited in other files?
PASS with one caveat (see F-002).
All D-IDs (D-001–D-008, D-010–D-016, D-020–D-030) and P-IDs (P-001–P-006) cited
across UI_PRD.md, Development.md, and index.md are present in DECISIONS.md.

### 4. Functional-requirements disclaimer placed before Section 3 in UI_PRD.md?
PASS. The blockquote disclaimer ("Section ini berisi Functional Requirements...
[DESIGN TBD] P-004") appears immediately before `## 3. Spesifikasi Per Layar`.
Placement is correct.

### 5. index.md legend defines all 4 markers?
PASS. All four markers defined: [CONFIRMED], [REF], [ASSUMPTION], [DESIGN TBD].
Definitions are accurate and consistent with usage in the files.

### 6. Inconsistency between DECISIONS.md and PRD files?
PARTIAL FAIL — see F-002 and F-003.

### 7. Confirmed content removed?
FAIL — see F-001.

---

## Findings

### F-001 [Important] — Confirmed scope constraint removed from index.md

**File:** index.md, Catatan Lintas-Domain
**Old line (removed):**
```
- Notifikasi suara/getar: opsional, tidak masuk v1.
```
**New content:** No equivalent entry exists — not in the new Catatan Lintas-Domain,
not in DECISIONS.md, not in any other file in the diff.

This is a confirmed product scope decision (notifications/sound out of v1) that was
silently dropped during the restructure. It is not the same as the items that were
converted to DECISIONS.md cross-references (threshold → P-002, PDF → P-001).
Violates the global constraint "no confirmed content removed."

**Fix required:** Either restore the line in index.md, or add a DECISIONS.md entry
(e.g. D-017: "Sound/vibration notifications — out of v1 scope") and cross-reference
it, consistent with how P-001 and P-002 are handled.

---

### F-002 [Minor] — D-021 description in DECISIONS.md omits Surface color

**File:** DECISIONS.md line 42
**D-021 description:** "Light theme palette (BG `#F4F7FE`, Primary `#4318FF`,
Heading `#2B3674`, Body `#A3AED0`)"
**Problem:** `color-surface: #FFFFFF` is cited as `[REF]` D-021 in both UI_PRD.md
and index.md, but Surface (#FFFFFF) is absent from D-021's description.
A reader checking D-021 cannot confirm the `#FFFFFF` value from the decision log.

**Fix:** Append "Surface `#FFFFFF`" to D-021's Keputusan cell, e.g.:
"Light theme palette (BG `#F4F7FE`, Surface `#FFFFFF`, Primary `#4318FF`,
Heading `#2B3674`, Body `#A3AED0`)"

---

### F-003 [Minor] — [DESIGN TBD] marker not defined in DECISIONS.md "Cara Membaca"

**File:** DECISIONS.md lines 70–73
**Problem:** The Cara Membaca glossary defines CONFIRMED, REF, ASSUMPTION, and
Pending (P-xxx) — but does not define `[DESIGN TBD]`. The marker is actively used
in UI_PRD.md (Section 3 disclaimer, tagged P-004). A reader consulting DECISIONS.md
for marker definitions will not find it.
(index.md legend does define it correctly — the gap is only in DECISIONS.md.)

**Fix:** Add a fifth bullet to Cara Membaca:
"- **DESIGN TBD:** Menunggu input desain aktual (Figma/mockup) — jangan
diimplementasikan sampai design file diterima"

---

### F-004 [Minor] — Font fallback [ASSUMPTION] cross-references a CONFIRMED D-ID

**File:** UI_PRD.md, Section 1.2 Tipografi
**Line:** "Font fallback: Inter, Roboto, system-ui. `[ASSUMPTION]` D-020 — fallback
order belum dikonfirmasi."
**Problem:** D-020 is a CONFIRMED decision (Plus Jakarta Sans). An [ASSUMPTION] tag
on the same line citing a CONFIRMED D-ID can confuse a reader: does [ASSUMPTION] apply
to D-020, or only to the fallback? The assumption is about fallback order, which has
no dedicated D-ID.

**Fix (two options):**
- Add a new DECISIONS.md entry (e.g. D-031: "Font fallback order: Inter, Roboto,
  system-ui — ASSUMPTION") and re-tag the line `[ASSUMPTION]` D-031.
- Or, if a new D-ID is not worth the overhead, rewrite the line to clearly separate
  the confirmed from the assumed:
  "Font: Plus Jakarta Sans `[CONFIRMED]` D-020. Fallback order (Inter, Roboto,
  system-ui) `[ASSUMPTION]` — belum dikonfirmasi."

---

## Summary

| ID | Severity | Description |
|---|---|---|
| F-001 | Important | "Notifikasi suara/getar: opsional, tidak masuk v1" removed with no equivalent preserved |
| F-002 | Minor | D-021 description missing Surface `#FFFFFF` — cited token has no backing in the decision log |
| F-003 | Minor | DECISIONS.md "Cara Membaca" does not define [DESIGN TBD] marker |
| F-004 | Minor | Font fallback [ASSUMPTION] co-tags a CONFIRMED D-ID (D-020), creating ambiguity |

**Blockers before merge:** F-001 must be resolved (confirmed content was removed).
F-002, F-003, F-004 can be fixed in the same pass — all are one-line or two-line edits.
No structural rework needed.
