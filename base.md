Sistem antarmuka **Pervasive** dirancang dengan pendekatan *Human-Centered Design* berstandar industri, memprioritaskan efisiensi kognitif, kejelasan hirarki visual, serta kecepatan pengambilan keputusan saat penanganan kendala teknis di lapangan.

---

### 1. `01_Daftar_Alarm_Global.png` — Center Monitoring & Log Alarm

* **Ide & Konsep UX**: Layar ini berfungsi sebagai *supervisory layer* untuk memantau seluruh anomali mesin secara terpusat. Pendekatannya menerapkan prinsip *progressive disclosure*—menyajikan ringkasan metrik tingkat tinggi di atas, lalu mendistribusikan detail insiden dalam bentuk tabel berprioritas untuk mencegah *cognitive overload* pada operator.
* **Fungsi Utama**:
* **Ringkasan KPI Teratas**: Menampilkan jumlah total alarm aktif, gangguan kritis, peringatan, serta metrik *Mean Time to Acknowledge* (MTTA) untuk memantau responsivitas pemeliharaan.
* **Filter Multilapis & Pencarian**: Memungkinkan pemfilteran cepat berdasarkan tingkat keparahan (*Kritis/Peringatan*), unit mesin, rentang waktu, serta kolom pencarian ID parameter.
* **Tabel Status Keterpaparan Telemetri**: Menyajikan data *real-time* nilai terbaca versus batas ambang (*threshold*) dengan sistem pengodean warna (*severity color-coding*) kontras tinggi.
* **Aksi Massal (Batch Operations Bar)**: *Floating bar* di bagian bawah memudahkan *Supervisor* untuk melakukan konfirmasi (*acknowledge*) atau penyelesaian insiden secara sekaligus.



---

### 2. `02_Buat_Laporan_Insiden.png` — Form Penerbitan Work Order

* **Ide & Konsep UX**: Dirancang sebagai formulir pembuatan perintah kerja (*Work Order*) teknis yang presisi. Pola tata letak memisahkan antara konteks data telemetri otomatis (sisi atas & kanan) dengan input manual teknisi (sisi kiri) guna memastikan seluruh laporan tervalidasi oleh data aktual sebelum diterbitkan.
* **Fungsi Utama**:
* **Header Konteks Mesin**: Menampilkan data *live telemetry* saat insiden terjadi (suhu, getaran, lokasi fisik) sebagai acuan dasar penanganan.
* **Matriks Prioritas SLA**: Tombol seleksi prioritas visual (P1 Urgent, P2 Tinggi, P3 Sedang) yang langsung menampilkan batas target waktu respons *SLA*.
* **Upload & Management Media**: Komponen *drag-and-drop* untuk melampirkan foto inspeksi fisik dan citra termal FLIR sebagai bukti validasi kondisi mesin.
* **Integrasi Output Dokumentasi**: Panel status penerbitan otomatis dokumen WO ke sistem ERP Maintenance, notifikasi darurat multi-kanal, dan penguncian status mesin di SCADA.



---

### 3. `03_Verifikasi_Otorisasi_Laporan.png` — Modal Decision Supervisor

* **Ide & Konsep UX**: Menggunakan pola *Modal Dialog* berpenerangan terisolasi (*dark backdrop overlay*) untuk menarik fokus penuh *Supervisor* saat mengambil keputusan krusial. Desain ini menyandingkan bukti data teknis dengan kontrol otorisasi secara *side-by-side* untuk mempercepat verifikasi tanpa kehilangan konteks.
* **Fungsi Utama**:
* **Validasi Silang Telemetri & Media**: Menyandingkan anomali angka sensor terkini dengan bukti foto fisik dan peta panas (*thermal hotspot*) secara langsung.
* **Alur Keputusan Terstruktur**: Opsi tombol radio tegas untuk memilih tindakan (*Setujui & Terbitkan SPK*, *Minta Revisi*, atau *Tolak*) guna menghindari batasan ambigu.
* **Pengaturan Alokasi Downtime**: *Input field* khusus untuk membatasi durasi *Emergency Shut-off* yang diizinkan pada lini produksi.
* **Audit Trail & Otentikasi Digital**: Mengunci identitas penandatangan, peran *Supervisor*, alamat IP, dan opsi otomatisasi pengiriman data ke sistem ERP SAP.



---

### 4. `04_Login_Portal_Autentikasi.png` — Gerbang Akses Sistem

* **Ide & Konsep UX**: Antarmuka autentikasi berpendekatan *Clean & Secure Design*. Tata letak terpusat (*centered card layout*) memberikan rasa aman, minim gangguan, serta dioptimalkan untuk pengoperasian pada layar komputer industri maupun tablet lapangan.
* **Fungsi Utama**:
* **Indikator Keamanan & Node**: Status badge *real-time* ("NODE CKR-04 ONLINE" dan enkripsi "TLS 1.3") memberikan kepastian konektivitas sistem yang aman.
* **Formulir Kredensial Ergonomis**: Input *User ID* dan *Kata Sandi* dilengkapi fitur *visibility toggle* untuk meminimalkan kesalahan ketik pengguna di lingkungan pabrik.
* **Informasi Hak Akses & Bantuan**: Modul pemberitahuan tingkat akses operasional serta tautan bantuan cepat jika terjadi kendala akun.
* **Telemetri Koneksi Sistem**: Memuat informasi ID Stasiun perangkat dan indikator *latency* jaringan dalam satuan milidetik (ms).



---

### 5. `05_Ringkasan_Operasional_Pabrik.png` — Dashboard Monitoring Utama

* **Ide & Konsep UX**: Berfungsi sebagai pusat kendali (*Control Room Display*) berarsitektur *Bento-Grid*. Halaman ini menyajikan gambaran umum (*helicopter view*) atas seluruh aset operasional pabrik agar *Supervisor* dapat mengidentifikasi unit yang mengalami deviasi dalam hitungan detik.
* **Fungsi Utama**:
* **Ringkasan Status Aset**: Card statistik utama yang mengelompokkan unit mesin ke dalam kategori *Beroperasi Normal*, *Perlu Perhatian*, dan *Gangguan Kritis*.
* **Grid Unit Mesin Modular**: Setiap kartu mesin menampilkan parameter krusial (suhu, tekanan, getaran) lengkap dengan grafik tren mini (*sparkline*) 30 menit terakhir.
* **Indikator Visual & Akses Cepat**: Kartu berpendar merah/kuning sesuai tingkat urgensi insiden, dilengkapi tombol navigasi langsung (*Investigasi*, *Inspeksi*, atau *Atur Kapasitas*).
* **Tabel Alarm Darurat**: Menampilkan daftar insiden yang belum ditangani di bagian bawah layar untuk mengeksekusi tindakan cepat (*Quick Action*).



---

### 6. `06_Detail_Unit_Telemetri.png` — Diagnostik Spesifik Unit

* **Ide & Konsep UX**: Layar analisis mendalam (*deep-dive diagnostics page*) yang berfokus pada satu mesin spesifik. Menggabungkan data telemetri historis, spesifikasi mekanis, serta rekaman insiden untuk mendukung keputusan *Predictive Maintenance*.
* **Fungsi Utama**:
* **Radial Gauge Parameters**: Meteran visual melingkar yang menampilkan tingkat persentase beban sensor aktual terhadap batas maksimum toleransi aman.
* **Grafik Tren Multivariat**: Chart interaktif berresolusi tinggi yang memetakan korelasi antara dua parameter (Suhu vs Getaran) terhadap garis batas toleransi kritis.
* **Panel Spesifikasi & Manual**: Modul informasi teknis aset mencakup foto fisik unit, ID tag, kapasitas daya, tanggal servis terakhir, serta akses ke buku catatan pemeliharaan.
* **Riwayat Peristiwa Kritis**: Tabel histori penyimpangan parameter operasional mesin yang dilengkapi tombol penanganan lanjutan atau peninjauan *log*.