# Task 3 Brief: Refactor UI_PRD.md

## What you are doing

You are editing ONE file: `C:/Claude/Pervasive/UI_PRD.md`

This is a Markdown-only documentation task — no code, no tests.

## Context from earlier tasks

- Task 1 added a status marker legend to index.md (defines [CONFIRMED] / [REF] / [ASSUMPTION] / [DESIGN TBD])
- Task 2 created DECISIONS.md with D-IDs for every key decision

You will reference those D-IDs when tagging values.

## Global Constraints

- Language: Indonesian (English technical terms OK)
- Do NOT remove any confirmed content — only add markers and metadata
- Do NOT add new design decisions — only mark existing ones with their source
- Every `[ASSUMPTION]` tag must cite a D-ID from DECISIONS.md
- Every `[REF]` tag must cite a D-ID from DECISIONS.md
- Git binary: `"C:/Program Files/Git/cmd/git.exe"` (use full path — bare `git` is NOT in PATH)

## Steps to execute

### Step 1: Add document metadata and status banner

Read `C:/Claude/Pervasive/UI_PRD.md` first.

Replace the current heading block (the first few lines) so it reads:

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

Dokumen ini ditujukan untuk **UI Designer**. Berisi semua spesifikasi visual yang dibutuhkan untuk membuat desain yang konsisten dan sesuai standar produk.
```

### Step 2: Tag Section 1.1 color tables

The current Section 1.1 has three subsections. Add a 5th column "Source" to each color table. The final format for each table:

**Light Theme table** — add `| Source |` column:
```markdown
| Token | Hex | Penggunaan | Source |
|---|---|---|---|
| `color-background` | `#F4F7FE` | Latar belakang halaman | `[REF]` D-021 |
| `color-surface` | `#FFFFFF` | Latar kartu / panel | `[REF]` D-021 |
| `color-primary` | `#4318FF` | Aksen utama, tombol primary, link aktif | `[REF]` D-021 |
| `color-text-heading` | `#2B3674` | Teks judul, heading | `[REF]` D-021 |
| `color-text-body` | `#A3AED0` | Teks sekunder, label, caption | `[REF]` D-021 |
```

**Dark Theme table** — add `| Source |` column:
```markdown
| Token | Hex | Penggunaan | Source |
|---|---|---|---|
| `color-background-dark` | `#0F172A` | Latar belakang halaman (dark) | `[ASSUMPTION]` D-023 |
| `color-surface-dark` | `#1E293B` | Latar kartu / panel (dark) | `[ASSUMPTION]` D-023 |
| `color-primary-dark` | `#818CF8` | Aksen utama (lighter indigo untuk dark bg) | `[ASSUMPTION]` D-023 |
| `color-text-heading-dark` | `#E2E8F0` | Teks judul (dark) | `[ASSUMPTION]` D-023 |
| `color-text-body-dark` | `#94A3B8` | Teks sekunder (dark) | `[ASSUMPTION]` D-023 |
```

**Status / Alarm Colors table** — add `| Source |` column:
```markdown
| Token | Hex | Penggunaan | Source |
|---|---|---|---|
| `color-status-normal` | `#22C55E` | Status beroperasi / normal | `[REF]` D-022 |
| `color-status-warning` | `#F59E0B` | Status peringatan | `[REF]` D-022 |
| `color-status-fault` | `#EF4444` | Status gangguan / fault | `[REF]` D-022 |
```

Also add this line after the Status table (replacing the existing badge text line):
```markdown
**Teks di atas badge status:** putih `#FFFFFF` untuk semua variant. `[ASSUMPTION]` D-027 — contrast ratio WCAG AA terpenuhi, perlu validasi designer.
```

### Step 3: Tag Section 1.2 (Typography)

Add `| Source |` column to the typography table:
```markdown
| Token | Font | Size | Weight | Penggunaan | Source |
|---|---|---|---|---|---|
| `text-title` | Plus Jakarta Sans | 24–32 px | Bold (700) | Judul halaman, nama mesin | `[CONFIRMED]` D-020 |
| `text-body` | Plus Jakarta Sans | 16 px | Regular (400) | Konten utama, deskripsi | `[CONFIRMED]` D-020 |
| `text-caption` | Plus Jakarta Sans | 12–14 px | Regular / Medium (400/500) | Label, timestamp, unit parameter | `[CONFIRMED]` D-020 |
```

After the table add:
```
Font fallback: Inter, Roboto, system-ui. `[ASSUMPTION]` — fallback order belum dikonfirmasi.
```

### Step 4: Tag Section 1.3 (Spacing)

Add `| Source |` column to the spacing table:
```markdown
| Token | Value | Penggunaan | Source |
|---|---|---|---|
| `space-xs` | 8 px | Gap antar elemen dalam kartu | `[REF]` D-030 |
| `space-sm` | 16 px | Padding internal kartu, margin grid | `[REF]` D-030 |
| `space-md` | 24 px | Jarak antar seksi | `[REF]` D-030 |
| `space-lg` | 32 px | Jarak antar kartu / blok besar | `[REF]` D-030 |
```

### Step 5: Tag Section 1.4 (Layout)

Replace the Section 1.4 heading with:
```markdown
### 1.4 Layout & Responsive Breakpoints `[ASSUMPTION]` D-024

> ⚠️ Breakpoints di bawah adalah asumsi standar industri yang dipilih Claude.
> Harus dikonfirmasi oleh user/designer sebelum CSS ditulis. Lihat D-024 di DECISIONS.md.
```

Add `| Source |` column to the breakpoints table:
```markdown
| Breakpoint | Range | Layout Notes | Source |
|---|---|---|---|
| Desktop | 1280px+ | Main target — side nav tetap terbuka | `[ASSUMPTION]` D-024 |
| Tablet | 768–1279px | Side nav bisa collapsible | `[ASSUMPTION]` D-024 |
| Mobile | <768px | Side nav collapse jadi hamburger menu | `[ASSUMPTION]` D-024 |
```

The two bullet points below the table also get tagged:
```markdown
- **Grid:** 12 kolom, margin 16 px, gutter 16 px `[REF]` D-030
- **Touch target minimum:** 48 × 48 px `[REF]` D-029
```

### Step 6: Tag Section 2 (Components)

In Section 2.1 (Status Badge), add after the table:
```markdown
> Teks di atas semua badge: putih `#FFFFFF`. `[ASSUMPTION]` D-027
```

In Section 2.2 (Button), add source tags to the spec bullets:
```markdown
- Tinggi: 48 px `[REF]` D-029
- Border radius: 8 px `[ASSUMPTION]` D-028 — ganti dengan nilai dari design system Figma
```

In Section 2.3 (Equipment Card), add after grid note:
```markdown
> Grid layout 2 kolom × 3 baris. `[CONFIRMED]` D-025
```

In Section 2.4 (Navigation), replace the type line with:
```markdown
**Desktop/Tablet (768px+):** Side Navigation (vertikal di kiri) `[ASSUMPTION]` D-026
**Mobile (<768px):** Collapse menjadi hamburger menu atau bottom nav `[ASSUMPTION]` D-026
> Konfirmasi preferensi nav sebelum implementasi. Lihat D-026 di DECISIONS.md.
```

### Step 7: Add functional-vs-visual disclaimer above Section 3

Insert before the `## 3. Spesifikasi Per Layar` heading:

```markdown
---

> **Penting:** Section ini berisi **Functional Requirements** — elemen apa saja yang
> harus ada di setiap layar dan apa fungsinya. Ini BUKAN visual spec.
>
> Visual layout, spacing exact, posisi elemen, dan styling akan didefinisikan setelah
> Figma design diterima. Jangan gunakan section ini sebagai panduan visual tanpa
> design file dari designer. `[DESIGN TBD]` P-004

```

### Step 8: Commit

```
"C:/Program Files/Git/cmd/git.exe" -C "C:/Claude/Pervasive" add UI_PRD.md
"C:/Program Files/Git/cmd/git.exe" -C "C:/Claude/Pervasive" commit -m "prd: tag all design tokens with source markers, separate functional req from visual spec"
```

## Report

Write your report to: `C:/Claude/Pervasive/.superpowers/sdd/2026-09-16-prd-professionalisation/task-3-report.md`

Report must contain:
- Status: DONE / DONE_WITH_CONCERNS / NEEDS_CONTEXT / BLOCKED
- Commit hash
- Any concerns

Return to me: status, commit hash, one-line summary. Do NOT dispatch subagents.
