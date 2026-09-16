RODUCT REQUIREMENT DOCUMENT (PRD)
================================================================================
Nama Produk     : Application Monitoring Peralatan Industri (Tablet-based)
Target Perangkat: Tablet Landscape (1280 x 800 px / 1194 x 834 px)
Pengguna Utama  : Teknisi Lapangan PT Maju Teknik Industri
1. RINGKASAN PRODUK & TUJUAN
--------------------------------------------------------------------------------
1.1 Masalah Pengguna
Teknisi area produksi perlu memantau 6 unit peralatan utama saat berkeliling lapangan secara efisien. Tantangan utamanya adalah mengidentifikasi status abnormal dengan cepat di bawah pencahayaan atau kondisi kerja lapangan.
1.2 Solusi
Aplikasi tablet real-time monitoring yang menampilkan status seluruh mesin dalam < 3 detik melalui penggunaan warna kognitif (semantic color), kartu status yang informatif, serta navigasi responsif yang ramah sentuhan (touch target >= 48 px).
2. TARGET PENGGUNA & KARAKTERISTIK INTERAKSI
--------------------------------------------------------------------------------
* Pengguna: Teknisi & Supervisor Produksi.
* Kondisi Penggunaan: Digunakan sambil berjalan, memegang tablet dengan satu atau dua tangan.
* Prinsip UI:
  - Touch Target Minimal: 48 x 48 px untuk mencegah salah ketuk (fat-finger effect).
  - Hirarki Visual: Informasi paling mendesak (status Merah/Kuning) diletakkan di posisi dominan.
  - Spasi & Layout: Menggunakan sistem 8-point grid (8, 16, 24, 32 px) untuk konsistensi.
3. SPESIFIKASI DESAIN & DESIGN SYSTEM
--------------------------------------------------------------------------------
* Frame Size   : 1280 x 800 px (Landscape) - Gunakan preset Tablet
* Grid System  : 12 Column | Margin: 16 px, Gutter: 16 px
* Typography   : Plus Jakarta Sans | Max 3 variasi ukuran.
* Warna Latar & UI (Adaptasi BloomBoost):
  - Latar Belakang (Background) : #F4F7FE (Soft grayish-blue khas modern UI)
  - Latar Kartu (Surface/Card)  : #FFFFFF (Putih bersih dengan soft drop-shadow)
  - Warna Primary / Aksen       : #4318FF (Vibrant Indigo/Purple)
  - Teks Utama (Heading)        : #2B3674 (Dark Blue Navy)
  - Teks Sekunder (Body/Label)  : #A3AED0 (Cool Gray)
* Warna Status/Alarm (Wajib Sesuai Aturan Kognitif):
  - Beroperasi (Hijau) : #22C55E
  - Peringatan (Kuning): #F59E0B
  - Gangguan (Merah)   : #EF4444
4. STRUKTUR LAYAR & SPESIFIKASI KEBUTUHAN
--------------------------------------------------------------------------------
Layar 1: Login
* Tujuan: Autentikasi teknisi masuk ke sistem monitoring.
* Elemen UI Utama:
  - Logo Perusahaan / App Branding (PT Maju Teknik Industri).
  - Field Input: ID Teknisi & Password (ukuran input minimal tinggi 48 px).
  - Button Primary: "Masuk / Login" (48 px height).
  - Option: "Ingat Saya" / "Lupa Password".
Layar 2: Dashboard Monitoring (Layar Utama)
* Tujuan: Memberikan gambaran umum kondisi 6 mesin dalam waktu kurang dari 3 detik.
* Elemen UI Utama:
  - Header: Nama Teknisi, Waktu Terakhir Diperbarui (Real-time status), Status Koneksi.
  - KPI Summary Bar (Ringkasan): Total Peralatan (6), Normal (x), Peringatan (x), Gangguan (x).
  - Grid 6 Kartu Peralatan: P-101 (Pompa), C-201 (Kompresor), M-301 (Motor), CH-01 (Chiller), G-01 (Genset), CV-02 (Conveyor).
  - Isi Setiap Kartu: Nama mesin, ID, Badge Status Warna, Parameter Utama (misal: Temp: 78 C, Press: 2.4 bar), dan Mini Trendline (Sparkline).
  - Panel Tren / Daftar Alarm Aktif: Tampilan cepat 3-5 alarm terbaru.
  - Navigasi Utama (Bottom/Side Navigation): Dashboard, Detail Mesin, Daftar Alarm, Pengaturan.
Layar 3: Detail Peralatan
* Tujuan: Analisis mendalam ketika satu kartu peralatan diklik.
* Elemen UI Utama:
  - Header Mesin: Nama Mesin (misal: P-101 Pompa Utama), Status Badge besar.
  - Widget Parameter Lengkap: Gauges/Card untuk Suhu (C), Tekanan (bar), Getaran (mm/s), Beban (%).
  - Grafik Tren (Main Chart): Grafik garis interaktif (24 jam / 1 minggu) yang memperlihatkan ambang batas aman (threshold line).
  - Tabel Riwayat Alarm Mesin: Tanggal, Waktu, Parameter abnormal, Nilai pemicu.
  - Action Button: Button Utama "Buat Laporan / Work Order" (Warna kontras/Primary).
Layar 4: Daftar Alarm (Global)
* Tujuan: Memantau semua riwayat pemicu batas aman dari seluruh mesin.
* Elemen UI Utama:
  - Filter Bar: Filter berdasarkan Keparahan (All, Merah/Gangguan, Kuning/Peringatan) & Rentang Waktu.
  - Tabel Alarm: Kolom Timestamp, ID Mesin, Nama Mesin, Parameter Terpengaruh, Nilai, Status Resolusi.
  - Quick Action: Tombol "Tandai Dibaca" / "Aksi Lanjut".
Layar 5 (Bonus/Opsional): Buat Laporan / Pengaturan
* Tujuan: Form pengerjaan tindak lanjut ketika teknisi menemukan masalah.
* Elemen UI Utama: Form input jenis kerusakan, unggah foto/lampiran, dan catatan teknisi.
5. ALUR PROTOTYPE INTERAKTIF (USER FLOW)
--------------------------------------------------------------------------------
[Layar 1: Login] 
       |
       v (Klik "Masuk")
[Layar 2: Dashboard] ----> (Klik Tab "Alarm") ----> [Layar 4: Daftar Alarm]
       |                                                 |
       v (Klik Kartu Mesin / P-101)                      | (Klik Salah Satu Item)
[Layar 3: Detail Peralatan] <----------------------------+
       |
       v (Klik "Buat Laporan")
[Layar 5: Form Laporan (Bonus)]
6. CHECKLIST PENILAIAN TUGAS (PENERAPAN FITUR FIGMA)
--------------------------------------------------------------------------------
1. Auto Layout: Digunakan pada Kartu Peralatan, Form Input, Tabel Alarm, dan Layout Grid.
2. Components & Variants:
   - Component Status Badge (Normal, Warning, Critical).
   - Component Button (Primary, Secondary, Disabled).
3. Color Styles & Text Styles: Tersimpan rapi di panel Local Styles.
4. Interactive Prototype:
   - On Click -> Navigate to.
   - Smart Animate untuk transisi kartu ke detail.
   - Back Button berfungsi dengan baik di setiap layar anak.
7. RUBRIK PENILAIAN
--------------------------------------------------------------------------------
* Kelengkapan layar (min. 4) sesuai spesifikasi: 25%
* Penggunaan fitur Figma (Auto Layout, Component/Variant, Color Style): 25%
* Kualitas visual: hirarki, konsistensi, keterbacaan, kode warna status: 25%
* Prototype berfungsi sesuai alur: 15%
* Laporan & argumentasi keputusan desain: 10%

8. TIPS PENGERJAAN
--------------------------------------------------------------------------------
* Setup Awal: Buat Local Styles untuk warna dan teks sebelum mulai mendesain layar. Ini akan menghemat banyak waktu dan menjaga konsistensi.
* Komponen Reusable: Buat satu master component untuk "Kartu Peralatan" dan gunakan fitur properti (teks, boolean, variant) agar mudah diubah untuk 6 mesin berbeda.
* Touch Target: Pastikan semua elemen yang bisa diklik (tombol, tab navigasi, ikon back) memiliki tinggi/lebar minimal 48px agar sesuai standar tablet.
* Cek Kontras: Pastikan teks di atas badge warna (hijau, kuning, merah) dapat terbaca dengan jelas (gunakan teks putih atau hitam pekat menyesuaikan warna latar).