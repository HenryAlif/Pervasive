---
version: alpha
name: Motion — Smart Industrial Asset Tagging
description: Mobile-first industrial asset tracking system for seat manufacturing plant. RFID automatic detection on jigs (Station 1-12) and pallets (conveyor to warehouse), barcode tracking on finished goods seats. Four internal teams (MES, Maintenance, PPIC, PD) monitor production flow, maintenance status, and asset history in real-time. Bold, high-contrast visual language where status and asset condition drive hierarchy — not decoration.
colors:
  primary: "#FFF12E"
  secondary: "#37380D"
  neutral: "#E6E6E6"
  surface: "#FFFFFF"
  on-surface: "#091B2B"
  active-jig: "#22C55E"
  warning-maintenance: "#F59E0B"
  fault-offline: "#EF4444"
  dark-bg: "#091B2B"
typography:
  display:
    fontFamily: Nunito
    fontSize: 28px
    fontWeight: 700
    lineHeight: 1.2
  headline-lg:
    fontFamily: Nunito
    fontSize: 20px
    fontWeight: 700
    lineHeight: 1.25
  headline-md:
    fontFamily: Nunito
    fontSize: 16px
    fontWeight: 600
    lineHeight: 1.3
  body:
    fontFamily: Nunito
    fontSize: 14px
    fontWeight: 400
    lineHeight: 1.5
  body-strong:
    fontFamily: Nunito
    fontSize: 14px
    fontWeight: 600
    lineHeight: 1.5
  caption:
    fontFamily: Nunito
    fontSize: 12px
    fontWeight: 500
    lineHeight: 1.3
    letterSpacing: 0.01em
rounded:
  sm: 6px
  md: 12px
  lg: 16px
  full: 9999px
spacing:
  xs: 4px
  sm: 8px
  md: 12px
  lg: 16px
  xl: 24px
  xxl: 32px
components:
  page:
    backgroundColor: "{colors.neutral}"
  heading-text:
    textColor: "{colors.on-surface}"
    typography: "{typography.headline-lg}"
  body-text:
    textColor: "{colors.on-surface}"
    typography: "{typography.body}"
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.on-surface}"
    rounded: "{rounded.sm}"
    height: 40px
    padding: "0 16px"
  button-secondary:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.primary}"
    borderColor: "{colors.primary}"
    rounded: "{rounded.sm}"
    height: 40px
    padding: "0 16px"
  status-active:
    backgroundColor: "{colors.active-jig}"
    textColor: "#FFFFFF"
    rounded: "{rounded.full}"
    padding: "6px 12px"
  status-warning:
    backgroundColor: "{colors.warning-maintenance}"
    textColor: "#FFFFFF"
    rounded: "{rounded.full}"
    padding: "6px 12px"
  status-fault:
    backgroundColor: "{colors.fault-offline}"
    textColor: "#FFFFFF"
    rounded: "{rounded.full}"
    padding: "6px 12px"
  card:
    backgroundColor: "{colors.surface}"
    rounded: "{rounded.md}"
    padding: "12px"
    borderColor: "{colors.neutral}"
  input:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    rounded: "{rounded.sm}"
    height: 40px
    padding: "8px 12px"
---

# Design System — Motion

## Overview

Motion is a **real-time industrial asset tracking system** deployed on mobile devices for a seat manufacturing plant. Three main technologies work together:

1. **RFID (automatic detection):** Jigs move through production stations 1–12, pallets move on conveyor to warehouse — RFID readers capture data automatically as assets pass. Technician takes no scan action.
2. **Barcode (manual gun scanner):** Finished seat goods carry barcode for full traceability. Gun scanner sends data to PC; mobile app displays tracking info only (read-only).
3. **Mobile app:** MES, Maintenance, PPIC, and PD teams monitor dashboard, track barcode info, manage RFID asset registry, view maintenance alerts, and analyze trends — all on-the-go from a phone.

The design system is **bold and high-contrast** — navy-and-gold brand identity (Motion), with a separate semantic color language for asset condition (green = active, amber = needs attention, red = offline/fault). Every screen must answer the core question in under 3 seconds: *What is the status of my jigs, pallets, and production flow right now?*

## Colors

### Brand Palette
- **Primary (`#FFF12E`):** Bold, high-energy gold-yellow. Used for primary CTAs, active states, accent elements. Must pop on dark backgrounds.
- **Secondary (`#37380D`):** Deep olive. Used for secondary UI and supporting text when primary is too bright.
- **On-surface (`#091B2B`):** Navy dark. Text, headings, primary foreground — sharp contrast against white surfaces.
- **Dark BG (`#091B2B`):** Navy. Optional dark theme background (not primary, but mentioned for future expansion).
- **Neutral (`#E6E6E6`):** Light gray. Page backgrounds, disabled states, subtle dividers.
- **Surface (`#FFFFFF`):** Pure white. Card, panel, and input backgrounds.

### Semantic / Status Colors (identical across all themes)
- **Active (`#22C55E`):** Jig/pallet actively running, production moving, RFID tag detected and online.
- **Warning (`#F59E0B`):** Maintenance due, attention needed, minor issue detected.
- **Fault (`#EF4444`):** Offline, RFID not responding, production halted, critical maintenance required.

These three colors are the protagonists of the system. They drive card borders, status badge fills, and sort order on the dashboard — not decoration, but critical information hierarchy.

## Typography

**Font family:** Nunito throughout. Fallback stack: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, sans-serif.

Numeric data (RFID IDs, sequence numbers, lot numbers, station numbers, timestamps) — use tabular figures where available so columns align vertically.

- **Display (28px, Bold):** Splash screen branding, page titles.
- **Headline Large (20px, Bold):** Dashboard title, major section headers, card titles.
- **Headline Medium (16px, Semibold):** Sub-section headers, modal titles, data labels.
- **Body (14px, Regular):** Main content, descriptions, table cells, list items.
- **Body Strong (14px, Semibold):** Emphasized values, asset IDs, key data points.
- **Caption (12px, Medium):** Timestamps, units, table headers, secondary info.

## Layout & Grid

**Target device:** Mobile phone, portrait orientation (primary). Secondary support: tablet landscape (follow tablet rules if layout permits).

**Mobile grid:** 4 columns (narrow screens), 8-point spacing scale (4, 8, 12, 16, 24, 32px). Safe area margins: 12px left/right.

**Primary screen dimensions:** 360×800px (base case — responsive up to 480px width). Assume small screen, gloved fingers, reading in harsh factory lighting.

Every interactive element: **minimum 40px height** (touch target). No tiny buttons.

## Elevation & Depth

**Resting state (normal operation):** Soft, subtle shadows on cards — barely perceptible lift against the neutral background. No decoration.

**Asset state signals depth differently:**
- **Active (green):** Thin green left-border on card, optional subtle glow. Feels calm, confident, "everything is fine."
- **Warning (amber):** Thin amber left-border, slightly more visible shadow. Draws attention gently.
- **Fault (red):** Bold red left-border + noticeable colored shadow/glow. Must visibly stand out — production is stopped or at risk.

This is the single most important depth rule: **elevation communicates asset health, not just affordance.**

## Shapes

**Corner radius scale (consistent everywhere):**
- `sm` 6px: buttons, inputs, small badges
- `md` 12px: cards, standard components
- `lg` 16px: modals, large containers
- `full` 9999px: status badges (pills)

Never mix radii arbitrarily within a view. Consistency builds polish.

## Components

### Status Badge (Jig / Pallet / Seat Condition)
- Pill-shaped, flat color fill (never gradient).
- Text: white, bold, 12-14px.
- Labels: "Active", "Attention Required", "Offline".
- Height: 28px for inline/table use, 36px for header-level display.
- Padding: 6–12px horizontal.
- These badges appear on dashboard cards, detail screens, alert rows — always consistent styling.

### Button
| Variant | Background | Text | Border | Usage |
|---|---|---|---|---|
| Primary | `#FFF12E` (gold) | `#091B2B` (navy) | None | Main CTA ("Scan", "Update", "Submit") |
| Secondary | `#FFFFFF` (white) | `#FFF12E` (gold) | 1px gold | Secondary actions, cancel |
| Disabled | `#E6E6E6` (gray) | `#FFFFFF` | None | Inactive state |

- Height: 40px minimum.
- Corner radius: 6px.
- Label: always visible text, never icon-only on primary actions.

### Jig / Pallet Status Card
Displayed on Dashboard in a scrollable list or grid. Each card shows:
- **Asset ID** (RFID ID, large tabular font) — e.g., "JIG-0847" or "PLT-123"
- **Current location/station** (for jigs) or **current position** (for pallets) — e.g., "Station 05" or "Conveyor Segment 02"
- **Status badge** — Active/Warning/Fault
- **Sequence number** (if applicable) — e.g., "Seq: 542"
- **Last detected** timestamp — e.g., "09:34:22"
- **Left border accent** — color matches status (green/amber/red)

Card height: 80–100px. Tap opens detail screen.

### RFID Tag Registry Row (Manage RFID screen)
For CRUD operations. Each row shows:
- **RFID ID** (editable text field)
- **Asset type** (Jig / Pallet, dropdown)
- **Asset name** (editable text field)
- **Status** (display-only badge, pulled from current tag detection)
- **Action buttons** — Edit (pencil icon) · Delete (trash icon)

Tappable row for full-screen detail / edit modal.

### Barcode Info Card (Barcode Scan screen)
Displays read-only tracking information from scanned barcode:
- **Sequence** (tabular font)
- **Product Code**
- **Part Number**
- **Lot Number**
- **Datetime** of barcode assignment
- Optional: **QR/barcode image** thumbnail if stored in database

Background: subtle gray tint to show this is "read-only, informational" vs. editable input.

### Alert Item (Alerts screen)
Each alert row contains:
- **Alert icon** (warning triangle or alert symbol, color-coded)
- **Alert title** — e.g., "JIG-0847 Maintenance Overdue"
- **Alert timestamp**
- **Severity badge** (Warning / Fault)
- **Dismiss or detail button** (arrow icon)

Tap opens alert detail / dismissal flow.

### Analytics Chart Widget
Simple bar or line chart showing:
- **X-axis:** Time (months or weeks)
- **Y-axis:** Alert count (or breakdown: jigs vs. pallets)
- **Color coding:** amber for warnings, red for faults, neutral for normal
- **Touch interaction:** optional tap-to-show-details, no complex hover states (mobile)

Keep visual simple — data density over animation.

## Do's and Don'ts

**Do:**
- Let asset status (green/amber/red) drive visual hierarchy — border color, glow, sort order.
- Keep the resting (all-green) state calm and quiet — soft background, plenty of white space.
- Use tabular/aligned numeric figures everywhere an ID, sequence, or timestamp appears.
- Keep primary actions (buttons) clearly labeled with text — field teams need certainty, not guessing.
- Maintain the corner-radius scale consistently across all components.
- Use the gold-yellow accent for CTAs and active states; let it pop on dark/neutral backgrounds.

**Don't:**
- Decorate with illustrations, gradients-for-decoration, or "friendly SaaS" pastels.
- Create low-contrast gray-on-gray text — this app is read under factory lighting, not office lighting.
- Mix rounded and sharp corners in the same view.
- Use decorative gradients on buttons or cards.
- Hide primary navigation — all nav items should be visible (side rail on tablet, bottom bar on mobile).
- Rely on color alone for meaning — always pair status color with text label or icon.

**Accepted caveat:** The three status badges (green/amber/red with white text) do not individually exceed WCAG AA 4.5:1 text contrast at their exact hex values — this is intentional. These are the CONFIRMED brand status colors and are never substituted. Legibility is carried by: bold weight (600+), large pill size (28–36px), color redundancy with adjacent text label ("Active" / "Attention Required" / "Offline"), and consistent placement.

## Component Interactions

- **Tap status badge** (on dashboard card): Opens detail screen for that jig/pallet.
- **Tap card row**: Depends on screen — may open detail, edit modal, or focus view.
- **Long-press**: Reserved for future multi-select on Manage RFID screen.
- **Swipe**: Not primary — avoid due to accidental triggers in factory setting.
- **Buttons**: Standard tap, visual feedback on press (opacity change or slight scale), haptic feedback optional.
