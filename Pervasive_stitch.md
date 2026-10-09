# Pervasive — Industrial Equipment Monitoring App
### UI Design Brief for Google Stitch → Figma Handoff

---

## 0. How to Use This Document

This brief is written to be dropped directly into Google Stitch as a design prompt. It contains everything needed to generate a cohesive, production-grade UI: product context, art direction, design tokens, component specs, and all 6 screens. Nothing in this document references external files — treat it as the single source of truth.

**Client:** PT Maju Teknik Industri
**Platform:** Tablet-first web app, landscape orientation
**Primary frame size:** 1280 × 800 px (also support 1194 × 834 px)

---

## 1. Product Context

Pervasive is a real-time industrial equipment monitoring application used by field technicians and supervisors walking the production floor. The core problem: a technician needs to glance at a tablet while walking — possibly in harsh factory lighting, possibly holding the device with one hand — and know within **3 seconds** whether all equipment is operating normally, or whether something needs attention.

This is not an office SaaS dashboard. It is a **field instrument**. Every design decision should be filtered through: *"Can a technician read this at a glance, under bad lighting, while moving?"*

**Primary users:**
- **Technicians** — monitor equipment, view alarms, file incident reports.
- **Supervisors** — everything technicians can do, plus user management, machine configuration, report approval, and data export.

**The 6 monitored machines:**

| ID | Name | Monitored Parameters |
|---|---|---|
| P-101 | Pompa (Pump) | Temperature (°C), Pressure (bar), Vibration (mm/s) |
| C-201 | Kompresor (Compressor) | Temperature (°C), Pressure (bar), Vibration (mm/s) |
| M-301 | Motor | Temperature (°C), Load (%), Vibration (mm/s) |
| CH-01 | Chiller | Temperature (°C), Pressure (bar), Load (%) |
| G-01 | Genset (Generator) | Temperature (°C), Load (%), Voltage (V) |
| CV-02 | Conveyor | Speed (m/s), Load (%), Vibration (mm/s) |

---

## 2. Design Direction — The Taste

Think **industrial command center**, not startup dashboard. The reference feeling is a modern SCADA/control-room interface crossed with the polish of a premium consumer product — calm when everything is fine, impossible to ignore when it isn't.

**Three design principles to hold onto for every screen:**

1. **Status color is the hero, not decoration.** Green/amber/red isn't a badge tucked in a corner — it drives border glow, card elevation, and sort order. A faulted machine should pull the eye before the user even reads text. Resting state (all-green) should feel quiet and confident — plenty of soft blue-gray negative space, no visual noise. The moment something goes wrong, the UI should visibly "wake up" around that element.

2. **Precision over decoration.** This is instrumentation, not marketing. Avoid illustrations, gradients-for-the-sake-of-gradients, playful mascots, or rounded blob shapes. Favor crisp data typography, tabular alignment for numbers, thin dividing lines, and generous but disciplined whitespace. Numbers (temperature, pressure, voltage) should always sit in a monospaced or tabular-figure treatment so values are scannable in a column.

3. **One accent color, used with intent.** Indigo (`#4318FF`) is the single brand accent — used for primary actions, active nav state, and focus states only. It should never compete with the semantic status colors. If a screen has indigo AND a red fault badge, the red must win the eye.

**Avoid at all costs (anti-AI-slop checklist):**
- Generic rounded-everything "friendly SaaS" look with pastel blobs and emoji-style icons.
- Centered hero sections, marketing-style empty states with big illustrations.
- Overly decorative gradients on cards or buttons.
- Inconsistent corner radii / shadow depths between components.
- Low-contrast gray-on-gray text that fails a glance-test under bright light.
- Icon-only buttons without labels on primary actions (field users need certainty, not guessing).

**Mood references to channel:** aviation cockpit MFDs, modern SCADA/HMI software (Siemens WinCC, Ignition), premium fitness/health dashboards (Oura, Whoop) for the calm-data-density feel, Linear/Vercel for typographic discipline — but warmer and more legible, since this isn't a developer tool.

---

## 3. Design Tokens

### 3.1 Color — Light Theme (default)

| Token | Hex | Usage |
|---|---|---|
| `color-background` | `#F4F7FE` | Page background |
| `color-surface` | `#FFFFFF` | Card / panel background |
| `color-surface-raised` | `#FFFFFF` with soft shadow | Modals, dropdowns, popovers |
| `color-primary` | `#4318FF` | Primary buttons, active nav, links, focus rings |
| `color-primary-hover` | `#3311CC` | Primary hover/pressed state |
| `color-text-heading` | `#2B3674` | Titles, machine names, headings |
| `color-text-body` | `#A3AED0` | Secondary text, labels, captions, placeholder text |
| `color-border` | `#E9EDF7` | Card borders, dividers, table row separators |

### 3.2 Color — Dark Theme (required, full parity with light)

| Token | Hex | Usage |
|---|---|---|
| `color-background-dark` | `#0F172A` | Page background |
| `color-surface-dark` | `#1E293B` | Card / panel background |
| `color-surface-raised-dark` | `#273349` | Modals, dropdowns, popovers |
| `color-primary-dark` | `#818CF8` | Primary buttons, active nav, links (lightened indigo for dark contrast) |
| `color-primary-hover-dark` | `#9FA8FA` | Primary hover/pressed state |
| `color-text-heading-dark` | `#E2E8F0` | Titles, machine names, headings |
| `color-text-body-dark` | `#94A3B8` | Secondary text, labels, captions |
| `color-border-dark` | `#334155` | Card borders, dividers |

Dark theme is a **first-class deliverable** — design every screen in both themes, not light-only with a dark palette swap as afterthought. Factory floors often have poor overhead lighting where dark mode is the more practical default; assume technicians may toggle between themes depending on shift and ambient light.

### 3.3 Status / Alarm Colors (identical across both themes — never swap these)

| Token | Hex | Meaning | Label (Indonesian, keep as-is in UI) |
|---|---|---|---|
| `color-status-normal` | `#22C55E` | Operating normally | "Beroperasi" |
| `color-status-warning` | `#F59E0B` | Warning / needs attention | "Peringatan" |
| `color-status-fault` | `#EF4444` | Fault / critical | "Gangguan" |

Text on top of any status badge is always white `#FFFFFF`, bold weight, for guaranteed WCAG AA contrast.

### 3.4 Typography

**Font family:** Plus Jakarta Sans (primary). Fallback stack: Inter, Roboto, system-ui, sans-serif.
**Numeric data (temperatures, pressures, voltages, IDs):** use tabular/monospaced figure variant where available, so columns of numbers align visually.

| Token | Size | Weight | Usage |
|---|---|---|---|
| `text-display` | 32px | Bold (700) | Page-level titles (e.g. "Dashboard") |
| `text-title` | 24px | Bold (700) | Card titles, machine names, section headers |
| `text-subtitle` | 18px | Semibold (600) | Sub-section headers, modal titles |
| `text-body` | 16px | Regular (400) | Main content, descriptions, table cells |
| `text-body-strong` | 16px | Semibold (600) | Emphasized body text, key values |
| `text-caption` | 13px | Medium (500) | Labels, timestamps, units, table headers |

### 3.5 Spacing (8-point grid)

| Token | Value | Usage |
|---|---|---|
| `space-xs` | 8px | Gap between tightly related elements inside a component |
| `space-sm` | 16px | Internal card padding, grid margins |
| `space-md` | 24px | Gap between sections |
| `space-lg` | 32px | Gap between major blocks / card groups |
| `space-xl` | 48px | Page-level top/bottom breathing room |

### 3.6 Grid & Layout

- **Grid system:** 12 columns, 16px margin, 16px gutter.
- **Primary target:** Tablet landscape, 1280×800px. Side navigation stays persistently open — never collapses on this breakpoint.
- **Secondary breakpoints (support but tablet landscape is primary):**
  - Desktop ≥1280px: same layout as tablet, side nav open, content area simply gets more breathing room.
  - Mobile <768px: side navigation collapses into a bottom navigation bar (not hamburger — field users need one-tap access to the 4 main sections at all times).
- **Touch target minimum:** 48×48px for every interactive element, no exceptions. This is a glove-friendly, walking-while-tapping interface.
- **Corner radius system:** `radius-sm` 8px (buttons, inputs, badges), `radius-md` 16px (cards), `radius-lg` 24px (modals). Keep this consistent everywhere — radius inconsistency is one of the fastest ways an interface reads as unpolished.
- **Elevation:** Use soft, low-opacity shadows (not hard drop shadows) for card elevation in light theme. In dark theme, prefer a subtle lighter-border + minimal shadow instead of shadow alone (shadows barely read on dark backgrounds).

---

## 4. Core Components

### 4.1 Status Badge

A pill-shaped label showing machine or alarm state at a glance.

- Background: the status color (`#22C55E` / `#F59E0B` / `#EF4444`).
- Text: white, bold, 13–14px, label in Indonesian ("Beroperasi" / "Peringatan" / "Gangguan").
- Height: minimum 32px for inline/table use, 48px for header-level "large" variant on the Equipment Detail screen.
- Horizontal padding: 12–16px.
- No border, no gradient — flat, confident color fill.

### 4.2 Button

| Variant | Background | Text | Border | Usage |
|---|---|---|---|---|
| Primary | `color-primary` | White | None | Main CTA per screen ("Masuk", "Buat Laporan", "Kirim Laporan") |
| Secondary | Transparent | `color-primary` | 1.5px `color-primary` | Secondary actions, cancel-adjacent actions |
| Disabled | `color-text-body` (muted) | White | None | Inactive state, reduced opacity ~50% |

- Height: 48px minimum (56px for the Login screen's primary CTA, to feel substantial on the first impression screen).
- Corner radius: 8px (`radius-sm`).
- Label font: `text-body-strong`, never icon-only for primary actions.

### 4.3 Equipment Card

The atomic unit of the Dashboard. Appears in a **2-column × 3-row grid** (6 cards total — one per machine), designed to flex if machine count grows later.

Contents, top to bottom:
1. **Machine name** (`text-title`) + **Machine ID** (`text-caption`, muted) on the same row, ID right-aligned or directly beneath name.
2. **Status Badge** (top-right corner of the card).
3. **Key parameters** — 2–3 values shown as a compact inline row, e.g. `Suhu: 78°C` · `Tekanan: 2.4 bar`. Use tabular figures so values align across cards.
4. **Sparkline** — a small trendline (last ~24h) of the primary parameter, rendered thin and quiet in resting state, in the accent color when normal.

**Emergency visual hierarchy (critical requirement):** A card in **Fault** state gets a colored left-border or full-border glow in `color-status-fault`, plus a very subtle elevated shadow in that same hue — it should look like it's "lit up." **Warning** state gets the same treatment in amber, slightly less intense. **Normal** state cards stay visually quiet: thin neutral border, standard elevation, no colored glow. This hierarchy is the single most important visual behavior in the entire app — the dashboard's job is to make the eye land on trouble first.

### 4.4 Navigation

- **Tablet/Desktop (≥768px):** Persistent vertical side navigation, left-aligned, always expanded (icon + label, not icon-only) — a field tech should never have to tap to reveal nav.
- **Mobile (<768px):** Bottom navigation bar, 4 icons + labels, 48px+ touch targets.
- **Nav items, in order:**
  1. Dashboard
  2. Alarm List
  3. User Management *(Supervisor role only — hidden entirely for Technicians)*
  4. Settings

### 4.5 Data Table

Used for Alarm List, Alarm History, and the three User Management sub-tables.

- Header row: `text-caption`, uppercase or semibold, muted color, bottom border 1px `color-border`.
- Row height: minimum 56px (comfortable tap target for row actions).
- Zebra striping optional but keep contrast subtle — avoid loud alternating colors.
- Status/severity values in table cells render as the same Status Badge component used elsewhere — never a plain colored text, always the pill.
- Row actions (e.g. "Tandai Selesai", "Edit", "Nonaktifkan") sit right-aligned as a Secondary button or icon+label link.

### 4.6 Gauge / Value Card (Equipment Detail screen)

A per-parameter widget showing current value against safe range.

- Large numeric value (`text-display` or `text-title` scale) with unit as `text-caption` beside it.
- A circular or horizontal gauge arc showing position within min/max safe range, colored by current status (green/amber/red) rather than always the accent color — the gauge itself should reflect health, not just brand.
- Threshold markers visible on the gauge track where applicable.

---

## 5. Screens

### S-01 — Login

**Purpose:** Authenticate before entering the system. First impression of the product — should feel calm, trustworthy, industrial-grade.

**Layout:** Centered card on the `color-background` canvas, generous negative space. No stock-photo backgrounds, no gradients — a clean, confident, almost utilitarian login.

**Elements:**
- Company logo / app branding placeholder for "PT Maju Teknik Industri", top of the card.
- Input field: Technician ID (48px min height).
- Input field: Password (48px min height, show/hide toggle icon).
- Checkbox: "Ingat Saya" (Remember Me).
- Text link: "Lupa Password" (Forgot Password), right-aligned near the password field.
- Primary button: "Masuk" (56px height, full width of the card).

**States to design:**
- Default (empty fields).
- Filled (valid input, button active).
- Error (wrong ID/password) — red inline error message beneath the relevant field, input border turns `color-status-fault`.
- Loading (authenticating) — button shows a spinner and disables, label dims.

---

### S-02 — Dashboard (Main Screen)

**Purpose:** Let the user assess the state of all 6 machines in under 3 seconds. This is the screen the app is built around — give it the most design attention.

**Layout, top to bottom:**
1. **Header bar** — logged-in user's name, "last updated" timestamp (live-updating), connection status indicator (small dot: connected/disconnected).
2. **KPI summary bar** — 4 large stat tiles in a row: Total (6) · Normal (n) · Peringatan (n) · Gangguan (n). Each tile's number should visually borrow its status color (the "Gangguan" tile's number renders in red, etc.) so the summary itself previews the detail below.
3. **Equipment card grid** — 2 columns × 3 rows (see §4.3). **Auto-sort order: Fault cards first, then Warning, then Normal** — the grid re-orders itself live as states change, so the most urgent machines are always top-left, closest to where the eye naturally lands first.
4. **Active alarms panel** — a compact list of the 3–5 most recent unresolved alarms, positioned below or beside the card grid (right rail if space allows on 1280px canvas).
5. **Side navigation** — persistent, per §4.4.

---

### S-03 — Equipment Detail

**Purpose:** Deep-dive analysis of a single machine, reached by tapping its card.

**Elements:**
- **Header:** machine name + ID, large Status Badge (48px variant), positioned prominently at top.
- **Parameter widgets:** one Gauge/Value Card (§4.6) per monitored parameter for that machine (2–3 depending on machine type, see table in §1).
- **Trend chart:** interactive line chart with a time-range switch (24 hours / 1 week / 1 month tabs), showing a visible threshold line for the safe operating boundary. If no threshold is set for a parameter yet, the line is simply omitted (nullable) rather than showing a placeholder.
- **Alarm history table:** columns — Date, Time, Parameter, Value, Status. Uses the Data Table component (§4.5).
- **Primary button:** "Buat Laporan / Work Order" — visible only to Supervisor role, positioned prominently (e.g. top-right of header or sticky at page bottom).

---

### S-04 — Global Alarm List

**Purpose:** Single view of every currently unresolved alarm across all 6 machines.

**Elements:**
- **Filter bar:** severity filter (All / Peringatan / Gangguan) as segmented control or pill tabs, plus a time-range picker.
- **Table:** columns — Timestamp, Machine ID, Machine Name, Parameter, Value, Status. Uses Data Table (§4.5).
- **Row-level quick action:** "Tandai Selesai" (Mark Resolved) button per row.
- **Export button:** "Export PDF" — visible only to Supervisor role, top-right of the screen.

**Note:** Once an alarm is resolved, it disappears from this list (resolved history lives per-machine on S-03's alarm history table instead).

---

### S-05 — Report / Work Order Form

**Purpose:** Supervisor creates a formal incident report / work order, typically launched from S-03.

**Elements:**
- Pre-filled, read-only context: Machine ID + Machine Name (carried over from the detail screen that launched this form).
- Dropdown: "Jenis Kerusakan" (Fault Type).
- Textarea: "Catatan / Deskripsi Temuan" (Notes / Findings).
- File upload: photo/attachment, drag-and-drop or tap-to-browse, with thumbnail preview once uploaded.
- Primary button: "Kirim Laporan" (Submit Report).
- On submit, this generates a PDF report (exact PDF template/layout is a separate design task, not covered here — note it as a future deliverable, don't attempt to design the PDF itself).

---

### S-06 — User Management

**Purpose:** Supervisor-only screen for managing technician accounts, machine configuration, report approvals, and data export. Likely organized as tabs or a sub-navigation within this screen given four distinct sub-sections.

**Sub-section: Manage Technicians**
- Table: ID, Name, Role, Account Status (Active/Inactive), Last Login.
- Button: "Tambah Teknisi" (Add Technician) → opens a form (name, ID, initial password).
- Row actions: Edit · Deactivate.

**Sub-section: Manage Machines**
- Table: ID, Name, Type, Status, Monitored Parameters.
- Button: "Tambah Mesin" (Add Machine) → opens a form (ID, name, type, parameters).

**Sub-section: Report Checklist**
- List of submitted reports (from S-05), each tagged with status: Menunggu (Pending) / Disetujui (Approved) / Ditolak (Rejected) — rendered via the Status Badge pattern, repurposed with these three states.
- Row actions: View Detail · Approve · Reject (with a note field on reject).

**Sub-section: Export Data**
- Export the alarm list (by date range) as PDF.
- Export the report list as PDF.

---

## 6. User Flow

```
[S-01 Login]
     │ (tap "Masuk", success)
     ▼
[S-02 Dashboard] ──(tap equipment card)──► [S-03 Equipment Detail]
     │                                            │
     │ (nav: Alarm List)                          │ (tap "Buat Laporan", Supervisor only)
     ▼                                            ▼
[S-04 Global Alarm List]                   [S-05 Report Form]
     │ (tap a row)
     ▼
[S-03 Equipment Detail]

[Side Nav: User Management, Supervisor only] ──► [S-06 User Management]

Every screen → Back / Nav → returns to previous screen
```

**Role-gated elements (do not render for Technician role):**
- "User Management" nav item (S-06).
- "Buat Laporan / Work Order" button on S-03.
- "Export PDF" button on S-04.
- The entire S-05 flow (only reachable via a Supervisor-gated entry point).

---

## 7. Summary Brief for Stitch (one paragraph)

Design a tablet-landscape (1280×800px) industrial equipment monitoring web app for PT Maju Teknik Industri, in both light and dark themes with full parity. Visual language: calm, confident, instrumentation-grade — soft blue-gray surfaces (`#F4F7FE` light / `#0F172A` dark), a single indigo accent (`#4318FF` / `#818CF8` dark) used sparingly for primary actions and active states, and three semantic status colors (green `#22C55E`, amber `#F59E0B`, red `#EF4444`) that drive card borders, glows, and sort order — not just badges. Typography is Plus Jakarta Sans with tabular figures for all numeric data. Persistent left side navigation on tablet/desktop, bottom nav on mobile. Design all 6 screens: Login, Dashboard (6-card equipment grid, auto-sorted fault-first, KPI summary bar, live alarm panel), Equipment Detail (gauges, trend chart with threshold line, alarm history table), Global Alarm List (filterable table with export), Report/Work Order Form, and User Management (technicians, machines, report approvals, data export — Supervisor-only). Prioritize glanceability and touch-friendliness (48px minimum targets) over decoration — this is a field tool used while walking a factory floor, not an office dashboard.
