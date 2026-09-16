# Development — Application Monitoring Peralatan Industri

Dokumen ini ditujukan untuk **Developer**. Berisi spesifikasi teknis yang mencerminkan struktur layar dan kebutuhan fungsional dari UI PRD.

---

## 1. Tech Stack

> **Perlu Diisi:** Tentukan pilihan tech stack sebelum development dimulai. Semua section di bawah mengasumsikan web-based, sesuaikan jika berbeda.

| Layer | Pilihan (Contoh) | Keterangan |
|---|---|---|
| Frontend | — | Misalnya: React, Vue, Angular, atau native Android/iOS |
| State Management | — | Misalnya: Redux, Zustand, Context API |
| Charting | — | Untuk grafik tren dan sparkline (contoh: Recharts, Chart.js, D3) |
| Styling | — | Misalnya: Tailwind CSS, styled-components, MUI |
| Backend / API | — | REST API atau WebSocket untuk real-time data |
| Database | — | Misalnya: PostgreSQL, InfluxDB (untuk time-series), atau SCADA bridge |
| Auth | — | Session-based atau JWT |

---

## 2. Struktur Halaman / Routes

Setiap route mencerminkan layar di [UI_PRD.md](./UI_PRD.md).

| Route | Layar | Komponen Utama |
|---|---|---|
| `/login` | S-01 Login | `LoginForm`, `BrandingHeader` |
| `/dashboard` | S-02 Dashboard | `KPISummaryBar`, `EquipmentGrid`, `AlarmPanel`, `NavBar` |
| `/equipment/:id` | S-03 Detail Peralatan | `EquipmentHeader`, `ParameterWidgets`, `TrendChart`, `AlarmTable` |
| `/alarms` | S-04 Daftar Alarm | `AlarmFilterBar`, `AlarmTable` |
| `/report/new` | S-05 Form Laporan | `ReportForm` |

> **Perlu Diisi:** Apakah ada route lain yang dibutuhkan? (Pengaturan profil, manajemen user, notifikasi, dll)

---

## 3. Data Model

### 3.1 Equipment (Peralatan)

```
Equipment {
  id: string           // contoh: "P-101"
  name: string         // contoh: "Pompa Utama"
  type: string         // Pompa | Kompresor | Motor | Chiller | Generator | Conveyor
  status: "normal" | "warning" | "fault"
  parameters: Parameter[]
  lastUpdated: datetime
}
```

### 3.2 Parameter (Nilai Sensor)

```
Parameter {
  key: string          // contoh: "temperature"
  label: string        // contoh: "Suhu"
  value: number
  unit: string         // contoh: "°C", "bar", "mm/s", "%"
  thresholdWarning: number
  thresholdFault: number
}
```

> **Perlu Diisi:** Nilai threshold (batas aman) per parameter per mesin. Ini yang akan dirender sebagai garis di grafik tren.

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
  resolvedAt?: datetime
}
```

### 3.4 Technician (User)

```
Technician {
  id: string
  name: string
  role: "technician" | "supervisor"
  passwordHash: string
}
```

> **Perlu Diisi:** Field tambahan jika ada (shift, area tanggung jawab, nomor HP untuk notifikasi, dll).

---

## 4. Komponen yang Perlu Dibangun

| Komponen | Halaman | Deskripsi |
|---|---|---|
| `StatusBadge` | Dashboard, Detail | Badge warna sesuai status (normal/warning/fault) |
| `EquipmentCard` | Dashboard | Kartu mesin dengan badge, parameter, sparkline |
| `KPISummaryBar` | Dashboard | 4 angka: total, normal, warning, fault |
| `Sparkline` | Dashboard | Grafik garis mini per kartu |
| `ParameterWidget` | Detail | Card/gauge untuk satu parameter (suhu, tekanan, dll) |
| `TrendChart` | Detail | Grafik garis interaktif dengan threshold line |
| `AlarmTable` | Detail, Alarm List | Tabel riwayat alarm |
| `AlarmFilterBar` | Alarm List | Filter keparahan + rentang waktu |
| `NavBar` | Semua (kecuali Login) | Navigasi utama (bottom/side) |
| `LoginForm` | Login | Form ID + password + tombol masuk |
| `ReportForm` | Form Laporan | Form laporan + upload foto |

---

## 5. State Management

### State Global yang Dibutuhkan

| State | Tipe | Keterangan |
|---|---|---|
| `currentUser` | `Technician \| null` | User yang sedang login |
| `equipments` | `Equipment[]` | Data semua mesin (di-poll / real-time) |
| `activeAlarms` | `Alarm[]` | Alarm yang belum resolved |
| `connectionStatus` | `"online" \| "offline"` | Status koneksi ke backend |

### State Lokal (Per Halaman)

- **Detail:** `selectedEquipmentId`, `trendRange` (24h / 1w)
- **Alarm List:** `filterSeverity`, `filterTimeRange`

---

## 6. Real-Time Data

> **Perlu Diisi:** Mekanisme update data real-time — pilih salah satu dan konfigurasikan:
> - **Polling** — frontend request ke API setiap X detik (contoh: setiap 5 detik)
> - **WebSocket** — koneksi persistent, backend push data saat ada perubahan
> - **Server-Sent Events (SSE)** — alternatif WebSocket untuk satu arah

Requirement dari UI: status seluruh mesin harus tampil dalam < 3 detik setelah halaman dibuka.

---

## 7. Autentikasi

- Halaman `/login` tidak memerlukan auth
- Semua halaman lain perlu guard: redirect ke `/login` jika belum autentikasi
- "Ingat Saya" → simpan token/session lebih lama (sesuaikan durasi)

> **Perlu Diisi:** Durasi session normal vs. "Ingat Saya". Apakah ada role-based access (teknisi vs. supervisor melihat hal berbeda)?

---

## 8. Referensi ke UI

Semua keputusan desain visual (warna, ukuran, spacing) ada di [UI_PRD.md](./UI_PRD.md). Developer cukup mengikuti design tokens di Section 1 UI_PRD untuk implementasi CSS/styling.
