# Task 1 Brief: Status Marker Legend in index.md

## What you are doing

You are editing ONE file: `C:/Claude/Pervasive/index.md`

This is a Markdown-only documentation task — no code, no tests, no tooling.

## Global Constraints (apply to every edit)

- Language: Indonesian (English technical terms OK)
- Do NOT remove any confirmed content — only add metadata and markers
- Do NOT add design decisions not from user input or reference docs
- Every `[ASSUMPTION]` or `[DESIGN TBD]` marker must include what input is needed to resolve it
- Git binary: `"C:/Program Files/Git/cmd/git.exe"` (use this full path — bare `git` is NOT in PATH)

## Steps to execute (verbatim)

### Step 1: Insert PRD metadata + status marker legend

Read `C:/Claude/Pervasive/index.md` first.

Then insert the following block IMMEDIATELY AFTER the `# Index — Application Monitoring Peralatan Industri` heading (before the `## Deskripsi Produk` line):

```
**PRD Version:** 0.2 — Prototype Draft
**Last Updated:** 2026-09-16
**Status:** In Progress — Design not yet received

---

## Status Marker Legend

Every section in this PRD set uses one of four markers:

| Marker | Meaning |
|---|---|
| `[CONFIRMED]` | Explicitly decided by user (Henry) in session |
| `[REF]` | Derived from reference docs (UI_stitch / UI_stitch_Gemini) — needs user validation before design handoff |
| `[ASSUMPTION]` | Claude's best-guess fill-in — NOT confirmed, must be validated or replaced before design starts |
| `[DESIGN TBD]` | Intentionally left blank — requires actual design input (Figma / mockup) before this field can be filled |

**Rule:** Any field marked `[ASSUMPTION]` or `[DESIGN TBD]` in UI_PRD.md is NOT safe to implement until the designer or user provides the real value.

---

```

### Step 2: Tag each line in the "Ringkasan Design System" section

Find the `## Ringkasan Design System` section. Replace it with this exact tagged version:

```markdown
## Ringkasan Design System

- **Layout:** Responsive — desktop 1280px+ / tablet 768–1279px / mobile <768px `[ASSUMPTION]` D-024
- **Grid:** 12 kolom, margin 16 px, gutter 16 px `[REF]` D-030
- **Spacing:** 8-point grid (8, 16, 24, 32 px) `[REF]` D-030
- **Font:** Plus Jakarta Sans `[CONFIRMED]` D-020
- **Light theme:** Background `#F4F7FE` · Surface `#FFFFFF` · Primary `#4318FF` · Heading `#2B3674` · Body `#A3AED0` `[REF]` D-021
- **Dark theme:** Background `#0F172A` · Surface `#1E293B` · Primary `#818CF8` · Heading `#E2E8F0` · Body `#94A3B8` `[ASSUMPTION]` D-023
- **Status:** Normal `#22C55E` · Peringatan `#F59E0B` · Gangguan `#EF4444` `[REF]` D-022
```

### Step 3: Commit

```
"C:/Program Files/Git/cmd/git.exe" -C "C:/Claude/Pervasive" add index.md
"C:/Program Files/Git/cmd/git.exe" -C "C:/Claude/Pervasive" commit -m "prd: add status marker legend and metadata to index.md"
```

## Report

Write your report to: `C:/Claude/Pervasive/.superpowers/sdd/2026-09-16-prd-professionalisation/task-1-report.md`

Report must contain:
- Status: DONE / DONE_WITH_CONCERNS / NEEDS_CONTEXT / BLOCKED
- Commit hash
- Any concerns

Return to me: status, commit hash, one-line summary.

Do NOT dispatch any subagents.
