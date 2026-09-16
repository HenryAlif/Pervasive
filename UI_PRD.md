# UI PRD — Application Monitoring Peralatan Industri

Dokumen ini ditujukan untuk **UI Designer**. Berisi semua spesifikasi visual yang dibutuhkan untuk membuat desain yang konsisten dan sesuai standar produk.

---

## 1. Design Tokens

### 1.1 Warna

#### UI Colors

| Token | Hex | Penggunaan |
|---|---|---|
| `color-background` | `#F4F7FE` | Latar belakang halaman |
| `color-surface` | `#FFFFFF` | Latar kartu / panel |
| `color-primary` | `#4318FF` | Aksen utama, tombol primary, link aktif |
| `color-text-heading` | `#2B3674` | Teks judul, heading |
| `color-text-body` | `#A3AED0` | Teks sekunder, label, caption |

#### Status / Alarm Colors

| Token | Hex | Penggunaan |
|---|---|---|
| `color-status-normal` | `#22C55E` | Status beroperasi / normal |
| `color-status-warning` | `#F59E0B` | Status peringatan |
| `color-status-fault` | `#EF4444` | Status gangguan / fault |

> **Perlu Diisi:** Warna untuk teks di atas badge status (putih atau hitam pekat per badge) — pastikan contrast ratio memenuhi WCAG AA.

> **Perlu Diisi:** Apakah ada kebutuhan dark mode? Jika ya, tentukan pasangan warna dark theme di sini.

### 1.2 Tipografi

| Token | Font | Size | Weight | Penggunaan |
|---|---|---|---|---|
| `text-title` | Plus Jakarta Sans | 24–32 px | Bold (700) | Judul halaman, nama mesin |
| `text-body` | Plus Jakarta Sans | 16 px | Regular (400) | Konten utama, deskripsi |
| `text-caption` | Plus Jakarta Sans | 12–14 px | Regular / Medium | Label, timestamp, unit parameter |

> **Perlu Diisi:** Apakah font Plus Jakarta Sans sudah tersedia di environment desain? Alternatif fallback: Inter atau Roboto.

### 1.3 Spacing (8-Point Grid)

| Token | Value | Penggunaan |
|---|---|---|
| `space-xs` | 8 px | Gap antar elemen dalam kartu |
| `space-sm` | 16 px | Padding internal kartu, margin grid |
| `space-md` | 24 px | Jarak antar seksi |
| `space-lg` | 32 px | Jarak antar kartu / blok besar |

### 1.4 Ukuran & Layout

| Item | Nilai |
|---|---|
| Ukuran kanvas | 1280 × 800 px (Landscape) |
| Grid kolom | 12 kolom |
| Margin | 16 px |
| Gutter | 16 px |
| Touch target minimum | 48 × 48 px |

---

## 2. Komponen UI

### 2.1 Status Badge

Digunakan di kartu mesin dan header detail peralatan.

| Variant | Warna BG | Label |
|---|---|---|
| `Normal` | `#22C55E` | "Beroperasi" |
| `Warning` | `#F59E0B` | "Peringatan" |
| `Fault` | `#EF4444` | "Gangguan" |

- Ukuran: min 48 px tinggi, padding horizontal 12 px
- Teks: bold, ukuran 12–14 px
- Pastikan teks kontras di atas warna badge

### 2.2 Button

| Variant | BG | Teks | Penggunaan |
|---|---|---|---|
| `Primary` | `#4318FF` | Putih | Aksi utama ("Masuk", "Buat Laporan") |
| `Secondary` | Transparan + border | `#4318FF` | Aksi sekunder |
| `Disabled` | `#A3AED0` | Putih | Tombol tidak aktif |

- Tinggi: 48 px
- Border radius: sesuai preferensi desainer

> **Perlu Diisi:** Apakah ada variant button lain yang diperlukan (destructive/danger, ghost, icon-only)?

### 2.3 Equipment Card (Kartu Mesin)

Digunakan di grid Dashboard (6 kartu).

Elemen dalam satu kartu:
- **Nama Mesin** (text-title)
- **ID Mesin** (text-caption, `color-text-body`)
- **Status Badge** (Normal / Warning / Fault)
- **Parameter Utama** — 2–3 nilai singkat, contoh: `Temp: 78°C`, `Press: 2.4 bar`
- **Sparkline / Mini Trendline** — grafik garis kecil sebagai indikator tren

> **Perlu Diisi:** Ukuran kartu yang diinginkan dalam grid (3 kolom × 2 baris, atau 2 kolom × 3 baris?)

### 2.4 Navigation

- Tipe: Bottom Navigation atau Side Navigation (pilih salah satu)
- Item: Dashboard · Detail Mesin · Daftar Alarm · Pengaturan
- Touch target per item: min 48 px

> **Perlu Diisi:** Preferensi bottom nav atau side nav? Side nav lebih cocok untuk landscape tablet.

---

## 3. Spesifikasi Per Layar

### S-01 — Login

**Tujuan:** Autentikasi teknisi sebelum masuk ke sistem.

**Elemen UI:**
- Logo / App Branding PT Maju Teknik Industri (posisi: tengah-atas atau kiri)
- Field: ID Teknisi (min height 48 px)
- Field: Password (min height 48 px, dengan toggle show/hide)
- Checkbox: "Ingat Saya"
- Link: "Lupa Password"
- Button Primary: "Masuk / Login" (lebar penuh atau fixed width)

**State yang perlu didesain:**
- Default (kosong)
- Filled (ada input)
- Error (ID/password salah)
- Loading (saat proses autentikasi)

> **Perlu Diisi:** Apakah ada logo resmi perusahaan atau placeholder boleh digunakan?

---

### S-02 — Dashboard Monitoring

**Tujuan:** Overview kondisi semua mesin dalam < 3 detik.

**Layout (dari atas ke bawah):**
1. **Header Bar** — Nama teknisi · Waktu diperbarui · Indikator koneksi
2. **KPI Summary Bar** — 4 angka: Total (6) · Normal (n) · Peringatan (n) · Gangguan (n)
3. **Grid Kartu Mesin** — 6 kartu (P-101, C-201, M-301, CH-01, G-01, CV-02)
4. **Panel Alarm Aktif** — 3–5 alarm terbaru
5. **Navigation** — Bottom/side nav

**Hirarki visual:** Kartu dengan status Fault/Warning harus muncul lebih menonjol (warna border, ukuran badge, atau urutan grid).

> **Perlu Diisi:** Urutan prioritas tampilan kartu — apakah kartu fault otomatis naik ke atas, atau posisi tetap?

---

### S-03 — Detail Peralatan

**Tujuan:** Analisis mendalam satu mesin.

**Elemen UI:**
- Header: Nama mesin + ID + Status Badge (besar)
- Widget parameter: Suhu · Tekanan · Getaran · Beban — tampilkan sebagai gauge atau card
- Grafik tren interaktif: switch antara 24 jam / 1 minggu, tampilkan threshold line
- Tabel riwayat alarm: kolom Tanggal, Waktu, Parameter, Nilai, Status
- Button Primary: "Buat Laporan / Work Order"

> **Perlu Diisi:** Threshold (batas aman) per parameter dan per mesin — nilai ini harus muncul di grafik sebagai garis referensi.

---

### S-04 — Daftar Alarm Global

**Tujuan:** Semua alarm dari semua mesin, bisa difilter.

**Elemen UI:**
- Filter Bar: Keparahan (All / Peringatan / Gangguan) · Rentang Waktu
- Tabel: Timestamp · ID Mesin · Nama Mesin · Parameter · Nilai · Status Resolusi
- Per baris: Quick action — "Tandai Dibaca" / "Aksi Lanjut"

> **Perlu Diisi:** Apakah tabel ini perlu pagination atau infinite scroll?

---

### S-05 — Form Laporan (Opsional)

**Tujuan:** Form tindak lanjut / work order.

**Elemen UI:**
- Dropdown: Jenis Kerusakan
- Textarea: Catatan Teknisi
- Upload: Foto / Lampiran
- Button: Kirim Laporan

> **Perlu Diisi:** Apakah form ini perlu validasi wajib (required fields)? Field apa saja yang mandatory?

---

## 4. Interaction & Prototype Flow

```
[S-01 Login] → (Klik "Masuk") → [S-02 Dashboard]
[S-02 Dashboard] → (Klik kartu mesin) → [S-03 Detail] — transisi: Smart Animate
[S-02 Dashboard] → (Klik tab Alarm) → [S-04 Daftar Alarm]
[S-04 Daftar Alarm] → (Klik item) → [S-03 Detail]
[S-03 Detail] → (Klik "Buat Laporan") → [S-05 Form Laporan]
Semua layar anak → Back button → layar sebelumnya
```

> **Perlu Diisi:** Ada alur lain yang perlu ditambahkan? (Logout, Pengaturan, notifikasi push, dll)
