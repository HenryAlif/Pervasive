# Design Rationale — Pervasive

Dokumen ini adalah catatan desain (*design rationale*) untuk enam mockup yang ada di folder ini. Bukan sekadar deskripsi "apa yang terlihat", tapi penjelasan *kenapa* setiap keputusan visual dan interaksi diambil — supaya saat masuk ke Figma, keputusan itu bisa dipertahankan secara sadar, bukan ditiru begitu saja.

Konteks pengguna sistem ini bukan pengguna kantoran biasa: teknisi yang berjalan di lantai produksi dengan tangan kadang kotor atau memakai sarung tangan, dan supervisor yang harus mengambil keputusan cepat atas insiden mesin yang punya konsekuensi fisik nyata (downtime, risiko kerusakan, biaya perbaikan). Setiap pilihan desain di bawah ini — warna, hirarki, kepadatan informasi — ditarik dari kebutuhan itu, bukan dari estetika semata.

---

## 1. `S-01 Login — Masuk Sistem.png`

**Ide & Latar Belakang**
Login bukan sekadar gerbang akses — di lingkungan industri, ini adalah titik pertama di mana pengguna memastikan dia terhubung ke *node* dan jaringan yang benar sebelum bertindak atas data mesin yang kritis. Karena itu layar ini tidak hanya menyajikan form username/password, tapi juga status koneksi sistem secara eksplisit.

**Konsep Visual & Interaksi**
Kartu login diletakkan di tengah kanvas dengan banyak *whitespace* di sekelilingnya — pendekatan ini sengaja dibuat tenang dan tidak ramai, karena ini satu-satunya layar di seluruh aplikasi yang tidak butuh kepadatan data tinggi. Status "NODE CKR-04 ONLINE" dan "TLS 1.3 Aktif" ditempatkan di baris paling atas kartu, sebelum judul — artinya status koneksi dianggap lebih penting dibaca lebih dulu daripada identitas form itu sendiri.

**Fungsi Utama**
- Indikator status node & enkripsi (TLS 1.3) sebagai sinyal kepercayaan sebelum pengguna memasukkan kredensial
- Field User ID dengan contoh format inline (`TKN-8821` atau `SPV-104`) — langsung mengajarkan dua skema ID berbeda (teknisi vs supervisor) tanpa perlu halaman bantuan terpisah
- Toggle *show/hide* password — penting karena pengguna sering mengetik di layar tablet dengan sarung tangan atau sambil berjalan, salah ketik lebih mungkin terjadi
- Opsi "Ingat Saya" untuk perangkat tablet bersama yang dipakai bergantian per shift
- Footer teknis: ID stasiun perangkat dan latensi jaringan (ms) — informasi yang biasanya disembunyikan di aplikasi konsumer, tapi di sini dianggap relevan karena pengguna adalah staf teknis yang terbiasa membaca metrik koneksi

**Alasan Desain**
Menampilkan info teknis (node, TLS, latency, station ID) secara terbuka bukan kebetulan — ini membangun kepercayaan ke sistem monitoring yang akan dipakai mengambil keputusan tentang mesin fisik. Kalau koneksi lambat atau node tidak sinkron, pengguna harus tahu *sebelum* login, bukan sesudah salah membaca data karena delay.

---

## 2. `S-02 Dashboard — Monitoring Operasional.png`

**Ide & Latar Belakang**
Ini adalah *control room* digital. Fungsinya menjawab satu pertanyaan dalam hitungan detik begitu dibuka: "Mesin mana yang bermasalah SEKARANG?" Semua elemen di layar ini disusun untuk mendukung jawaban itu lebih dulu, baru detail setelahnya.

**Konsep Visual & Interaksi**
Hirarki baca mengikuti pola Z — dari ringkasan angka (KPI bar: Total Mesin, Beroperasi Normal, Perlu Perhatian, Gangguan Kritis), turun ke grid kartu mesin 2×3, lalu ke tabel alarm aktif di paling bawah. Kartu mesin yang bermasalah (P-101 dengan status *Gangguan*, border merah di sisi kiri) ditempatkan di posisi kiri-atas grid — posisi yang secara alami pertama dibaca mata dalam budaya baca kiri-ke-kanan. Setiap kartu punya *left border accent* berwarna status (merah/kuning/hijau) selain badge teks — pengulangan sinyal warna ini penting supaya status tetap terbaca sekilas dari jarak atau sudut pandang miring, situasi umum saat tablet dipegang sambil berjalan.

**Fungsi Utama**
- KPI bar 4-kolom sebagai ringkasan tertinggi (Total / Normal / Perlu Perhatian / Gangguan Kritis)
- Grid 6 kartu mesin, masing-masing menampilkan 3 parameter kunci + mini-sparkline tren 30 menit terakhir, supaya tren naik/turun terlihat tanpa harus membuka detail
- Tombol aksi kontekstual berbeda per kartu (`Investigasi Unit` + `Buat Laporan` untuk mesin bermasalah; `Inspeksi`, `Atur Kapasitas Beban`, `Detail Siklus`, `Log Generator`, `Kalibrasi Kecepatan` untuk mesin normal) — tombol disesuaikan dengan apa yang relevan dilakukan terhadap status mesin itu, bukan tombol generik yang sama di semua kartu
- Panel "Alarm Aktif Membutuhkan Penanganan Segera" di bawah grid sebagai lapisan kedua setelah ringkasan visual kartu, berisi daftar insiden yang belum ditangani lengkap dengan tombol aksi cepat
- Sidebar kiri menampung identitas supervisor yang bertugas, status koneksi, dan info shift — konteks yang tetap terlihat di semua halaman tanpa perlu dicari

**Alasan Desain**
Keputusan paling penting di layar ini adalah mendahulukan *status* di atas *detail*. Supervisor tidak perlu membaca satu per satu angka suhu/tekanan untuk tahu ada masalah — warna dan posisi kartu sudah menyampaikan itu dalam waktu kurang dari tiga detik. Detail numerik baru dibutuhkan setelah mereka memutuskan mesin mana yang perlu diperiksa — dan itu sudah difasilitasi lewat tombol `Investigasi Unit` yang membawa ke S-03.

---

## 3. `S-03 Detail Mesin P-101 (Pompa Utama).png`

**Ide & Latar Belakang**
Begitu supervisor memutuskan untuk menyelidiki satu mesin, kebutuhannya berubah dari "ringkasan cepat" ke "bukti yang cukup untuk mengambil keputusan teknis." Halaman ini adalah tempat keputusan "apakah mesin ini perlu dihentikan sekarang" benar-benar dibuat.

**Konsep Visual & Interaksi**
Tiga parameter kritis (Suhu Bearing, Tekanan Discharge, Getaran Sumbu) ditampilkan sebagai *radial gauge* — bentuk melingkar yang secara visual langsung menunjukkan seberapa dekat nilai aktual terhadap batas maksimal, tanpa pengguna harus menghitung sendiri selisihnya. Di bawah tiga gauge itu, grafik tren multivariat menumpuk dua parameter (suhu dan getaran) dalam satu chart dengan garis ambang batas kritis sebagai referensi putus-putus — pendekatan ini sengaja dipilih supaya korelasi antara dua parameter (misalnya suhu naik bersamaan dengan getaran) langsung terlihat sebagai pola, bukan harus dibandingkan dari dua chart terpisah. Anotasi "08:30 Spike Mulai" ditempel langsung di titik grafik tempat anomali dimulai — ini mengarahkan mata langsung ke momen yang relevan tanpa pengguna harus menyisir seluruh garis waktu.

**Fungsi Utama**
- Header status besar dengan tag kontekstual (`Multi-Stage Centrifugal`, lokasi fisik `Area Water Intake Bay B`, level urgensi `Trip Imminent — Evaluasi Segera`)
- Tiga radial gauge dengan keterangan ambang batas eksplisit dan deskripsi jenis alarm (misal "Vibrasi Kritis — Bearing cavitation") — bukan cuma angka mentah, tapi juga interpretasi teknis dari angka itu
- Grafik tren dengan pilihan rentang waktu (24 Jam / 1 Minggu / 1 Bulan) dan catatan sumber data (`Modbus RTU/RS-485`, sampling 1 detik) — menjaga kredibilitas data di mata teknisi yang paham spesifikasi sensor
- Panel spesifikasi teknis unit (foto fisik, model, daya motor, tanggal servis terakhir) sebagai konteks aset, bukan hanya data real-time
- Tabel riwayat alarm & peristiwa kritis sebagai jejak historis mesin ini secara spesifik
- Tombol `Buat Laporan` di header — akses langsung ke S-05 begitu keputusan "ini perlu ditindaklanjuti" sudah diambil

**Alasan Desain**
Radial gauge dipilih di atas angka polos karena kebutuhan di sini bukan presisi desimal, tapi *rasa jarak terhadap bahaya* — seberapa dekat suatu parameter ke titik kritis. Format melingkar secara psikologis lebih cepat dibaca sebagai "penuh/hampir penuh" dibanding angka yang perlu dihitung manual terhadap ambang batas. Tiga warna status (hijau/kuning/merah) tetap konsisten dipakai di sini, menjaga bahasa visual yang sama dengan dashboard.

---

## 4. `S-04 Daftar Alarm Global.png`

**Ide & Latar Belakang**
Dashboard (S-02) menunjukkan status *saat ini* per mesin. Layar ini menjawab pertanyaan berbeda: "Apa saja yang sedang terjadi di seluruh pabrik, dan mana yang paling butuh perhatian saya duluan?" — ini adalah lapisan supervisi lintas-mesin, bukan per-unit.

**Konsep Visual & Interaksi**
Pola *progressive disclosure* diterapkan secara eksplisit: metrik ringkasan (Total Alarm Aktif, Gangguan Kritis, Peringatan, Mean Time to Acknowledge) ditaruh di baris atas sebagai gambaran besar sebelum pengguna menyelam ke tabel detail. Filter (Semua/Kritis/Peringatan) ditampilkan sebagai tab berjumlah — bukan dropdown tersembunyi — supaya jumlah masing-masing kategori langsung terlihat tanpa harus mengklik apa pun dulu. Checkbox di setiap baris tabel memungkinkan seleksi multi-item, dengan *floating action bar* yang muncul di bagian bawah saat ada item terpilih — pola ini menghindari supervisor harus membuka dan menutup satu per satu alarm yang sejenis.

**Fungsi Utama**
- KPI bar dengan metrik MTTA (Mean Time to Acknowledge) terhadap target waktu respons — ukuran performa tim, bukan cuma status mesin
- Filter tab berjumlah + dropdown mesin + dropdown rentang waktu + kolom pencarian bebas (ID mesin, parameter, atau kode alarm)
- Tabel dengan kolom yang menjawab lima pertanyaan sekaligus per baris: kapan, mesin apa, parameter apa, seberapa jauh dari ambang batas, dan seberapa parah
- Catatan integritas data di footer tabel ("Buffer log telemetry terenkripsi SHA-256") — detail kecil yang menegaskan bahwa data alarm ini bisa dipertanggungjawabkan secara audit
- Floating batch action bar untuk menandai beberapa alarm selesai sekaligus
- Tombol `Export PDF (SPV)` — hanya relevan untuk peran supervisor yang butuh dokumentasi harian/mingguan

**Alasan Desain**
Perbedaan paling penting dari dashboard adalah: di sini unit analisisnya adalah *insiden*, bukan *mesin*. Satu mesin bisa punya beberapa baris alarm historis; tabel ini perlu padat tapi tetap scannable, karena itu kolom dibuat selebar perlu dan filter diletakkan menonjol di atas tabel, bukan disembunyikan di menu.

---

## 5. `S-05 Form Laporan & Work Order.png`

**Ide & Latar Belakang**
Setelah supervisor memutuskan sebuah anomali perlu tindak lanjut formal, dokumentasi itu harus akurat dan bisa dipertanggungjawabkan — karena hasilnya adalah perintah kerja (*work order*) resmi yang akan mengarahkan tim teknisi fisik ke lapangan dan berdampak pada sistem lain (ERP, SCADA).

**Konsep Visual & Interaksi**
Layout dua kolom memisahkan dua jenis informasi secara sengaja: kolom kiri untuk input manual dari pengguna (form keputusan dan deskripsi), kolom kanan untuk bukti objektif (lampiran foto, hasil scan thermal, dan ringkasan output dokumen). Pemisahan ini membuat jelas mana yang merupakan *judgment* manusia dan mana yang merupakan *bukti* — dua hal yang nanti akan sama-sama direview oleh pihak lain di S-06. Header konteks mesin (lokasi, suhu, getaran, waktu pemicu) ditempel di paling atas form dan tidak bisa diedit — menegaskan bahwa laporan ini terikat pada data telemetri aktual, bukan isian bebas.

**Fungsi Utama**
- Header konteks otomatis dari data mesin yang memicu laporan (lokasi, parameter anomali, waktu, pelapor) — mengurangi kemungkinan technician salah mengisi ulang data yang sebenarnya sudah tercatat sistem
- Pemilihan prioritas penanganan sebagai kartu visual (P1 Urgent / P2 Tinggi / P3 Sedang) yang masing-masing langsung menampilkan target SLA — keputusan prioritas dan konsekuensi waktunya terlihat bersamaan, bukan terpisah
- Dropdown jenis kerusakan dan tim penugasan, dengan info ketersediaan tim ditampilkan langsung di bawah pilihan
- Area deskripsi temuan dengan penghitung karakter — menjaga laporan tetap ringkas tapi cukup detail
- Checklist tindakan korektif awal yang sudah dilakukan sebelum laporan diajukan — supaya reviewer tahu apa yang sudah dicoba, bukan hanya apa yang belum
- Zona unggah bukti foto/thermal dengan drag-and-drop, dan ringkasan dampak sistem dari laporan ini (sinkronisasi ERP, notifikasi multi-kanal, kunci status mesin di SCADA)
- Autosave draft dan nomor registrasi dokumen yang sudah terbentuk sejak awal pengisian

**Alasan Desain**
Form ini sengaja tidak terasa seperti "form kosong yang harus diisi dari nol" — sebagian besar konteks sudah terisi otomatis dari insiden yang memicunya. Ini mengurangi beban kognitif teknisi/supervisor di lapangan yang mungkin sedang menangani situasi mendesak, dan mengurangi risiko kesalahan input data teknis yang krusial untuk keputusan selanjutnya.

---

## 6. `S-06 Sub-section: Report Checklist & Approval Modal.png`

**Ide & Latar Belakang**
Laporan yang masuk dari S-05 tidak otomatis menjadi perintah kerja resmi — perlu ada satu titik keputusan yang jelas dan tercatat, di mana seorang supervisor berwenang menyetujui, meminta revisi, atau menolaknya. Modal ini adalah titik itu.

**Konsep Visual & Interaksi**
Dipilih sebagai *modal dialog* dengan latar belakang digelapkan (dimmed backdrop), bukan halaman penuh terpisah — karena tindakan ini biasanya terjadi di tengah alur kerja lain (misalnya supervisor sedang membuka daftar laporan), dan modal menjaga konteks itu tanpa benar-benar meninggalkan halaman sebelumnya. Sama seperti S-05, pola dua-kolom dipakai lagi secara konsisten: kiri untuk bukti (data telemetri + lampiran foto, termasuk citra thermal dengan overlay titik panas), kanan untuk keputusan (radio button pilihan tindakan + field pendukung). Opsi "Setujui & Terbitkan SPK Penuh" ditandai dengan warna hijau terang saat terpilih — kontras visual yang jelas dari dua opsi lain (revisi/tolak) yang netral.

**Fungsi Utama**
- Ringkasan parameter anomali yang disandingkan langsung dengan ambang batasnya (misal "94.2°C" vs "ambang 80.0°C") — supervisor tidak perlu membuka halaman lain untuk validasi ulang
- Lampiran bukti visual (foto fisik + thermal scan dengan anotasi titik panas) ditampilkan inline, bukan sebagai tautan unduhan — mempercepat verifikasi visual
- Tiga opsi keputusan yang saling eksklusif dan masing-masing punya deskripsi konsekuensi (otorisasi pembongkaran darurat, instruksi inspeksi ulang, atau penolakan dengan pemantauan berkala)
- Field alokasi estimasi downtime yang diizinkan — keputusan teknis tambahan yang menyertai persetujuan, bukan sekadar ya/tidak
- Catatan otorisasi opsional untuk arahan khusus ke tim lapangan
- Checkbox sinkronisasi ke sistem ERP dan notifikasi broadcast — supervisor memutuskan sejauh mana keputusan ini perlu disebar ke sistem lain
- Jejak audit yang tampak jelas: nama otorisator dan alamat IP tercatat di bagian bawah panel keputusan

**Alasan Desain**
Menyandingkan bukti dan kontrol keputusan secara *side-by-side* (bukan bukti di atas, keputusan di bawah dengan scroll) adalah keputusan sadar untuk mempercepat verifikasi — supervisor tidak perlu mengingat angka yang baru dibaca saat berpindah ke bagian keputusan, karena keduanya ada dalam satu bidang pandang. Jejak audit (nama + IP) ditampilkan terbuka, bukan disembunyikan di log terpisah, karena keputusan di modal ini punya konsekuensi fisik dan finansial — transparansi akuntabilitas perlu terasa di titik keputusan itu sendiri, bukan hanya tercatat diam-diam di backend.

---

## Prinsip Desain yang Konsisten di Seluruh Layar

Beberapa keputusan desain sengaja diulang di semua enam layar, karena konsistensi lintas-halaman adalah yang membuat sistem terasa dapat dipercaya dan cepat dipelajari:

- **Bahasa warna status yang sama di semua tempat** — hijau (normal), kuning (peringatan), merah (gangguan/kritis) dipakai konsisten baik di badge, border kartu, maupun gauge, tanpa makna warna yang bergeser antar halaman.
- **Progressive disclosure sebagai pola berulang** — ringkasan tinggi dulu (angka besar/KPI), baru detail (tabel/grafik) di bawahnya. Pola ini muncul di S-02 maupun S-04, membuat pengguna tidak perlu belajar ulang cara "membaca" halaman baru.
- **Konteks yang menempel pada data, bukan terpisah** — di S-03, S-05, dan S-06, data telemetri yang relevan selalu ditempel langsung di header atau di samping form/keputusan, bukan harus dicari di halaman lain.
- **Breadcrumb dan identitas shift yang selalu terlihat** — sidebar dan breadcrumb konsisten menunjukkan "siapa yang login, di plant/line mana, dan sedang di langkah apa", penting untuk sistem yang dipakai bergilir antar shift.
- **Transparansi akuntabilitas di titik keputusan** — baik di S-05 (nomor WO, siapa pelapor) maupun S-06 (otorisator + IP), jejak "siapa melakukan apa" selalu melekat pada aksi itu sendiri, bukan dipisah ke log administratif yang terpisah.

Enam prinsip di atas yang sebaiknya tetap dijaga saat proses desain berpindah dari mockup ini ke Figma — bukan sekadar meniru tampilan, tapi menjaga alasan di baliknya.
