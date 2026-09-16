# User Requirements — Application Monitoring Peralatan Industri

Dokumen ini ditujukan untuk **User / Stakeholder**. Berisi kebutuhan fungsional dari perspektif pengguna akhir, ditulis secara deskriptif.

File ini bersifat **living document** — akan terus diperbarui seiring bertambahnya kebutuhan baru.

---

## Panduan Mengisi Dokumen Ini

Untuk setiap fitur atau kebutuhan baru, jelaskan:
- **Konteks:** Kapan / situasi apa fitur ini dibutuhkan?
- **Kebutuhan:** Apa yang ingin user lakukan?
- **Prioritas:** Penting (harus ada) / Sedang (diinginkan) / Rendah (nice to have)

---

## 1. Persona Pengguna

### Teknisi Lapangan

- **Peran:** Berpatroli di lantai produksi, memantau kondisi mesin secara langsung.
- **Kondisi Penggunaan:** Berjalan sambil memegang tablet atau ponsel dengan satu tangan, kadang di lingkungan dengan pencahayaan kurang atau terlalu terang karena matahari langsung.
- **Kebutuhan Utama:** Mengetahui mesin mana yang bermasalah secepat mungkin tanpa harus membuka halaman satu per satu.

### Supervisor Produksi

- **Peran:** Mengawasi kondisi keseluruhan area produksi, bertanggung jawab atas tindak lanjut masalah dan pelaporan formal.
- **Kondisi Penggunaan:** Umumnya dari ruang kontrol atau kantor, bisa juga di lapangan.
- **Kebutuhan Utama:** Membuat laporan formal, mengapprove work order dari teknisi, memantau seluruh history alarm, mengelola akun pengguna.

---

## 2. Kebutuhan Per Halaman / Fitur

### 2.1 Login

**Prioritas: Penting**

- Teknisi ingin bisa masuk ke aplikasi dengan cepat menggunakan ID dan password.
- Jika di lapangan menggunakan tablet yang sama terus-menerus, teknisi ingin opsi "Ingat Saya" agar tidak perlu login ulang setiap shift.
- Akun teknisi dibuat dan dikelola oleh supervisor — tidak ada self-register.
- Metode login: hanya ID + password (tidak ada QR code, NFC, atau biometrik).

---

### 2.2 Dashboard — Monitoring Utama

**Prioritas: Penting**

- Teknisi ingin langsung melihat kondisi semua mesin begitu aplikasi dibuka — tidak perlu navigasi ke mana-mana.
- Jika ada mesin yang berstatus peringatan atau gangguan, kartu mesin tersebut harus otomatis naik ke posisi paling atas grid dan terlihat mencolok dengan warna sesuai statusnya.
- Teknisi ingin tahu kapan data terakhir diperbarui dan apakah koneksi ke sistem masih aktif.
- Data diperbarui setiap 10 detik (polling) — cukup untuk prototype tanpa membebani sisi development.
- Notifikasi suara/getar: **tidak termasuk v1**, bisa ditambahkan di versi berikutnya.

---

### 2.3 Detail Peralatan

**Prioritas: Penting**

- Saat melihat mesin bermasalah, teknisi ingin tahu parameter mana yang melebihi batas normal.
- Teknisi ingin melihat tren historis untuk menentukan apakah kondisi memburuk secara bertahap atau tiba-tiba.
- Rentang waktu historis yang tersedia: **24 jam / 1 minggu / 1 bulan**.
- Setelah memeriksa di lapangan, supervisor ingin langsung membuat catatan / laporan dari halaman ini.

**Parameter yang ditampilkan per mesin:**

| Mesin | Parameter |
|---|---|
| P-101 Pompa Utama | Suhu (°C), Tekanan (bar), Getaran (mm/s) |
| C-201 Kompresor | Suhu (°C), Tekanan (bar), Getaran (mm/s) |
| M-301 Motor | Suhu (°C), Beban (%), Getaran (mm/s) |
| CH-01 Chiller | Suhu (°C), Tekanan (bar), Beban (%) |
| G-01 Genset | Suhu (°C), Beban (%), Tegangan (V) |
| CV-02 Conveyor | Kecepatan (m/s), Beban (%), Getaran (mm/s) |

---

### 2.4 Daftar Alarm Global

**Prioritas: Penting**

- Teknisi dan supervisor ingin melihat semua alarm aktif (belum resolved) dari semua mesin dalam satu tempat.
- User ingin bisa memfilter alarm berdasarkan keparahan (peringatan vs gangguan) dan rentang waktu.
- Alarm yang sudah ditindaklanjuti (resolved) **hilang dari daftar ini** — hanya alarm aktif yang tampil. Riwayat alarm bisa dilihat per mesin di halaman Detail.
- Supervisor ingin bisa **export daftar alarm sebagai PDF** untuk keperluan laporan.

---

### 2.5 Form Laporan / Work Order

**Prioritas: Penting (Supervisor)**

- Ketika menemukan masalah, supervisor ingin mendokumentasikan temuannya secara formal dari aplikasi.
- Laporan harus otomatis terhubung ke mesin yang dilaporkan (tidak perlu isi ulang ID mesin).
- Supervisor ingin bisa melampirkan foto kondisi mesin sebagai bukti.
- Laporan tersimpan di database lokal.
- Output laporan dalam format **PDF** — template dan format detail akan didiskusikan terpisah (TODO).

---

### 2.6 User Management (S-06)

**Prioritas: Penting (Supervisor)**

- Supervisor ingin bisa mendaftarkan akun teknisi baru (nama, ID, password awal).
- Supervisor ingin bisa menonaktifkan akun teknisi yang sudah tidak aktif.
- Supervisor ingin bisa melihat status laporan yang masuk dan melakukan approve atau reject.
- Supervisor ingin bisa export data untuk keperluan reporting.

---

## 3. Kebutuhan Tambahan

*(Isi bagian ini saat ada kebutuhan baru yang belum tercakup di atas)*

---

## 4. Yang TIDAK Termasuk dalam Scope Saat Ini

- **Notifikasi push / suara / getar** → opsional, masuk v2 jika diperlukan
- **Integrasi ke sistem ERP atau SCADA** → belum di scope
- **Threshold per parameter** → belum ditentukan, menunggu data dari pengujian sensor. Saat ini field threshold nullable.
- **Template PDF laporan** → belum di-lock, akan dibahas terpisah
- **Multi-language** → belum di scope, default Indonesia
- **Deployment ke server / cloud** → saat ini aplikasi berjalan di local saja (prototype)
- **Manajemen user oleh admin IT** → supervisor yang mengelola akun
