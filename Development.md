# Development — Application Monitoring Peralatan Industri

Dokumen ini ditujukan untuk **Developer**. Berisi spesifikasi teknis yang mencerminkan struktur layar dari UI PRD dan kebutuhan fungsional dari User Requirements.

---

## 1. Tech Stack

| Layer | Pilihan | Penjelasan Singkat |
|---|---|---|
| Frontend | **React JS** | Library UI berbasis komponen, cocok untuk SPA |
| Styling | **Tailwind CSS** | Utility-first CSS, tulis class langsung di JSX, cepat untuk prototype |
| State Management | **Zustand** | "Kotak penyimpanan global" untuk React — simpan data mesin, alarm, user di satu tempat dan bisa diakses dari halaman manapun. Lebih simple dari Redux, API minimal |
| Charting | **Recharts** | Library chart dibangun khusus untuk React. Lebih idiomatis dari Chart.js (yang dibangun untuk vanilla JS) |
| Backend | **Express.js** | Node.js server minimalis. Cukup beberapa endpoint REST API untuk prototype |
| Database | **SQLite** (via `better-sqlite3`) | File database lokal, zero setup, tidak perlu install server database |
| Auth | **JWT** (JSON Web Token) | Token autentikasi stateless — server tidak perlu ingat siapa yang login. Token disimpan di browser, cocok untuk React SPA |

### Catatan Auth: JWT vs Session-based
- **JWT (dipilih):** Token digenerate server saat login, dikirim ke browser, disimpan di `localStorage` atau `httpOnly cookie`. Server tidak menyimpan state session. Lebih simple untuk prototype.
- **Session-based:** Server menyimpan session di memori/Redis, lebih secure untuk production karena token bisa di-invalidate kapan saja. Pertimbangkan upgrade ke ini saat production.

### Catatan Real-time: Polling vs SSE vs WebSocket
- **Polling 10 detik (dipilih untuk prototype):** Frontend fetch data setiap 10 detik. Paling simple, tidak butuh setup khusus, tidak ada persistent connection.
- **SSE (Server-Sent Events):** Server push data satu arah ke browser secara real-time. Lebih efisien dari polling, cocok untuk monitoring (data mengalir dari server ke client). Auto-reconnect built-in. Upgrade ke ini setelah prototype stabil.
- **WebSocket:** Koneksi dua arah (browser ↔ server). Cocok untuk aplikasi kolaboratif / chat. Overkill untuk monitoring yang mayoritas server → client.

---

## 2. Struktur Halaman / Routes

Setiap route mencerminkan layar di [UI_PRD.md](./UI_PRD.md).

| Route | Layar | Komponen Utama | Guard |
|---|---|---|---|
| `/login` | S-01 Login | `LoginForm`, `BrandingHeader` | Public |
| `/dashboard` | S-02 Dashboard | `KPISummaryBar`, `EquipmentGrid`, `AlarmPanel`, `NavBar` | Auth |
| `/equipment/:id` | S-03 Detail Peralatan | `EquipmentHeader`, `ParameterWidgets`, `TrendChart`, `AlarmTable` | Auth |
| `/alarms` | S-04 Daftar Alarm | `AlarmFilterBar`, `AlarmTable` | Auth |
| `/report/new` | S-05 Form Laporan | `ReportForm` | Supervisor only |
| `/admin` | S-06 User Management | `UserTable`, `MachineTable`, `ReportChecklist`, `ExportPanel` | Supervisor only |

**Auth Guard:** Semua route kecuali `/login` perlu token JWT valid. Jika tidak ada, redirect ke `/login`.
**Supervisor Guard:** `/report/new` dan `/admin` hanya bisa diakses jika `role === "supervisor"`.

---

## 3. Data Model

### 3.1 Equipment (Peralatan)

```
Equipment {
  id: string           // "P-101"
  name: string         // "Pompa Utama"
  type: string         // "Pompa" | "Kompresor" | "Motor" | "Chiller" | "Generator" | "Conveyor"
  status: "normal" | "warning" | "fault"
  parameters: Parameter[]
  lastUpdated: datetime
}
```

### 3.2 Parameter (Nilai Sensor)

```
Parameter {
  key: string               // "temperature"
  label: string             // "Suhu"
  value: number
  unit: string              // "°C" | "bar" | "mm/s" | "%" | "V" | "m/s"
  thresholdWarning: number | null   // nullable — sensor belum ditest
  thresholdFault: number | null     // nullable — sensor belum ditest
}
```

Threshold bersifat **nullable** karena nilai batas aman per sensor belum ditentukan (sensor belum ditest). Setelah ada data real, field ini diisi dan menjadi garis referensi di grafik tren.

### 3.3 Alarm

```
Alarm {
  id: string
  equipmentId: string
  equipmentName: string
  parameter: string
  value: number
  severity: "warning" | "fault"
  timestamp: datetime
  resolved: boolean
  resolvedAt: datetime | null
}
```

Alarm dengan `resolved: true` tidak ditampilkan di S-04 Daftar Alarm Global — hanya muncul di riwayat per mesin (S-03).

### 3.4 Technician (User)

```
Technician {
  id: string
  name: string
  role: "technician" | "supervisor"
  passwordHash: string     // bcrypt hash, JANGAN simpan plain text
  isActive: boolean
  lastLogin: datetime | null
}
```

### 3.5 Report (Laporan)

```
Report {
  id: string
  equipmentId: string
  equipmentName: string
  createdBy: string        // technician/supervisor ID
  createdAt: datetime
  faultType: string
  description: string
  photoPath: string | null  // path file di local storage
  status: "pending" | "approved" | "rejected"
  reviewedBy: string | null
  reviewedAt: datetime | null
  reviewNote: string | null
}
```

---

## 4. Komponen yang Perlu Dibangun

| Komponen | Halaman | Deskripsi |
|---|---|---|
| `StatusBadge` | S-02, S-03 | Badge warna sesuai status — Normal/Warning/Fault |
| `EquipmentCard` | S-02 | Kartu mesin: badge, parameter, sparkline. Mendukung auto-sort by status |
| `KPISummaryBar` | S-02 | 4 angka: total, normal, warning, fault |
| `Sparkline` | S-02 | Grafik garis mini (last N data points) per kartu |
| `ParameterWidget` | S-03 | Card/gauge untuk satu parameter (suhu, tekanan, dll) |
| `TrendChart` | S-03 | Grafik garis interaktif dengan threshold line (nullable). Switch 24h/1w/1m |
| `AlarmTable` | S-03, S-04 | Tabel alarm — reusable di detail per mesin dan list global |
| `AlarmFilterBar` | S-04 | Filter keparahan + rentang waktu |
| `NavBar` | Semua (kecuali S-01) | Side nav desktop/tablet, hamburger mobile. Tampilkan User Management hanya untuk supervisor |
| `LoginForm` | S-01 | Form ID + password + Remember Me |
| `ReportForm` | S-05 | Form laporan + upload foto |
| `UserTable` | S-06 | Tabel manajemen teknisi |
| `MachineTable` | S-06 | Tabel manajemen mesin |
| `ReportChecklist` | S-06 | Daftar laporan pending + approve/reject |
| `ExportPanel` | S-06 | Tombol export PDF alarm dan laporan |
| `AuthGuard` | Routing | HOC/wrapper yang redirect ke login jika tidak autentikasi |
| `SupervisorGuard` | Routing | HOC/wrapper yang blokir akses jika bukan supervisor |

---

## 5. State Management (Zustand)

### State Global

| Store | State | Tipe | Keterangan |
|---|---|---|---|
| `authStore` | `currentUser` | `Technician \| null` | User yang sedang login |
| `authStore` | `token` | `string \| null` | JWT token aktif |
| `equipmentStore` | `equipments` | `Equipment[]` | Data semua mesin (di-refresh tiap 10 detik) |
| `alarmStore` | `activeAlarms` | `Alarm[]` | Alarm yang belum resolved |
| `uiStore` | `connectionStatus` | `"online" \| "offline"` | Status koneksi ke backend |
| `uiStore` | `theme` | `"light" \| "dark"` | Tema aktif |

### State Lokal (Per Halaman)

- **S-03 Detail:** `selectedEquipmentId`, `trendRange` ("24h" | "1w" | "1m")
- **S-04 Alarm List:** `filterSeverity`, `filterTimeRange`
- **S-06 User Management:** `activeTab` ("users" | "machines" | "reports" | "export")

---

## 6. Real-Time Data

**Mekanisme:** Polling tiap **10 detik** (untuk prototype).

```
useEffect(() => {
  const interval = setInterval(() => {
    fetchEquipments()  // update equipmentStore
    fetchActiveAlarms() // update alarmStore
  }, 10000)
  return () => clearInterval(interval)
}, [])
```

Requirement dari UI: status seluruh mesin harus tampil dalam < 3 detik setelah halaman dibuka. Polling 10 detik memenuhi ini karena initial load langsung fetch tanpa tunggu interval.

**Upgrade path:** Setelah prototype stabil, pertimbangkan migrasi ke SSE untuk real-time push yang lebih efisien.

---

## 7. Autentikasi (JWT)

- `/login` → public, tidak butuh token
- Semua route lain → `AuthGuard` cek JWT di `localStorage` atau `httpOnly cookie`
- "Ingat Saya" ON → token expire 30 hari
- "Ingat Saya" OFF → token expire saat browser ditutup (session)
- Role check untuk supervisor routes → cek `currentUser.role === "supervisor"`

---

## 8. Security Notices

Bagian ini mencatat semua titik yang perlu diperhatikan dari sisi keamanan.

| Item | Risiko | Mitigasi |
|---|---|---|
| **JWT Secret** | Jika secret bocor, semua token bisa dipalsukan | Simpan di `.env` (`JWT_SECRET=...`), JANGAN hardcode di source code. Tambahkan `.env` ke `.gitignore` |
| **JWT di localStorage** | Rentan XSS — script jahat bisa baca token | Untuk prototype OK. Untuk production: pindah ke `httpOnly cookie` |
| **Password** | Plain text password bocor jika DB diakses | SELALU hash dengan `bcrypt` sebelum simpan. JANGAN pernah simpan password plain text |
| **SQLite file path** | File DB bisa diakses jika path terbuka | Simpan di luar folder `public/` atau folder yang di-serve static. Contoh: `./data/app.db` |
| **File upload (foto laporan)** | Upload file arbitrary bisa jadi attack vector | Validasi MIME type + extension. Batasi ukuran file. Simpan di folder yang tidak di-serve langsung |
| **CORS** | Request dari domain lain ke API | Set CORS hanya ke `localhost` selama development. Jangan gunakan `*` |
| **`.env` file** | Berisi secret, jangan pernah di-commit ke git | Tambahkan `.env` ke `.gitignore` sebelum push pertama kali |

---

## 9. Referensi ke UI

Semua keputusan visual (warna, ukuran, spacing, komponen) ada di [UI_PRD.md](./UI_PRD.md). Developer mengikuti design tokens di Section 1 UI_PRD untuk implementasi Tailwind CSS (custom theme di `tailwind.config.js`).
