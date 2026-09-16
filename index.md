# Index — Application Monitoring Peralatan Industri

## Deskripsi Produk

Aplikasi tablet berbasis *real-time monitoring* untuk memantau status 6 unit peralatan industri di lantai produksi PT Maju Teknik Industri. Dirancang untuk digunakan oleh teknisi lapangan yang berpatroli sambil memegang tablet, dengan fokus pada identifikasi cepat status abnormal (< 3 detik).

> **Perlu Diisi:** Nama proyek resmi, versi produk, dan nama perusahaan jika berbeda dari "PT Maju Teknik Industri".

---

## Dokumen PRD

| File | Audiens | Deskripsi |
|---|---|---|
| [UI_PRD.md](./UI_PRD.md) | UI Designer | Spesifikasi visual: warna, tipografi, layout, komponen, per-screen |
| [Development.md](./Development.md) | Developer | Spesifikasi teknis: tech stack, halaman, data model, state |
| [User_Requirements.md](./User_Requirements.md) | User / Stakeholder | Kebutuhan fungsional dari perspektif pengguna, per-fitur |

---

## Screens / Halaman

| ID | Nama Layar | Tujuan |
|---|---|---|
| S-01 | Login | Autentikasi teknisi masuk ke sistem |
| S-02 | Dashboard | Gambaran umum status 6 mesin secara sekilas |
| S-03 | Detail Peralatan | Analisis mendalam satu mesin (parameter, trend, alarm) |
| S-04 | Daftar Alarm | Seluruh riwayat alarm dari semua mesin |
| S-05 | Form Laporan | Tindak lanjut / work order ketika menemukan masalah |

---

## Peralatan yang Dipantau

| ID Mesin | Nama | Tipe |
|---|---|---|
| P-101 | Pompa Utama | Pompa |
| C-201 | Kompresor | Kompresor |
| M-301 | Motor | Motor |
| CH-01 | Chiller | Chiller |
| G-01 | Genset | Generator |
| CV-02 | Conveyor | Conveyor |

> **Perlu Diisi:** Tambahkan mesin lain jika ada di luar 6 unit ini, beserta parameter yang dipantau (suhu, tekanan, getaran, beban, dll).

---

## Ringkasan Design System

- **Kanvas:** 1280 × 800 px (Tablet Landscape)
- **Grid:** 12 kolom, margin 16 px, gutter 16 px
- **Spacing:** 8-point grid (8, 16, 24, 32 px)
- **Font:** Plus Jakarta Sans
- **Warna Utama:** `#4318FF` (Indigo), Background `#F4F7FE`, Surface `#FFFFFF`
- **Warna Status:** Hijau `#22C55E` · Kuning `#F59E0B` · Merah `#EF4444`

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
     v (Klik "Buat Laporan")
[S-05 Form Laporan]
```

---

## Catatan Umum

> **Perlu Diisi:** Timeline pengerjaan, anggota tim, dan pembagian tanggung jawab (siapa yang handle design, siapa development).

> **Perlu Diisi:** Platform target (native Android/iOS, web app, atau hybrid) — ini akan mempengaruhi keputusan di Development.md.

> **Perlu Diisi:** Apakah ada integrasi ke sistem existing (SCADA, ERP, database plant)? Kalau ada, sebutkan di sini sebagai catatan lintas-domain.
