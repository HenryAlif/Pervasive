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

---

## 1. Design Tokens

### 1.1 Warna

#### Light Theme

| Token | Hex | Penggunaan | Source |
|---|---|---|---|
| `color-background` | `#F4F7FE` | Latar belakang halaman | `[REF]` D-021 |
| `color-surface` | `#FFFFFF` | Latar kartu / panel | `[REF]` D-021 |
| `color-primary` | `#4318FF` | Aksen utama, tombol primary, link aktif | `[REF]` D-021 |
| `color-text-heading` | `#2B3674` | Teks judul, heading | `[REF]` D-021 |
| `color-text-body` | `#A3AED0` | Teks sekunder, label, caption | `[REF]` D-021 |

#### Dark Theme

| Token | Hex | Penggunaan | Source |
|---|---|---|---|
| `color-background-dark` | `#0F172A` | Latar belakang halaman (dark) | `[ASSUMPTION]` D-023 |
| `color-surface-dark` | `#1E293B` | Latar kartu / panel (dark) | `[ASSUMPTION]` D-023 |
| `color-primary-dark` | `#818CF8` | Aksen utama (lighter indigo untuk dark bg) | `[ASSUMPTION]` D-023 |
| `color-text-heading-dark` | `#E2E8F0` | Teks judul (dark) | `[ASSUMPTION]` D-023 |
| `color-text-body-dark` | `#94A3B8` | Teks sekunder (dark) | `[ASSUMPTION]` D-023 |

#### Status / Alarm Colors (sama di light dan dark)

| Token | Hex | Penggunaan | Source |
|---|---|---|---|
| `color-status-normal` | `#22C55E` | Status beroperasi / normal | `[REF]` D-022 |
| `color-status-warning` | `#F59E0B` | Status peringatan | `[REF]` D-022 |
| `color-status-fault` | `#EF4444` | Status gangguan / fault | `[REF]` D-022 |

**Teks di atas badge status:** putih `#FFFFFF` untuk semua variant. `[ASSUMPTION]` D-027 — contrast ratio WCAG AA terpenuhi, perlu validasi designer.

### 1.2 Tipografi

| Token | Font | Size | Weight | Penggunaan | Source |
|---|---|---|---|---|---|
| `text-title` | Plus Jakarta Sans | 24–32 px | Bold (700) | Judul halaman, nama mesin | `[CONFIRMED]` D-020 |
| `text-body` | Plus Jakarta Sans | 16 px | Regular (400) | Konten utama, deskripsi | `[CONFIRMED]` D-020 |
| `text-caption` | Plus Jakarta Sans | 12–14 px | Regular / Medium (400/500) | Label, timestamp, unit parameter | `[CONFIRMED]` D-020 |

Font fallback: Inter, Roboto, system-ui. `[ASSUMPTION]` — fallback order belum dikonfirmasi.

### 1.3 Spacing (8-Point Grid)

| Token | Value | Penggunaan | Source |
|---|---|---|---|
| `space-xs` | 8 px | Gap antar elemen dalam kartu | `[REF]` D-030 |
| `space-sm` | 16 px | Padding internal kartu, margin grid | `[REF]` D-030 |
| `space-md` | 24 px | Jarak antar seksi | `[REF]` D-030 |
| `space-lg` | 32 px | Jarak antar kartu / blok besar | `[REF]` D-030 |

### 1.4 Layout & Responsive Breakpoints `[ASSUMPTION]` D-024

> ⚠️ Breakpoints di bawah adalah asumsi standar industri yang dipilih Claude.
> Harus dikonfirmasi oleh user/designer sebelum CSS ditulis. Lihat D-024 di DECISIONS.md.

Aplikasi ini adalah web app responsive — bukan fixed canvas tablet.

| Breakpoint | Range | Layout Notes | Source |
|---|---|---|---|
| Desktop | 1280px+ | Main target — side nav tetap terbuka | `[ASSUMPTION]` D-024 |
| Tablet | 768–1279px | Side nav bisa collapsible | `[ASSUMPTION]` D-024 |
| Mobile | <768px | Side nav collapse jadi hamburger menu | `[ASSUMPTION]` D-024 |

- **Grid:** 12 kolom, margin 16 px, gutter 16 px `[REF]` D-030
- **Touch target minimum:** 48 × 48 px `[REF]` D-029

---

## 2. Komponen UI

### 2.1 Status Badge

Digunakan di kartu mesin dan header detail peralatan.

| Variant | Warna BG | Label | Teks |
|---|---|---|---|
| `Normal` | `#22C55E` | "Beroperasi" | Putih `#FFFFFF` |
| `Warning` | `#F59E0B` | "Peringatan" | Putih `#FFFFFF` |
| `Fault` | `#EF4444` | "Gangguan" | Putih `#FFFFFF` |

> Teks di atas semua badge: putih `#FFFFFF`. `[ASSUMPTION]` D-027

- Ukuran: min 48 px tinggi, padding horizontal 12 px
- Teks: bold, 12–14 px

### 2.2 Button

| Variant | BG | Teks | Penggunaan |
|---|---|---|---|
| `Primary` | `#4318FF` | Putih | Aksi utama ("Masuk", "Buat Laporan") |
| `Secondary` | Transparan + border `#4318FF` | `#4318FF` | Aksi sekunder |
| `Disabled` | `#A3AED0` | Putih | Tombol tidak aktif |

- Tinggi: 48 px `[REF]` D-029
- Border radius: 8 px `[ASSUMPTION]` D-028 — ganti dengan nilai dari design system Figma

### 2.3 Equipment Card (Kartu Mesin)

Digunakan di grid Dashboard — layout **2 kolom × 3 baris** (6 kartu total). Grid harus mudah di-adjust jika jumlah mesin bertambah.

> Grid layout 2 kolom × 3 baris. `[CONFIRMED]` D-025

Elemen dalam satu kartu:
- **Nama Mesin** (text-title)
- **ID Mesin** (text-caption, `color-text-body`)
- **Status Badge** (Normal / Warning / Fault)
- **Parameter Utama** — 2–3 nilai, contoh: `Suhu: 78°C`, `Tekanan: 2.4 bar`
- **Sparkline / Mini Trendline** — grafik garis kecil sebagai indikator tren

**Hirarki visual darurat:** Kartu dengan status Fault atau Warning harus terlihat lebih mencolok (border warna sesuai status, atau glow effect ringan).

### 2.4 Navigation

**Desktop/Tablet (768px+):** Side Navigation (vertikal di kiri) `[ASSUMPTION]` D-026
**Mobile (<768px):** Collapse menjadi hamburger menu atau bottom nav `[ASSUMPTION]` D-026
> Konfirmasi preferensi nav sebelum implementasi. Lihat D-026 di DECISIONS.md.

**Nav Items (urutan):**
1. Dashboard (S-02)
2. Daftar Alarm (S-04)
3. User Management (S-06) — *tampil hanya untuk Supervisor*
4. Pengaturan

Touch target per item: min 48 px tinggi.

---

---

> **Penting:** Section ini berisi **Functional Requirements** — elemen apa saja yang
> harus ada di setiap layar dan apa fungsinya. Ini BUKAN visual spec.
>
> Visual layout, spacing exact, posisi elemen, dan styling akan didefinisikan setelah
> Figma design diterima. Jangan gunakan section ini sebagai panduan visual tanpa
> design file dari designer. `[DESIGN TBD]` P-004

## 3. Spesifikasi Per Layar

### S-01 — Login

**Tujuan:** Autentikasi sebelum masuk ke sistem.

**Elemen UI:**
- Logo / App Branding PT Maju Teknik Industri (placeholder boleh digunakan)
- Field: ID Teknisi (min height 48 px)
- Field: Password (min height 48 px, toggle show/hide)
- Checkbox: "Ingat Saya"
- Link: "Lupa Password"
- Button Primary: "Masuk / Login"

**State yang perlu didesain:**
- Default (kosong)
- Filled (ada input)
- Error (ID/password salah) — tampilkan pesan error merah
- Loading (proses autentikasi) — disable button + spinner

---

### S-02 — Dashboard Monitoring

**Tujuan:** Overview kondisi semua mesin dalam < 3 detik.

**Layout (dari atas ke bawah):**
1. **Header Bar** — Nama user yang login · Waktu diperbarui · Indikator koneksi
2. **KPI Summary Bar** — 4 angka: Total (6) · Normal (n) · Peringatan (n) · Gangguan (n)
3. **Grid Kartu Mesin** — 2 kolom × 3 baris, auto-sort: Fault di atas, Warning tengah, Normal bawah
4. **Panel Alarm Aktif** — 3–5 alarm terbaru (yang belum resolved)
5. **Side Navigation**

**Sorting kartu:** Kartu dengan status Fault otomatis naik paling atas, disusul Warning, lalu Normal.

---

### S-03 — Detail Peralatan

**Tujuan:** Analisis mendalam satu mesin.

**Elemen UI:**
- Header: Nama mesin + ID + Status Badge (besar)
- Widget parameter: tampilkan sebagai gauge atau value card per parameter
- Grafik tren interaktif: switch 24 jam / 1 minggu / 1 bulan, tampilkan threshold line (nullable jika belum ada nilai)
- Tabel riwayat alarm: kolom Tanggal, Waktu, Parameter, Nilai, Status
- Button Primary: "Buat Laporan / Work Order" (visible untuk Supervisor saja)

**Parameter per mesin:**

| Mesin | Parameter |
|---|---|
| P-101 Pompa | Suhu (°C), Tekanan (bar), Getaran (mm/s) |
| C-201 Kompresor | Suhu (°C), Tekanan (bar), Getaran (mm/s) |
| M-301 Motor | Suhu (°C), Beban (%), Getaran (mm/s) |
| CH-01 Chiller | Suhu (°C), Tekanan (bar), Beban (%) |
| G-01 Genset | Suhu (°C), Beban (%), Tegangan (V) |
| CV-02 Conveyor | Kecepatan (m/s), Beban (%), Getaran (mm/s) |

**Historical range:** 24 jam / 1 minggu / 1 bulan

---

### S-04 — Daftar Alarm Global

**Tujuan:** Semua alarm aktif (belum resolved) dari semua mesin.

**Elemen UI:**
- Filter Bar: Keparahan (All / Peringatan / Gangguan) · Rentang Waktu
- Tabel: Timestamp · ID Mesin · Nama Mesin · Parameter · Nilai · Status
- Per baris: Quick action — "Tandai Selesai"
- Button Export: "Export PDF" (Supervisor only)

**Catatan:** Alarm yang sudah di-resolve hilang dari daftar ini. Riwayat alarm (sudah resolved) bisa dilihat di S-03 Detail per mesin.

---

### S-05 — Form Laporan / Work Order

**Tujuan:** Buat laporan formal dan work order (Supervisor only).

**Elemen UI:**
- Pre-filled: ID Mesin, Nama Mesin (dari context mesin yang dipilih)
- Dropdown: Jenis Kerusakan
- Textarea: Catatan / Deskripsi Temuan
- Upload: Foto / Lampiran
- Button: "Kirim Laporan" → simpan ke database lokal
- Output: PDF laporan (format dan template — TODO, brainstorm terpisah)

---

### S-06 — User Management

**Tujuan:** Supervisor mengelola akun teknisi dan konfigurasi sistem. (Supervisor only)

**Elemen UI:**

**Sub-section: Kelola Teknisi**
- Tabel daftar teknisi: ID, Nama, Role, Status akun (aktif/nonaktif), Terakhir login
- Button: "Tambah Teknisi" → form input nama, ID, password awal
- Per baris: Edit · Nonaktifkan

**Sub-section: Kelola Mesin**
- Tabel daftar mesin: ID, Nama, Tipe, Status, Parameter yang dipantau
- Button: "Tambah Mesin" → form input ID, nama, tipe, parameter

**Sub-section: Checklist Laporan**
- Daftar laporan yang masuk (dari S-05), status: Menunggu / Disetujui / Ditolak
- Per laporan: Lihat detail · Approve · Reject dengan catatan

**Sub-section: Export Data**
- Export daftar alarm (by rentang waktu) sebagai PDF
- Export daftar laporan sebagai PDF

---

## 4. Interaction & Prototype Flow

```
[S-01 Login] → (Masuk) → [S-02 Dashboard]
[S-02 Dashboard] → (Klik kartu mesin) → [S-03 Detail]
[S-02 Dashboard] → (Nav: Alarm) → [S-04 Daftar Alarm]
[S-04 Daftar Alarm] → (Klik item) → [S-03 Detail]
[S-03 Detail] → (Klik "Buat Laporan") [Supervisor] → [S-05 Form Laporan]
[Nav Sidebar] → (User Management) [Supervisor] → [S-06 User Management]
Semua layar → Back / Nav → layar sebelumnya
```
