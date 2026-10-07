# PRD Professionalisation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Refactor all PRD files so every piece of content is clearly tagged by its confidence level — confirmed by user, derived from reference docs, or Claude assumption awaiting design input.

**Architecture:** Introduce a status-marker system (`[CONFIRMED]` / `[REF]` / `[ASSUMPTION]` / `[DESIGN TBD]`) as a shared legend in `index.md`, then apply it consistently across `UI_PRD.md`, `Development.md`, and `User_Requirements.md`. Create a `DECISIONS.md` log that is the single source of truth for all key decisions and their origins.

**Tech Stack:** Markdown only — no code, no tooling.

**Spec:** Derived from analysis of current PRD files + user brief (session context).

## Global Constraints

- All files live in `C:/Claude/Pervasive/`
- Language: Indonesian (mixed with English technical terms is OK)
- Do NOT remove any confirmed content — only reclassify or add markers
- Do NOT add design decisions that aren't from user input or reference docs
- Every `[ASSUMPTION]` or `[DESIGN TBD]` block must include what input is needed to resolve it

---

## Task 1: Define the Status Marker System (index.md)

**Files:**
- Modify: `C:/Claude/Pervasive/index.md`

**Interfaces:**
- Produces: shared legend used by all other files

- [ ] **Step 1: Add document metadata block at the top of index.md**

Insert after the `# Index` heading:

```markdown
**PRD Version:** 0.2 — Prototype Draft
**Last Updated:** 2026-09-16
**Status:** In Progress — Design not yet received

---

## Status Marker Legend

Every section in this PRD set uses one of four markers:

| Marker | Meaning |
|---|---|
| `[CONFIRMED]` | Explicitly decided by user (Henry) in session |
| `[REF]` | Derived from reference docs (UI_stitch / UI_stitch_Gemini) — needs user validation before design handoff |
| `[ASSUMPTION]` | Claude's best-guess fill-in — NOT confirmed, must be validated or replaced before design starts |
| `[DESIGN TBD]` | Intentionally left blank — requires actual design input (Figma / mockup) before this field can be filled |

**Rule:** Any field marked `[ASSUMPTION]` or `[DESIGN TBD]` in UI_PRD.md is NOT safe to implement until the designer or user provides the real value.
```

- [ ] **Step 2: Tag all sections in index.md with appropriate markers**

In the Design System section, each property gets a marker. Example:
```markdown
- **Layout:** Responsive — desktop 1280px+ / tablet 768–1279px / mobile <768px `[ASSUMPTION]`
- **Font:** Plus Jakarta Sans `[CONFIRMED]`
- **Light theme colors:** `[REF]` — from UI_stitch.md BloomBoost palette
- **Dark theme colors:** `[ASSUMPTION]` — picked by Claude, not confirmed
- **Status colors:** `[REF]` — #22C55E · #F59E0B · #EF4444
```

- [ ] **Step 3: Commit**

```
git add index.md
git commit -m "prd: add status marker legend and metadata to index.md"
```

---

## Task 2: Create DECISIONS.md

**Files:**
- Create: `C:/Claude/Pervasive/DECISIONS.md`

**Interfaces:**
- Produces: single source of truth for all key decisions across the PRD set

- [ ] **Step 1: Create DECISIONS.md with full decision log**

```markdown
# Decision Log — Application Monitoring Peralatan Industri

Setiap keputusan penting dalam PRD dicatat di sini beserta sumbernya.
Format: **[ID]** Keputusan — *Sumber* — Tanggal

---

## Platform & Tech

| ID | Keputusan | Sumber | Status |
|---|---|---|---|
| D-001 | Platform: React JS web app | CONFIRMED — user input | 2026-09-16 |
| D-002 | Styling: Tailwind CSS | CONFIRMED — user input | 2026-09-16 |
| D-003 | State management: Zustand | CONFIRMED — user input | 2026-09-16 |
| D-004 | Charting: Recharts | CONFIRMED — user input | 2026-09-16 |
| D-005 | Backend: Express.js | CONFIRMED — user input | 2026-09-16 |
| D-006 | Database: SQLite (local prototype) | CONFIRMED — user input | 2026-09-16 |
| D-007 | Auth: JWT | CONFIRMED — user input | 2026-09-16 |
| D-008 | Real-time: Polling 10 detik (prototype) | CONFIRMED — user input | 2026-09-16 |

## Scope & Screens

| ID | Keputusan | Sumber | Status |
|---|---|---|---|
| D-010 | 6 screens: S-01 s/d S-06 | CONFIRMED — user input | 2026-09-16 |
| D-011 | S-06 User Management — supervisor only | CONFIRMED — user input | 2026-09-16 |
| D-012 | Role-based access: teknisi vs supervisor | CONFIRMED — user input | 2026-09-16 |
| D-013 | Local deployment only, no cloud/SCADA | CONFIRMED — user input | 2026-09-16 |
| D-014 | Historical data range: 1 bulan | CONFIRMED — user input | 2026-09-16 |
| D-015 | Resolved alarm hilang dari global list | CONFIRMED — user input | 2026-09-16 |
| D-016 | Alarm export: PDF | CONFIRMED — user input | 2026-09-16 |

## Design System

| ID | Keputusan | Sumber | Status |
|---|---|---|---|
| D-020 | Font: Plus Jakarta Sans | CONFIRMED — user input | 2026-09-16 |
| D-021 | Light theme palette (BG #F4F7FE, Primary #4318FF, dll) | REF — UI_stitch.md BloomBoost | Perlu validasi |
| D-022 | Status colors (#22C55E / #F59E0B / #EF4444) | REF — UI_stitch.md + Gemini | Perlu validasi |
| D-023 | Dark theme palette (#0F172A, #1E293B, #818CF8, dll) | **ASSUMPTION — Claude** | ⚠️ Belum dikonfirmasi |
| D-024 | Responsive breakpoints (1280 / 768 / <768 px) | **ASSUMPTION — Claude** | ⚠️ Belum dikonfirmasi |
| D-025 | Equipment card grid: 2 kolom × 3 baris | CONFIRMED — user input | 2026-09-16 |
| D-026 | Navigation: side nav desktop, hamburger mobile | **ASSUMPTION — Claude** | ⚠️ Belum dikonfirmasi |
| D-027 | Badge text color: putih #FFFFFF | **ASSUMPTION — Claude** (contrast calc) | ⚠️ Perlu validasi |
| D-028 | Button border radius: 8px | **ASSUMPTION — Claude** | ⚠️ Belum dikonfirmasi |
| D-029 | Touch target minimum: 48×48 px | REF — UI_stitch.md | Perlu validasi |
| D-030 | 8-point grid spacing (8/16/24/32 px) | REF — UI_stitch.md | Perlu validasi |

## Pending Decisions (Belum Diputuskan)

| ID | Topik | Butuh Input Dari | Catatan |
|---|---|---|---|
| P-001 | Template & format PDF laporan (S-05) | User / Designer | Brainstorm terpisah |
| P-002 | Nilai threshold per parameter per mesin | User / Engineering | Menunggu data sensor |
| P-003 | Logo / branding visual app | User / Designer | Placeholder OK untuk prototype |
| P-004 | Desain visual aktual (Figma) — semua screen | Designer | Belum ada; UI_PRD Section 3 adalah functional spec, bukan visual spec |
| P-005 | Validasi dark mode palette | User / Designer | Claude memilih, belum disetujui |
| P-006 | Validasi responsive breakpoints | User | Claude mengasumsikan standar industri |
```

- [ ] **Step 2: Commit**

```
git add DECISIONS.md
git commit -m "prd: add decision log with source tracking (DECISIONS.md)"
```

---

## Task 3: Refactor UI_PRD.md — Separate Requirements from Design Specs

Ini task paling kritis. `UI_PRD.md` saat ini mencampur dua hal:
1. **Functional UI Requirements** — apa yang harus ada di screen (ini sudah bisa ditulis)
2. **Visual Design Specifications** — bagaimana tampilannya (ini HARUS dari designer)

**Files:**
- Modify: `C:/Claude/Pervasive/UI_PRD.md`

**Interfaces:**
- Consumes: Status marker legend dari Task 1, Decision IDs dari Task 2

- [ ] **Step 1: Add document metadata and status banner at top**

```markdown
# UI PRD — Application Monitoring Peralatan Industri

**Status:** DRAFT — Visual design not yet received
**Design Handoff Status:** Pending — sections marked `[DESIGN TBD]` cannot be implemented until Figma/mockup is delivered

> **⚠️ Catatan untuk Designer:**
> Section 1 (Design Tokens) berisi nilai yang sebagian adalah asumsi Claude (`[ASSUMPTION]`)
> dan sebagian dari dokumen referensi (`[REF]`). Nilai `[ASSUMPTION]` harus diganti dengan
> nilai dari Figma design system sebelum development dimulai.
>
> Section 3 (Per-Screen Specs) berisi **functional requirements** — apa yang harus ada di
> setiap screen. Layout dan visual detail ada di Figma (belum tersedia).
```

- [ ] **Step 2: Tag setiap nilai di Section 1 (Design Tokens)**

Contoh format per token:

```markdown
| `color-background` | `#F4F7FE` | Latar belakang halaman | `[REF]` D-021 |
| `color-primary` | `#4318FF` | Aksen utama | `[REF]` D-021 |
| `color-background-dark` | `#0F172A` | Latar belakang dark | `[ASSUMPTION]` D-023 |
| `color-primary-dark` | `#818CF8` | Aksen dark mode | `[ASSUMPTION]` D-023 |
| `color-status-normal` | `#22C55E` | Status normal | `[REF]` D-022 |
```

- [ ] **Step 3: Tag Section 1.4 (Layout)**

```markdown
### 1.4 Layout & Responsive Breakpoints `[ASSUMPTION]` D-024

> ⚠️ Breakpoints di bawah adalah asumsi standar industri yang dipilih Claude.
> Harus dikonfirmasi oleh user/designer sebelum CSS ditulis.

| Breakpoint | Range | Notes |
...
```

- [ ] **Step 4: Tag Section 2 (Komponen)**

```markdown
### 2.2 Button
- Border radius: 8px `[ASSUMPTION]` D-028 — ganti dengan nilai dari design system
- Tinggi: 48 px `[REF]` D-029

### 2.4 Navigation
- Tipe: Side nav (desktop/tablet), hamburger mobile `[ASSUMPTION]` D-026
  → Harus dikonfirmasi. Alternatif: bottom nav di semua breakpoint.
```

- [ ] **Step 5: Add disclaimer block di atas Section 3 (Per-Screen Specs)**

```markdown
## 3. Spesifikasi Per Layar

> **Penting:** Section ini berisi **Functional Requirements** — elemen apa saja yang
> harus ada di setiap layar dan apa fungsinya. Ini BUKAN visual spec.
>
> Visual layout, spacing, ukuran eksak, dan styling akan didefinisikan setelah
> Figma design diterima. Jangan gunakan section ini sebagai panduan visual tanpa
> design file.
```

- [ ] **Step 6: Commit**

```
git add UI_PRD.md
git commit -m "prd: tag all design tokens with source markers, separate functional req from visual spec"
```

---

## Task 4: Add Source Tags to Development.md

**Files:**
- Modify: `C:/Claude/Pervasive/Development.md`

**Interfaces:**
- Consumes: Decision IDs dari Task 2

- [ ] **Step 1: Add document metadata block**

```markdown
# Development — Application Monitoring Peralatan Industri

**Status:** DRAFT — Tech stack confirmed, implementation not started
**Dependencies:** UI_PRD.md visual specs must be finalized before frontend styling begins
```

- [ ] **Step 2: Tag tech stack table dengan decision IDs**

```markdown
| Frontend | React JS | D-001 `[CONFIRMED]` |
| Styling | Tailwind CSS | D-002 `[CONFIRMED]` |
| State Management | Zustand | D-003 `[CONFIRMED]` |
...
```

- [ ] **Step 3: Tag threshold fields di data model**

```markdown
thresholdWarning: number | null   // [CONFIRMED] nullable — D-xxx, P-002
thresholdFault: number | null     // [CONFIRMED] nullable — sensor belum ditest
```

- [ ] **Step 4: Commit**

```
git add Development.md
git commit -m "prd: add source tags and decision IDs to Development.md"
```

---

## Task 5: Final Consistency Check

- [ ] **Step 1: Verify DECISIONS.md covers every tagged item**

Read DECISIONS.md and check: setiap D-xxx yang disebutkan di UI_PRD.md ada entrynya di tabel.

- [ ] **Step 2: Verify no [ASSUMPTION] content is presented as final spec**

Grep through all PRD files for any definitive-sounding statement that doesn't have a status marker. Add the marker.

- [ ] **Step 3: Verify index.md reflects the new structure**

Update the "Catatan Lintas-Domain" section to reference DECISIONS.md:
```markdown
## Catatan Lintas-Domain
- Semua keputusan dan sumbernya → [DECISIONS.md](./DECISIONS.md)
- Item bertanda `[ASSUMPTION]` tidak boleh diimplementasikan sebelum dikonfirmasi
```

- [ ] **Step 4: Final commit**

```
git add .
git commit -m "prd: final consistency pass — all assumptions marked, DECISIONS.md cross-referenced"
git push origin main
```

---

## Self-Review Checklist

- [ ] Setiap nilai hex color di UI_PRD.md punya status marker
- [ ] Setiap keputusan di DECISIONS.md punya Decision ID yang bisa di-cross-reference
- [ ] Section 3 UI_PRD.md punya disclaimer bahwa ini functional req, bukan visual spec
- [ ] Tidak ada kalimat di PRD yang berbunyi "harus X" tanpa status marker kalau X adalah asumsi
- [ ] index.md punya legend yang menjelaskan semua marker
- [ ] Semua `[ASSUMPTION]` entries di DECISIONS.md punya kolom "Butuh Input Dari"
