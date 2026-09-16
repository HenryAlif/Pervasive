# User Requirements — Application Monitoring Peralatan Industri

Dokumen ini ditujukan untuk **User / Stakeholder**. Berisi kebutuhan fungsional dari perspektif pengguna akhir, ditulis secara deskriptif.

File ini bersifat **living document** — akan terus diperbarui seiring bertambahnya kebutuhan baru.

---

## Panduan Mengisi Dokumen Ini

Untuk setiap fitur atau kebutuhan, jelaskan:
- **Konteks:** Kapan / situasi apa fitur ini dibutuhkan?
- **Kebutuhan:** Apa yang ingin user lakukan?
- **Prioritas:** Penting (harus ada) / Sedang (diinginkan) / Rendah (nice to have)

---

## 1. Persona Pengguna

### Teknisi Lapangan

- **Peran:** Berpatroli di lantai produksi, memantau kondisi mesin secara langsung.
- **Kondisi Penggunaan:** Berjalan sambil memegang tablet dengan satu tangan, kadang di lingkungan dengan pencahayaan kurang.
- **Kebutuhan Utama:** Mengetahui mesin mana yang bermasalah secepat mungkin tanpa harus membuka halaman satu per satu.

> **Perlu Diisi:** Apakah ada persona lain? Contoh: Supervisor yang hanya melihat laporan, atau operator kontrol ruangan yang monitoring dari jarak jauh.

---

## 2. Kebutuhan Per Halaman / Fitur

### 2.1 Login

- Teknisi ingin bisa masuk ke aplikasi dengan cepat menggunakan ID dan password.
- Jika di lapangan terus-menerus menggunakan tablet yang sama, teknisi ingin opsi "Ingat Saya" agar tidak perlu login ulang setiap shift.

> **Perlu Diisi:** Apakah ada kebutuhan login dengan cara lain? (Misalnya: QR code, NFC badge, biometrik/fingerprint)

> **Perlu Diisi:** Siapa yang mengelola akun teknisi? (Admin IT, supervisor, atau self-register?)

---

### 2.2 Dashboard — Monitoring Utama

- Teknisi ingin langsung melihat kondisi semua mesin begitu aplikasi dibuka — tidak perlu navigasi ke mana-mana.
- Jika ada mesin yang berstatus peringatan atau gangguan, teknisi ingin itu langsung terlihat mencolok tanpa harus mencari-cari.
- Teknisi ingin tahu kapan data terakhir diperbarui dan apakah koneksi ke sistem masih aktif.

> **Perlu Diisi:** Apakah kartu mesin yang bermasalah perlu otomatis disoroti / dipindah ke posisi atas? Atau urutan tetap berdasarkan ID mesin?

> **Perlu Diisi:** Berapa frekuensi refresh yang diharapkan user? (Setiap 5 detik, 10 detik, real-time push?)

> **Perlu Diisi:** Apakah perlu ada suara / notifikasi getar saat ada alarm baru muncul?

---

### 2.3 Detail Peralatan

- Saat melihat mesin bermasalah, teknisi ingin tahu parameter mana yang melebihi batas normal (suhu terlalu tinggi, tekanan terlalu rendah, dll).
- Teknisi ingin melihat tren historis untuk menentukan apakah kondisi ini memburuk secara bertahap atau tiba-tiba.
- Setelah memeriksa di lapangan, teknisi ingin langsung membuat catatan / laporan dari halaman ini.

> **Perlu Diisi:** Parameter apa saja yang ditampilkan per jenis mesin? (Contoh: untuk pompa — suhu, tekanan, aliran; untuk motor — suhu, beban, getaran). Ini penting untuk pengembangan.

> **Perlu Diisi:** Berapa rentang waktu historis yang dibutuhkan? (24 jam, 1 minggu, 1 bulan?)

---

### 2.4 Daftar Alarm Global

- Teknisi atau supervisor ingin melihat semua alarm yang pernah terjadi di semua mesin dalam satu tempat.
- User ingin bisa memfilter alarm berdasarkan tingkat keparahan (peringatan vs gangguan) dan rentang waktu.
- User ingin menandai alarm yang sudah ditindaklanjuti agar mudah diketahui mana yang masih perlu perhatian.

> **Perlu Diisi:** Apakah alarm yang sudah di-resolve perlu otomatis hilang dari daftar, atau tetap terlihat dengan status "Selesai"?

> **Perlu Diisi:** Apakah ada kebutuhan export data alarm (PDF / Excel) untuk keperluan laporan harian/mingguan?

---

### 2.5 Form Laporan / Work Order

- Ketika menemukan masalah, teknisi ingin mendokumentasikan temuannya langsung dari tablet.
- Teknisi ingin bisa melampirkan foto kondisi mesin sebagai bukti.
- Laporan ini sebaiknya langsung terhubung ke mesin yang dilaporkan, bukan harus diisi ulang.

> **Perlu Diisi:** Ke mana laporan dikirim setelah disubmit? (Email supervisor, sistem tiket, database internal, dll?)

> **Perlu Diisi:** Apakah ada template laporan standar yang harus diikuti?

---

## 3. Kebutuhan Tambahan

> **Perlu Diisi:** Tuliskan di sini kebutuhan fitur apapun yang belum tercakup di atas. Format bebas — deskriptif saja.

Contoh:
- "Saya ingin ada fitur notifikasi push ke HP supervisor ketika ada mesin yang fault"
- "Perlu halaman pengaturan untuk mengubah threshold batas aman per mesin"
- "Ada kebutuhan multi-language (Indonesia + English)"

---

## 4. Yang TIDAK Termasuk dalam Scope Saat Ini

> **Perlu Diisi:** Apa yang secara eksplisit tidak perlu dikerjakan? Ini penting untuk menghindari scope creep.

Contoh:
- Manajemen user (tambah/hapus akun teknisi) — tidak di scope versi ini
- Integrasi ke sistem ERP — belum di scope
