---
version: alpha
name: Pervasive — Industrial Equipment Monitoring
description: Tablet-first industrial equipment monitoring system for field technicians and supervisors at PT Maju Teknik Industri. A calm, instrumentation-grade visual language where status color — not brand color — drives visual hierarchy.
colors:
  primary: "#4318FF"
  secondary: "#A3AED0"
  neutral: "#F4F7FE"
  surface: "#FFFFFF"
  on-surface: "#2B3674"
  success: "#22C55E"
  warning: "#F59E0B"
  error: "#EF4444"
typography:
  headline-display:
    fontFamily: Plus Jakarta Sans
    fontSize: 32px
    fontWeight: 700
    lineHeight: 1.2
  headline-lg:
    fontFamily: Plus Jakarta Sans
    fontSize: 24px
    fontWeight: 700
    lineHeight: 1.25
  headline-md:
    fontFamily: Plus Jakarta Sans
    fontSize: 18px
    fontWeight: 600
    lineHeight: 1.3
  body-md:
    fontFamily: Plus Jakarta Sans
    fontSize: 16px
    fontWeight: 400
    lineHeight: 1.5
  body-md-strong:
    fontFamily: Plus Jakarta Sans
    fontSize: 16px
    fontWeight: 600
    lineHeight: 1.5
  label-sm:
    fontFamily: Plus Jakarta Sans
    fontSize: 13px
    fontWeight: 500
    lineHeight: 1.3
    letterSpacing: 0.01em
rounded:
  sm: 8px
  md: 16px
  lg: 24px
  full: 9999px
spacing:
  xs: 8px
  sm: 16px
  md: 24px
  lg: 32px
  xl: 48px
components:
  page:
    backgroundColor: "{colors.neutral}"
  heading-text:
    textColor: "{colors.on-surface}"
    typography: "{typography.headline-lg}"
  body-text:
    textColor: "{colors.secondary}"
    typography: "{typography.body-md}"
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "#FFFFFF"
    rounded: "{rounded.sm}"
    height: 48px
    padding: 16px
  button-secondary:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.primary}"
    rounded: "{rounded.sm}"
    height: 48px
    padding: 16px
  button-disabled:
    backgroundColor: "{colors.secondary}"
    textColor: "#FFFFFF"
    rounded: "{rounded.sm}"
    height: 48px
  badge-normal:
    backgroundColor: "{colors.success}"
    textColor: "#FFFFFF"
    rounded: "{rounded.full}"
    padding: 12px
  badge-warning:
    backgroundColor: "{colors.warning}"
    textColor: "#FFFFFF"
    rounded: "{rounded.full}"
    padding: 12px
  badge-fault:
    backgroundColor: "{colors.error}"
    textColor: "#FFFFFF"
    rounded: "{rounded.full}"
    padding: 12px
  card:
    backgroundColor: "{colors.surface}"
    rounded: "{rounded.md}"
    padding: 16px
  input:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    rounded: "{rounded.sm}"
    height: 48px
    padding: 16px
---

# Design System

## Overview

Pervasive is a field instrument, not an office dashboard. It runs on a tablet carried by a technician walking a factory floor — often with one hand, often under harsh or uneven lighting. The entire visual system exists to answer one question in under three seconds: *is everything normal, or does something need attention right now?*

The personality is **industrial command center**: calm and quiet when all six machines are healthy, visibly "woken up" the instant something isn't. Think aviation cockpit displays and modern SCADA/HMI software crossed with the typographic discipline of a premium consumer product — never a generic rounded-everything SaaS admin template, never decorative for decoration's sake. Every pixel should justify itself as either data or necessary structure.

## Colors

The palette is a soft blue-gray neutral base with a single disciplined accent, plus three semantic status colors that are the real protagonists of the system.

- **Primary (`#4318FF`):** The one brand accent. Used sparingly — primary buttons, active navigation state, links, focus rings. If a screen ever has both the primary accent and a fault badge competing for attention, the fault color must win.
- **Secondary (`#A3AED0`):** Muted cool gray-blue for secondary text, captions, labels, disabled states, placeholder content.
- **Neutral (`#F4F7FE`):** Page background. Soft, slightly cool, never stark white — gives surfaces something to sit on top of.
- **Surface (`#FFFFFF`):** Card and panel backgrounds. Clean white against the neutral page background creates the base elevation layer.
- **On-surface (`#2B3674`):** Dark navy for headings, titles, and primary text — chosen for strong contrast against both surface and neutral, never pure black.
- **Success (`#22C55E`):** Operating normally. Quiet in resting state — this color should feel unremarkable when everywhere.
- **Warning (`#F59E0B`):** Needs attention. Should visually interrupt the calm of the success state.
- **Error (`#EF4444`):** Fault / critical. The most urgent color in the system — reserved exclusively for genuine fault states, never reused decoratively.

These three status colors are not just badge fills. They drive card border color, glow intensity, and sort order across the dashboard. A faulted machine should pull the eye before any text is read.

**Dark theme companion palette** (for when a dark variant of this product is generated): background `#0F172A`, surface `#1E293B`, primary `#818CF8` (lightened indigo for dark contrast), heading text `#E2E8F0`, body text `#94A3B8`. The three status colors stay identical in both themes — they are the one piece of the system that must never shift. This dark palette is documented here as design intent only; it is not encoded as formal tokens in this file, since this system targets the light theme as the primary, fully-specified mode.

## Typography

**Font family:** Plus Jakarta Sans throughout. Fallback stack: Inter, Roboto, system-ui, sans-serif.

Numeric readouts — temperatures, pressures, voltages, machine IDs — should always render with tabular/monospaced figures where the renderer supports it, so columns of numbers stay visually aligned. This is instrumentation; numbers must read like a column of gauges, not like prose.

- **Headline Display (32px, Bold):** Page-level titles.
- **Headline Large (24px, Bold):** Card titles, machine names, section headers.
- **Headline Medium (18px, Semibold):** Sub-section headers, modal titles.
- **Body (16px, Regular):** Main content, descriptions, table cells.
- **Body Strong (16px, Semibold):** Emphasized values, key data points.
- **Label (13px, Medium):** Captions, timestamps, units, table headers.

## Layout

Primary target is tablet landscape, 1280×800px (also supports 1194×834px). The grid is 12 columns with 16px margins and 16px gutters, built on a strict 8-point spacing scale (8 / 16 / 24 / 32 / 48px).

Side navigation stays persistently open on tablet and desktop (≥768px) — it never collapses at this breakpoint, since a field technician should never have to tap to reveal navigation. Below 768px it becomes a bottom navigation bar rather than a hamburger menu, for the same one-tap-access reason.

Every interactive element has a minimum touch target of 48×48px — this is a glove-friendly interface used while walking, not a precision-pointer desktop UI.

## Elevation & Depth

Depth in the resting state is soft and quiet: low-opacity, diffuse shadows lift cards gently off the neutral background — no hard drop shadows, no heavy skeuomorphism.

Urgency is communicated differently from ordinary elevation. A card in **Fault** state gets a colored border (and a very subtle glow in the same hue) in addition to its normal elevation — it should visibly "light up" rather than simply sit higher. **Warning** state gets the same treatment, less intense, in amber. **Normal** state cards stay visually quiet: thin neutral border, standard soft shadow, no color bleed. This is the single most important depth rule in the system — elevation here is a signal of health, not just a decorative affordance.

## Shapes

A consistent, disciplined corner-radius scale: 8px for buttons and inputs, 16px for cards, 24px for modals, fully rounded (pill) for status badges. Radius is never mixed arbitrarily within the same view — pick the right scale level for the component type and hold it everywhere that component type appears.

## Components

- **Buttons:** Primary fills with the accent color and white text; secondary is a white/surface fill with accent-colored text and border; disabled uses the muted secondary color at reduced emphasis. Always labeled — never icon-only for a primary action, since field users need certainty, not interpretation. 48px height minimum.
- **Status Badge:** Flat, pill-shaped, color-filled (never gradient or outline-only), bold white label text. This is the atomic unit of "at a glance" status communication and appears identically whether inline in a table, on an equipment card, or large-format in a detail-screen header.
- **Equipment Card:** Machine name, ID, status badge, 2–3 key parameter values in tabular alignment, and a small sparkline trend. Cards auto-sort by urgency — fault first, then warning, then normal — and the fault/warning hierarchy from "Elevation & Depth" applies directly to this component. This is the component the entire dashboard is built around.
- **Navigation:** Persistent side rail with icon + label (never icon-only) on tablet/desktop; bottom bar on mobile. Role-gated items (e.g. supervisor-only sections) are simply absent for other roles, never shown disabled.
- **Data Table:** Muted, semibold header row with a thin bottom border; minimum 56px row height for comfortable tap targets; status/severity values always render as the Status Badge component, never as plain colored text.
- **Gauge / Value Card:** Large tabular numeric value with its unit as a label, paired with a circular or horizontal gauge arc colored by current health status (not the brand accent) so the gauge itself communicates condition at a glance.

## Do's and Don'ts

- Do let status color drive hierarchy — border glow and sort order, not just a small badge in a corner.
- Do keep the resting (all-normal) state visually quiet — plenty of soft neutral space, no competing color noise.
- Do use tabular/aligned numeric figures everywhere a measurement appears.
- Do keep the primary accent color reserved for actions and active states only — never let it compete with a status color.
- Do maintain a consistent corner-radius scale; never mix rounded and sharp corners in the same view.
- Do keep every primary action labeled with text, never icon-only.
- Don't use illustrations, mascots, pastel gradient blobs, or any "friendly SaaS" decorative language — this is a precision instrument, not a marketing surface.
- Don't use low-contrast gray-on-gray text; it fails the glance-test under harsh factory lighting.
- Don't apply decorative gradients to cards or buttons.
- **Accepted exception:** the three status badges (success/warning/error backgrounds with white text) do not individually clear the strict WCAG AA 4.5:1 text-contrast ratio at their exact hex values — this is intentional. These are the three CONFIRMED brand status colors for this product and are never substituted. Legibility is instead carried by bold weight, large pill size, color redundancy with the adjacent text label (e.g. "Beroperasi" / "Peringatan" / "Gangguan"), and consistent placement — not by raw text contrast alone.
