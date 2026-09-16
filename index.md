# Index — Application Monitoring Peralatan Industri

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

---

## Deskripsi Produk

Aplikasi web-based berbasis *real-time monitoring* untuk memantau status 6 unit peralatan industri di lantai produksi PT Maju Teknik Industri. Dirancang untuk teknisi lapangan dan supervisor produksi, dengan fokus pada identifikasi cepat status abnormal (< 3 detik).

**Platform:** Web app (React JS) — responsive, berjalan di desktop / tablet / mobile
**Tim:** Henry, Claude
**Status:** Prototype — berjalan di local, database SQLite
**Integrasi eksternal:** Tidak ada (scope saat ini lokal saja)

---

## Dokumen PRD

| File | Audiens | Deskripsi |
|---|---|---|
| [UI_PRD.md](./UI_PRD.md) | UI Designer | Spesifikasi visual: warna, tipografi, layout, komponen, per-screen |
| [Development.md](./Development.md) | Developer | Spesifikasi teknis: tech stack, halaman, data model, state, security |
| [User_Requirements.md](./User_Requirements.md) | User / Stakeholder | Kebutuhan fungsional dari perspektif pengguna, per-fitur |

**Referensi desain awal:** [REF/UI_stitch.md](./REF/UI_stitch.md) · [REF/UI_stitch_Gemini.md](./REF/UI_stitch_Gemini.md)

---

## Screens / Halaman

| ID | Nama Layar | Tujuan | Akses |
|---|---|---|---|
| S-01 | Login | Autentikasi masuk ke sistem | Semua |
| S-02 | Dashboard | Gambaran umum status 6 mesin secara sekilas | Semua |
| S-03 | Detail Peralatan | Analisis mendalam satu mesin (parameter, trend, alarm) | Semua |
| S-04 | Daftar Alarm | Semua alarm aktif (belum resolved) dari semua mesin | Semua |
| S-05 | Form Laporan | Buat work order / laporan formal tindak lanjut | Supervisor |
| S-06 | User Management | Kelola akun teknisi, tambah mesin, checklist laporan, export data | Supervisor |

---

## Peralatan yang Dipantau

| ID Mesin | Nama | Tipe | Parameter |
|---|---|---|---|
| P-101 | Pompa Utama | Pompa | Suhu (°C), Tekanan (bar), Getaran (mm/s) |
| C-201 | Kompresor | Kompresor | Suhu (°C), Tekanan (bar), Getaran (mm/s) |
| M-301 | Motor | Motor | Suhu (°C), Beban (%), Getaran (mm/s) |
| CH-01 | Chiller | Chiller | Suhu (°C), Tekanan (bar), Beban (%) |
| G-01 | Genset | Generator | Suhu (°C), Beban (%), Tegangan (V) |
| CV-02 | Conveyor | Conveyor | Kecepatan (m/s), Beban (%), Getaran (mm/s) |

---

## Role-based Access

| Fitur | Teknisi | Supervisor |
|---|---|---|
| Dashboard, Detail, Daftar Alarm | ✓ | ✓ |
| Buat Work Order (basic) | ✓ | ✓ |
| Buat Laporan Formal (PDF) | ✗ | ✓ |
| Export PDF | ✗ | ✓ |
| User Management (S-06) | ✗ | ✓ |
| Checklist / approve laporan | ✗ | ✓ |

---

## Ringkasan Design System

- **Layout:** Responsive — desktop 1280px+ / tablet 768–1279px / mobile <768px `[ASSUMPTION]` D-024
- **Grid:** 12 kolom, margin 16 px, gutter 16 px `[REF]` D-030
- **Spacing:** 8-point grid (8, 16, 24, 32 px) `[REF]` D-030
- **Font:** Plus Jakarta Sans `[CONFIRMED]` D-020
- **Light theme:** Background `#F4F7FE` · Surface `#FFFFFF` · Primary `#4318FF` · Heading `#2B3674` · Body `#A3AED0` `[REF]` D-021
- **Dark theme:** Background `#0F172A` · Surface `#1E293B` · Primary `#818CF8` · Heading `#E2E8F0` · Body `#94A3B8` `[ASSUMPTION]` D-023
- **Status:** Normal `#22C55E` · Peringatan `#F59E0B` · Gangguan `#EF4444` `[REF]` D-022

Detail lengkap → [UI_PRD.md](./UI_PRD.md)

---

## User Flow

```
[S-01 Login]
     |
     v (Masuk)
[S-02 Dashboard] ──────────────────> [S-04 Daftar Alarm]
     |                                       |
     v (Klik kartu mesin)                    v (Klik alarm item)
[S-03 Detail Peralatan] <───────────────────┘
     |
     v (Klik "Buat Laporan") [Supervisor]
[S-05 Form Laporan]

[Nav Sidebar] → [S-06 User Management] [Supervisor]
```

---

## Tech Stack (Ringkasan)

| Layer | Pilihan |
|---|---|
| Frontend | React JS |
| Styling | Tailwind CSS |
| State Management | Zustand |
| Charting | Recharts |
| Backend | Express.js |
| Database | SQLite (better-sqlite3) |
| Auth | JWT |

Detail lengkap → [Development.md](./Development.md)

---

## Catatan Lintas-Domain

- Semua keputusan dan sumbernya → [DECISIONS.md](./DECISIONS.md)
- Item bertanda `[ASSUMPTION]` TIDAK boleh diimplementasikan sebelum dikonfirmasi user/designer
- Item bertanda `[DESIGN TBD]` menunggu Figma design file — lihat P-004 di DECISIONS.md
- Nilai threshold per parameter masih nullable — lihat P-002 di DECISIONS.md
- Template PDF laporan (S-05) belum di-lock — lihat P-001 di DECISIONS.md
- Data berjalan lokal (SQLite). Tidak ada koneksi ke server eksternal, SCADA, atau ERP.
- Notifikasi suara/getar: opsional, tidak masuk v1 — tambahkan di v2 jika diperlukan.
