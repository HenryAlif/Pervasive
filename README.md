# Pervasive — Aplikasi Monitoring Peralatan Industri

Proyek ini adalah aplikasi web untuk memantau kondisi mesin-mesin di lantai produksi secara real-time. Teknisi lapangan bisa langsung melihat mesin mana yang bermasalah hanya dalam hitungan detik, dan supervisor bisa membuat laporan serta mengelola tim dari satu tempat.

> **Status:** Prototype — masih dalam tahap perencanaan dan pengembangan awal.

---

## Siapa Membaca Apa?

Tergantung peranmu, buka file yang sesuai:

| Saya adalah... | File yang perlu dibaca |
|---|---|
| Orang baru / ingin kenal proyeknya | [`index.md`](./index.md) |
| UI Designer / pembuat tampilan | [`UI_PRD.md`](./UI_PRD.md) |
| Developer / programmer | [`Development.md`](./Development.md) |
| User / pengguna akhir / stakeholder | [`User_Requirements.md`](./User_Requirements.md) |
| Ingin tahu kenapa suatu keputusan diambil | [`DECISIONS.md`](./DECISIONS.md) |

---

## Struktur Folder

```
Pervasive/
│
├── README.md               ← Kamu sedang baca ini — panduan awal proyek
├── index.md                ← Ringkasan lengkap proyek: screen, mesin, tech stack, user flow
├── DECISIONS.md            ← Catatan semua keputusan penting beserta alasannya
│
├── UI_PRD.md               ← Spesifikasi tampilan: warna, font, ukuran, per-layar
├── Development.md          ← Spesifikasi teknis: bahasa program, database, komponen
├── User_Requirements.md    ← Daftar kebutuhan fitur dari sudut pandang pengguna
│
├── docs/
│   └── plans/              ← Rencana implementasi detail (untuk pengembang internal)
│
└── REF/                    ← Dokumen referensi awal (jangan diedit)
    ├── UI_stitch.md        ← Brief asli desain UI (sumber pertama)
    └── UI_stitch_Gemini.md ← Versi brief yang sudah diformat ulang
```

---

## Penjelasan Setiap File

### `index.md` — Ringkasan Proyek
Titik masuk utama untuk memahami proyek secara menyeluruh. Berisi:
- Deskripsi produk dan tujuannya
- Daftar semua halaman aplikasi (Login, Dashboard, dll)
- Daftar 6 mesin yang dipantau beserta parameternya
- Siapa yang boleh akses halaman apa (teknisi vs supervisor)
- Ringkasan desain (warna, font, layout)
- Alur penggunaan aplikasi dari awal sampai akhir

**Baca ini dulu sebelum membuka file lain.**

---

### `DECISIONS.md` — Log Keputusan
Setiap keputusan penting dalam proyek dicatat di sini: siapa yang memutuskan, dari mana dasarnya, dan apakah sudah dikonfirmasi atau masih asumsi.

Berguna untuk menjawab pertanyaan seperti: *"Kenapa pakai React?"*, *"Siapa yang pilih warna ini?"*, *"Apakah ukuran ini sudah final?"*

---

### `UI_PRD.md` — Spesifikasi Tampilan (untuk UI Designer)
Berisi semua nilai visual yang dibutuhkan designer untuk membuat desain:
- Palet warna (light mode & dark mode)
- Ukuran font, spasi, grid
- Deskripsi tiap komponen UI (badge, tombol, kartu mesin, navigasi)
- Deskripsi fungsional tiap halaman — elemen apa yang harus ada

> **Catatan penting:** Dokumen ini masih DRAFT. Bagian visual yang ditandai `[ASSUMPTION]` belum dikonfirmasi dan harus diganti dengan nilai dari Figma sebelum development dimulai.

---

### `Development.md` — Spesifikasi Teknis (untuk Developer)
Panduan teknis untuk membangun aplikasi:
- Daftar teknologi yang dipakai (React, Tailwind, SQLite, dll) beserta alasannya
- Struktur halaman dan URL routing
- Model data (struktur mesin, alarm, laporan, user)
- Daftar komponen yang perlu dibuat
- Cara autentikasi (login, JWT token)
- Catatan keamanan (apa yang perlu dilindungi)

---

### `User_Requirements.md` — Kebutuhan Pengguna
Ditulis dari sudut pandang pengguna: apa yang mereka butuhkan dari aplikasi ini. Tidak teknikal — fokus pada fungsi dan tujuan.

File ini bersifat **hidup** — akan terus diperbarui seiring bertambahnya kebutuhan baru dari pengguna.

---

### `REF/` — Dokumen Referensi
Berisi brief asli yang menjadi dasar pembuatan PRD. Hanya untuk dibaca, tidak untuk diedit.

- `UI_stitch.md` — brief desain asli dalam format teks
- `UI_stitch_Gemini.md` — versi yang sudah diformat ulang dengan Markdown yang lebih rapi

---

### `docs/plans/` — Rencana Implementasi
Berisi file-file perencanaan teknis yang digunakan selama proses development. Ini dokumen internal untuk pengembang.

---

## Tentang Status Markers

Di dalam dokumen PRD, setiap informasi diberi label untuk menunjukkan seberapa pasti nilainya:

| Label | Artinya |
|---|---|
| `[CONFIRMED]` | Sudah diputuskan langsung oleh user — aman untuk diimplementasi |
| `[REF]` | Diambil dari dokumen referensi — perlu validasi sebelum production |
| `[ASSUMPTION]` | Perkiraan/pilihan sementara — **HARUS dikonfirmasi** sebelum desain dibuat |
| `[DESIGN TBD]` | Menunggu file desain dari designer (Figma) — belum bisa diisi |

Jika kamu melihat `[ASSUMPTION]` di suatu nilai, jangan implementasikan sampai ada konfirmasi.

---

## Tech Stack Singkat

| Bagian | Teknologi |
|---|---|
| Frontend (tampilan) | React JS + Tailwind CSS |
| State management | Zustand |
| Grafik & chart | Recharts |
| Backend (server) | Express.js |
| Database | SQLite (berjalan di lokal) |
| Login & auth | JWT |

---

## Catatan Penting

- Proyek ini saat ini **hanya berjalan di komputer lokal** — bukan di server atau cloud
- Data tersimpan di database lokal (SQLite), tidak terhubung ke sistem eksternal manapun
- Beberapa bagian masih dalam tahap diskusi dan belum final — lihat [`DECISIONS.md`](./DECISIONS.md) untuk detail
