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

---

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

---

## Design System

| ID | Keputusan | Sumber | Status |
|---|---|---|---|
| D-020 | Font: Plus Jakarta Sans | CONFIRMED — user input | 2026-09-16 |
| D-021 | Light theme palette (BG `#F4F7FE`, Primary `#4318FF`, Heading `#2B3674`, Body `#A3AED0`) | REF — UI_stitch.md BloomBoost | Perlu validasi user/designer |
| D-022 | Status colors (`#22C55E` / `#F59E0B` / `#EF4444`) | REF — UI_stitch.md + UI_stitch_Gemini.md | Perlu validasi user/designer |
| D-023 | Dark theme palette (BG `#0F172A`, Surface `#1E293B`, Primary `#818CF8`, Heading `#E2E8F0`, Body `#94A3B8`) | **ASSUMPTION — Claude** | ⚠️ Belum dikonfirmasi — butuh input user/designer |
| D-024 | Responsive breakpoints (desktop 1280px+, tablet 768–1279px, mobile <768px) | **ASSUMPTION — Claude** | ⚠️ Belum dikonfirmasi — butuh konfirmasi user |
| D-025 | Equipment card grid: 2 kolom × 3 baris (adjustable) | CONFIRMED — user input | 2026-09-16 |
| D-026 | Navigation: side nav desktop/tablet, hamburger/bottom nav mobile | **ASSUMPTION — Claude** | ⚠️ Belum dikonfirmasi — butuh konfirmasi user/designer |
| D-027 | Badge text color: putih `#FFFFFF` pada semua status variant | **ASSUMPTION — Claude** (berdasar contrast ratio WCAG AA) | ⚠️ Perlu validasi designer |
| D-028 | Button border radius: 8px | **ASSUMPTION — Claude** | ⚠️ Belum dikonfirmasi — butuh nilai dari design system |
| D-029 | Touch target minimum: 48 × 48 px | REF — UI_stitch.md | Perlu validasi user/designer |
| D-030 | Spacing: 8-point grid (8/16/24/32 px), grid 12 kolom, margin 16px, gutter 16px | REF — UI_stitch.md | Perlu validasi user/designer |

---

## Pending Decisions (Belum Diputuskan)

| ID | Topik | Butuh Input Dari | Catatan |
|---|---|---|---|
| P-001 | Template & format PDF laporan (S-05) | User / Designer | Brainstorm terpisah dijadwalkan |
| P-002 | Nilai threshold per parameter per mesin | User / Engineering | Menunggu data dari pengujian sensor |
| P-003 | Logo / branding visual app | User / Designer | Placeholder OK untuk prototype |
| P-004 | Desain visual aktual (Figma) — semua screen | Designer | Belum ada; UI_PRD.md Section 3 adalah functional spec, bukan visual spec |
| P-005 | Validasi dark mode palette (D-023) | User / Designer | Claude memilih warna, belum disetujui |
| P-006 | Validasi responsive breakpoints (D-024) | User | Claude mengasumsikan standar industri |

---

## Cara Membaca Dokumen Ini

- **CONFIRMED:** Keputusan sudah final, boleh langsung diimplementasikan
- **REF:** Dari dokumen referensi, perlu validasi sebelum design handoff
- **ASSUMPTION:** Claude yang memilih — HARUS diganti dengan nilai yang dikonfirmasi sebelum development visual dimulai
- **Pending (P-xxx):** Belum ada keputusan sama sekali — jangan diimplementasikan
