# Motion — Smart Industrial Asset Tagging
### UI Design Brief for Google Stitch → Figma Handoff

---

## 0. How to Use This Document

This brief is written to be dropped directly into Google Stitch as a design prompt. It contains everything needed to generate a cohesive, production-grade mobile UI: product context, art direction, design tokens, component specs, and all 7 screens.

**Client:** Internal, Seat Manufacturing Plant  
**Platform:** Mobile web app, portrait orientation  
**Primary target:** 360 × 800px (standard mobile), expandable to 480px  
**Users:** MES team, Maintenance team, PPIC team, PD team (all roles see same screens; login only differentiates identity)

---

## 1. Product Context

Motion is a **real-time industrial asset tracking application** for a seat manufacturing plant. The system integrates three data collection methods:

### Assets Tracked
1. **Jigs** (RFID-tagged production equipment) — Follow products through Assembly Line Stations 1–12, used in the seat-building process.
2. **Pallets** (RFID-tagged) — Transport finished seat goods from Station 12 onward via conveyor system to warehouse areas.
3. **Finished Seat Goods** (barcode-labeled) — Each completed seat carries a unique barcode with full production traceability.

### Data Collection
- **RFID (automatic):** Jigs and pallets are read automatically as they move through stations / on conveyors. No manual scan action required. RFID reader sends data to PC database in real-time.
  - Jig payload: RFID ID, Station number, Sequence, Datetime
  - Pallet payload: RFID ID, Sequence, Datetime
- **Barcode (gun scanner input):** Finished seats are scanned with a handheld gun scanner. Data flows: gun scanner → PC database. Mobile app displays read-only tracking only; the app is not a barcode scanner itself.
  - Barcode payload: Sequence, Product Code, Part Number, Lot Number, Datetime

### User Context
Four internal teams operate Motion:
- **MES Team** — Monitor production flow, track asset movement in real-time.
- **Maintenance Team** — View asset condition, maintenance history, and alerts; plan preventive maintenance.
- **PPIC Team** — Plan production, monitor capacity, track finished goods traceability.
- **PD Team** — Support all teams, view analytics and historical trends.

**Core user need:** Understand asset status and production flow **in under 3 seconds from any phone**, anywhere in the plant — in harsh lighting, while walking, often with one hand.

---

## 2. Design Direction — The Taste

Think **industrial control dashboard**, not office SaaS. The reference is modern SCADA/HMI interfaces crossed with bold, high-confidence brand identity. Motion uses a **navy-and-gold color language** — the brand (Motion) is confident and energetic; the product (asset tracking) is calm and precise.

**Three principles to hold onto for every screen:**

1. **Status color drives hierarchy, not brand color.** Green (active), amber (maintenance needed), red (offline/fault) are the visual protagonists. They determine card borders, glow intensity, and sort order on the dashboard. The gold brand accent is reserved for CTAs and active UI states only — it never competes with status colors.

2. **Numeric data is always tabular and aligned.** Jig IDs, sequence numbers, lot numbers, station numbers, timestamps — they appear in monospaced or tabular-figure treatment so columns of numbers are scannable at a glance, like rows of gauges in a physical control panel.

3. **One accent color, used with discipline.** Gold (`#FFF12E`) is the single brand accent — primary buttons, active navigation, focus rings. It pops on dark surfaces and draws attention to actionable elements.

**Avoid at all costs (anti-AI-slop checklist):**
- Generic rounded-everything "friendly startup" aesthetic with pastel blobs.
- Decorative gradients on buttons or cards.
- Centered hero sections with marketing-style illustrations.
- Icon-only buttons on primary actions — field teams need text labels.
- Low-contrast gray-on-gray text that fails a glance-test under bright factory lighting.
- Inconsistent corner radii or shadow depths between components.

**Mood to channel:** Aviation instrument panels (Garmin, G1000), modern HMI software (Siemens WinCC, Ignition), premium fitness dashboards (Oura) for calm-data-density — but warmer and more legible, with bold brand color presence.

---

## 3. Design Tokens

### 3.1 Color — Primary Brand Palette

| Token | Hex | Usage |
|---|---|---|
| `color-primary` | `#FFF12E` | Primary buttons, active nav, focus rings, accent highlights |
| `color-secondary` | `#37380D` | Secondary text, supporting UI, muted backgrounds |
| `color-on-surface` | `#091B2B` | Headings, primary text, strong contrast foreground |
| `color-surface` | `#FFFFFF` | Card / panel backgrounds |
| `color-neutral` | `#E6E6E6` | Page background, disabled states, subtle dividers |
| `color-dark-bg` | `#091B2B` | Optional: dark theme page background (future) |

### 3.2 Color — Semantic / Status (identical across light and dark themes)

| Token | Hex | Meaning | Label |
|---|---|---|---|
| `color-status-active` | `#22C55E` | Jig/pallet actively running, RFID detected, production moving | "Active" |
| `color-status-warning` | `#F59E0B` | Needs attention, maintenance due, minor alert | "Attention Required" |
| `color-status-fault` | `#EF4444` | Offline, RFID not responding, production halted, critical | "Offline" |

**Text on any status badge is always white (`#FFFFFF`), bold weight, for high contrast regardless of background.**

### 3.3 Typography

**Font family:** Nunito (primary). Fallback stack: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, sans-serif.
**Numeric data:** Use tabular/monospaced figures where available so columns align (e.g., sequence numbers, RFID IDs, station numbers).

| Token | Size | Weight | Usage |
|---|---|---|---|
| `text-display` | 28px | Bold (700) | Page titles, splash screen branding |
| `text-headline-lg` | 20px | Bold (700) | Dashboard title, major section headers, card titles |
| `text-headline-md` | 16px | Semibold (600) | Sub-section headers, modal titles, data field labels |
| `text-body` | 14px | Regular (400) | Main content, descriptions, table cells, list items |
| `text-body-strong` | 14px | Semibold (600) | Emphasized values, asset IDs, key data points |
| `text-caption` | 12px | Medium (500) | Timestamps, units, table headers, secondary info |

### 3.4 Spacing (4-point grid, scaled for mobile)

| Token | Value | Usage |
|---|---|---|
| `space-xs` | 4px | Micro-spacing within components |
| `space-sm` | 8px | Gap between tightly related elements, internal padding |
| `space-md` | 12px | Standard card padding, gaps between UI elements |
| `space-lg` | 16px | Section spacing, modal margins |
| `space-xl` | 24px | Major section breaks, top/bottom breathing room |
| `space-xxl` | 32px | Page-level spacing (header top, footer bottom) |

### 3.5 Grid & Layout

- **Grid system:** Mobile-first, 4 columns for narrow screens (360–480px). 8px base grid with 4px sub-grid for micro-alignment.
- **Safe area:** 12px margin left/right on all screens.
- **Touch target minimum:** 40px height (glove-friendly interface). No exceptions.
- **Corner radius scale:**
  - `sm` 6px (buttons, inputs, small badges)
  - `md` 12px (cards, standard components)
  - `lg` 16px (modals, large containers)
  - `full` 9999px (status badge pills)

---

## 4. Core Components

### 4.1 Status Badge

A **pill-shaped label** showing jig, pallet, or production status at a glance.

- **Background:** Status color (`#22C55E` / `#F59E0B` / `#EF4444`).
- **Text:** White, bold, 12–14px, centered. Labels: "Active" / "Attention Required" / "Offline".
- **Height:** 28px for inline use (list rows, table cells), 36px for header-level display (detail screen top).
- **Padding:** 6–12px horizontal.
- **No border, no gradient** — flat, confident color fill.

### 4.2 Button

| Variant | Background | Text | Border | Usage |
|---|---|---|---|---|
| Primary | `#FFF12E` | `#091B2B` | None | Main CTA ("Scan", "Update", "Save") |
| Secondary | `#FFFFFF` | `#FFF12E` | 1px gold | Secondary actions, cancel, dismiss |
| Disabled | `#E6E6E6` | `#FFFFFF` | None | Inactive state, reduced opacity |

- Height: 40px minimum.
- Width: full-width on mobile (12px margin left/right).
- Corner radius: 6px (`radius-sm`).
- Label: always visible text, never icon-only for primary actions (field users need certainty).

### 4.3 Jig / Pallet Status Card

Displayed on **Dashboard** in a scrollable vertical list.

**Contents:**
1. **RFID ID** — Large, tabular font (e.g., "JIG-0847" or "PLT-123"). Left-aligned, bold.
2. **Location/Position** — e.g., "Station 05" (for jigs) or "Conveyor Seg 2" (for pallets). Secondary text color, smaller font.
3. **Status Badge** — Positioned top-right of card. "Active" / "Attention Required" / "Offline".
4. **Key data row** — Sequence and last-detected timestamp (tabular font). E.g., "Seq: 542 | 09:34:22".
5. **Left border accent** — Full height, 3–4px, color-matched to status (green/amber/red).

**Card dimensions:** ~80–100px height, full-width minus margins. Tap opens detail screen for that asset.

**Emergency visual hierarchy:** Card in **Fault (red)** state gets the bold colored left-border plus a subtle elevated shadow in red hue — must visibly stand out. **Warning (amber)** state similar, less intense. **Active (green)** state stays quiet: thin green border, standard elevation.

### 4.4 RFID Tag Registry Row (Manage RFID screen)

Each row represents one tag entry (jig or pallet). Structure for CRUD operations:

| Column | Content | Editable? | Notes |
|---|---|---|---|
| RFID ID | `JIG-xxxx` or `PLT-xxxx` | Yes, in edit mode | Tabular font for alignment |
| Asset Type | Jig / Pallet | Yes, dropdown | Display as badge or tag |
| Asset Name | Custom name (optional) | Yes | Editable text field |
| Status | Badge (Active/Attention Required/Offline) | No, display-only | Pulled from current RFID detection |
| Actions | Edit · Delete | Yes | Icon buttons (pencil, trash) |

Tap row to open full-screen detail / edit modal. Swipe-to-delete optional (depends on UX validation).

### 4.5 Barcode Info Card (Barcode Scan screen)

Displays **read-only** tracking information from a scanned seat barcode.

**Contents:**
- **Barcode image** (optional thumbnail)
- **Sequence** (large, tabular font)
- **Product Code**
- **Part Number**
- **Lot Number**
- **Datetime** (when barcode was assigned / scanned)

Background: subtle gray tint (`color-neutral`) to indicate "informational, read-only" — not an input form.

Tap to expand / see full history (optional detail modal).

### 4.6 Alert Item (Alerts screen)

Each alert row conveys urgency and actionability.

**Contents:**
1. **Alert icon** — Warning triangle or alert symbol, color-coded (amber or red).
2. **Alert title** — e.g., "JIG-0847 Maintenance Overdue" or "PLT-456 RFID Offline".
3. **Timestamp** — When alert was triggered (e.g., "09:34" or "2 hours ago").
4. **Severity badge** — "Attention Required" or "Offline" (status badge pattern).
5. **Action button** — Arrow (→) or "View" to open detail / dismissal flow.

Minimum row height: 56px (touch-friendly). Tap anywhere on row opens detail.

### 4.7 Analytics Chart Widget (Analytics screen)

Simple, clean data visualization showing alert trends over time.

**Chart type:** Bar or line chart (your choice; bar is simpler for mobile).
**X-axis:** Time periods (weeks or months).
**Y-axis:** Alert count.
**Color coding:** Amber for "Perlu Perhatian", red for "Offline", neutral for no alerts.

**Interaction:** Tap a bar/point to show exact count. Avoid complex hover or swipe animations — mobile factory environment doesn't favor gestures.

---

## 5. Screens

### S-01 — Splash Screen

**Purpose:** App branding, first impression, loading state.

**Elements:**
- Motion logo / branding (centered, large — 120px+).
- Optional app tagline: "Smart Asset Tracking" (subtitle, secondary text color).
- Loading animation (spinner or progress bar, subtle).
- Optional company badge / "PT Maju Teknik Industri" at bottom.

**Duration:** 2–3 seconds (auto-advance to login on first launch; skip on subsequent launches).

---

### S-02 — Login Screen

**Purpose:** Authenticate user before dashboard access.

**Layout:** Centered card on neutral background, generous white space, clean and utilitarian.

**Elements:**
- Motion logo / branding at top of card.
- **User ID input field** (48px min height). Placeholder: "Enter User ID" (e.g., MES-001, MAINT-05).
- **Password input field** (48px min height, show/hide toggle icon).
- **Checkbox:** "Remember Me" — optional, for returning users on shared tablets.
- **Text link:** "Forgot Password?" — right-aligned below password field.
- **Primary button:** "Login", 48px height, full-card width (minus padding).

**States to design:**
- Default (empty fields).
- Filled (valid input, button active, gold color).
- Error (wrong credentials) — red error message beneath field, input border turns fault-red.
- Loading (authenticating) — button shows spinner, label dims, disabled state.

---

### S-03 — Dashboard (Main Screen)

**Purpose:** Assess jig, pallet, and production status **in under 3 seconds**. This is the screen the app is built around.

**Layout, top to bottom:**

1. **Header bar** — Logged-in user name ("MES-001" or "Maintenance Team"), last-updated timestamp (live-updating), small connection status indicator (dot: green=online, gray=offline).

2. **KPI summary row** — Four stat tiles in horizontal scroll or 2×2 grid (adapt to screen width):
   - **Total Jigs** (number, neutral color)
   - **Total Pallets** (number, neutral color)
   - **Jigs in Maintenance** (number, amber color)
   - **Pallets in Maintenance** (number, amber color)
   
   Each tile is a small card (touch target 40px+ min) showing the count prominently with a label.

3. **Status summary bar** — Optional; shows count of assets by status:
   - 🟢 **Active:** n
   - 🟡 **Attention Required:** n
   - 🔴 **Offline:** n
   
   Or use badge pills inline.

4. **Jig / Pallet card list** — Scrollable vertical list of Status Cards (§4.3). **Auto-sort order: Fault (red) first, then Warning (amber), then Active (green)** — urgent assets always top.

5. **Recent alerts panel** — Optional; shows 2–3 most recent unresolved alerts (compact list view, expandable).

6. **Bottom navigation** (if using bottom nav for 4 main sections):
   - Dashboard (active, highlighted in gold)
   - Barcode Scan
   - Manage RFID
   - Alerts

---

### S-04 — Barcode Scan / Tracking

**Purpose:** View read-only tracking information for scanned / finished seat goods.

**Elements:**

1. **Top bar** — Title "Barcode Scan" and a "Clear" button to reset.

2. **Barcode input / search field** (or camera integration if app supports it):
   - Placeholder: "Scan barcode or search sequence..."
   - Button: "Scan" (camera icon) or input field auto-triggers camera on focus.
   - Clear button (×) inside field.

3. **Barcode Info Card** (§4.5) — Displays once barcode is scanned or sequence entered:
   - Barcode image (if available)
   - Sequence (large, tabular)
   - Product Code
   - Part Number
   - Lot Number
   - Datetime
   - Optional: "View Full History" button

4. **History list** (optional, collapsible) — Previous scans in this session, listed reverse-chronologically.

---

### S-05 — Manage RFID

**Purpose:** Create, update, delete tag entries for jigs and pallets.

**Elements:**

1. **Top bar** — Title "Manage RFID" and a "+" (Add) button.

2. **Filter tabs** (optional):
   - All
   - Jigs
   - Pallets

3. **Tag registry list** — Each row is a RFID Tag Registry Row (§4.4):
   - RFID ID · Asset Type · Name · Status · Actions (edit, delete)
   - Tap row to open detail / edit modal.

4. **Add / Edit Modal** (tap "+" or edit icon):
   - **RFID ID** (text input, required) — auto-format as `JIG-xxxx` or `PLT-xxxx`
   - **Asset Type** (radio or dropdown) — Jig or Pallet
   - **Asset Name** (text input, optional) — Custom name
   - **Primary button:** "Save"
   - **Secondary button:** "Cancel"

---

### S-06 — Alerts

**Purpose:** View all unresolved alerts and maintenance-due notifications.

**Elements:**

1. **Top bar** — Title "Alerts" and a "Refresh" button (manual sync with database).

2. **Filter tabs**:
   - All
   - Attention Required (warnings)
   - Offline (faults)

3. **Alert list** — Scrollable list of Alert Items (§4.6), sorted by severity (Offline first, then Attention Required):
   - Icon · Title · Timestamp · Badge · Action (→)
   - Tap to open alert detail.

4. **Empty state** (if no alerts):
   - "No Alerts"
   - ✓ All systems running normally

---

### S-07 — Analytics (Optional but Recommended)

**Purpose:** Analyze trends — alert frequency, maintenance patterns, asset reliability over time.

**Elements:**

1. **Top bar** — Title "Analytics" and a date-range picker (optional; default to "Last 30 days").

2. **Summary cards** (optional):
   - **Total Alerts (This Period):** number (neutral color)
   - **Avg. Alert Per Day:** number
   - **Offline Time:** total hours/minutes

3. **Main chart** — Analytics Chart Widget (§4.7):
   - Bar or line chart showing alert count by week or month.
   - Breakdown by alert type (Attention Required / Offline) or asset type (Jig vs. Pallet).
   - Color-coded bars (amber/red).

4. **Data table** (optional, below chart):
   - Columns: Period · Attention Required Count · Offline Count
   - Rows: weekly or monthly breakdown
   - Sortable by column.

---

## 6. User Flow

```
[S-01 Splash]
     │ (auto-advance after 2–3s)
     ▼
[S-02 Login]
     │ (tap "Login", success)
     ▼
[S-03 Dashboard] ◄─────────────┐
     │                         │
     ├─ tap Jig card ─→ (future: opens detail, not in scope yet)
     │                         │
     ├─ tap nav: Barcode Scan ─┤
     ▼                         │
[S-04 Barcode Scan]            │
     │                         │
     └─ tap nav: back ─────────┘

[S-03 Dashboard]
     │
     ├─ tap nav: Manage RFID
     ▼
[S-05 Manage RFID]
     │ (create/edit/delete tags)
     └─ tap nav: back ─────────┐
                               │
[S-03 Dashboard]               │
     │                         │
     ├─ tap nav: Alerts        │
     ▼                         │
[S-06 Alerts]                  │
     │                         │
     └─ tap nav: back ─────────┤
                               │
[S-03 Dashboard]               │
     │                         │
     ├─ tap nav: Analytics     │
     ▼                         │
[S-07 Analytics]               │
     │                         │
     └─ tap nav: back ─────────┘
```

**Navigation:**
- Primary sections: Dashboard, Barcode Scan, Manage RFID, Alerts, Analytics.
- Back button or nav tap returns to Dashboard.
- No role-based hiding — all 5 sections visible to all 4 teams.

---

## 7. Key Interactions & Micro-Behaviors

- **Jig / Pallet card tap:** Loads asset detail (future enhancement; for prototype, can be a modal overlay showing full tag history).
- **Status badge color:** Drives urgency perception; no additional animation needed (factory lighting is harsh enough).
- **Button press:** Visual feedback via slight opacity change or scale; haptic feedback optional but nice-to-have.
- **Empty states:** Show relevant icon + message (e.g., "No Alerts" when Alerts screen is empty).
- **Refresh button:** Manual sync with database, shows brief loading spinner.
- **Add/Edit modal:** Overlay on previous screen, with semi-transparent backdrop. On dismiss, returns to list view.

---

## 8. Summary Brief for Stitch

Design a **mobile-first web app** (360×800px primary, scalable to 480px) for real-time industrial asset tracking at a seat manufacturing plant. Use Motion brand identity (navy `#091B2B` on-surface, bold gold `#FFF12E` accent) with separate semantic status colors (green/amber/red for asset condition). Nunito font throughout, tabular figures for all numeric data (RFID IDs, sequences, station numbers, timestamps). Seven screens: Splash (branding + loading), Login (clean centered form), Dashboard (KPI summary + scrollable Jig/Pallet card list, auto-sorted by status, fault-first), Barcode Scan (read-only tracking info), Manage RFID (CRUD tag registry), Alerts (unresolved alerts by severity), Analytics (trend charts, optional). All four user roles (MES, Maintenance, PPIC, PD) see identical navigation and screens — no role-based hiding. Prioritize glanceability and touch-friendliness (40px+ buttons, 56px+ rows) for factory floor use — cold, harsh lighting, often one-handed, gloved interaction. Status colors are visual protagonists; brand gold is reserved for CTAs and active states only. Layout is calm and precise, not decorative. RFID data flows automatically (no manual scan); barcode data is gun-scanner input displayed read-only on app.
