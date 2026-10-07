# Task 4 Brief: Tag Development.md with Decision IDs

## What you are doing

You are editing ONE file: `C:/Claude/Pervasive/Development.md`

This is a Markdown-only documentation task — no code, no tests.

## Context from earlier tasks

- Task 2 created DECISIONS.md with D-IDs (D-001 through D-030 with intentional gaps)
- Tech stack decisions confirmed: D-001 (React), D-002 (Tailwind), D-003 (Zustand), D-004 (Recharts), D-005 (Express.js), D-006 (SQLite), D-007 (JWT), D-008 (Polling 10s)

## Global Constraints

- Language: Indonesian (English technical terms OK)
- Do NOT remove any confirmed content — only add markers and metadata
- Do NOT add new design decisions
- Git binary: `"C:/Program Files/Git/cmd/git.exe"` (use full path — bare `git` is NOT in PATH)

## Steps to execute

### Step 1: Add document metadata block

Read `C:/Claude/Pervasive/Development.md` first.

Replace the current heading block (first 3 lines of the file) with:

```markdown
# Development — Application Monitoring Peralatan Industri

**Status:** DRAFT — Tech stack confirmed, implementation not started
**Dependencies:** UI_PRD.md visual specs must be finalized before frontend styling begins
```

(The existing `Dokumen ini ditujukan untuk **Developer**...` paragraph stays immediately after.)

### Step 2: Add Source column to the tech stack table (Section 1)

The current tech stack table has columns: Layer | Pilihan | Penjelasan Singkat

Replace it with a 4-column version adding "D-ID" as the last column:

```markdown
| Layer | Pilihan | Penjelasan Singkat | D-ID |
|---|---|---|---|
| Frontend | **React JS** | Library UI berbasis komponen, cocok untuk SPA | `[CONFIRMED]` D-001 |
| Styling | **Tailwind CSS** | Utility-first CSS, tulis class langsung di JSX, cepat untuk prototype | `[CONFIRMED]` D-002 |
| State Management | **Zustand** | "Kotak penyimpanan global" untuk React — simpan data mesin, alarm, user di satu tempat dan bisa diakses dari halaman manapun. Lebih simple dari Redux, API minimal | `[CONFIRMED]` D-003 |
| Charting | **Recharts** | Library chart dibangun khusus untuk React. Lebih idiomatis dari Chart.js (yang dibangun untuk vanilla JS) | `[CONFIRMED]` D-004 |
| Backend | **Express.js** | Node.js server minimalis. Cukup beberapa endpoint REST API untuk prototype | `[CONFIRMED]` D-005 |
| Database | **SQLite** (via `better-sqlite3`) | File database lokal, zero setup, tidak perlu install server database | `[CONFIRMED]` D-006 |
| Auth | **JWT** (JSON Web Token) | Token autentikasi stateless — server tidak perlu ingat siapa yang login. Token disimpan di browser, cocok untuk React SPA | `[CONFIRMED]` D-007 |
```

### Step 3: Tag the real-time data section (Section 6)

Add a source reference to the polling decision. Find the line:
```
**Polling 10 detik (dipilih untuk prototype):**
```
Change it to:
```
**Polling 10 detik (dipilih untuk prototype):** `[CONFIRMED]` D-008
```

### Step 4: Tag nullable threshold fields in Section 3.2

Find the two comment lines in the Parameter data model:
```
  thresholdWarning: number | null   // nullable — sensor belum ditest
  thresholdFault: number | null     // nullable — sensor belum ditest
```
Change them to:
```
  thresholdWarning: number | null   // [CONFIRMED] nullable — D-006 scope (prototype), P-002 (threshold values pending sensor test)
  thresholdFault: number | null     // [CONFIRMED] nullable — D-006 scope (prototype), P-002 (threshold values pending sensor test)
```

### Step 5: Commit

```
"C:/Program Files/Git/cmd/git.exe" -C "C:/Claude/Pervasive" add Development.md
"C:/Program Files/Git/cmd/git.exe" -C "C:/Claude/Pervasive" commit -m "prd: add source tags and decision IDs to Development.md"
```

## Report

Write your report to: `C:/Claude/Pervasive/.superpowers/sdd/2026-09-16-prd-professionalisation/task-4-report.md`

Report must contain:
- Status: DONE / DONE_WITH_CONCERNS / NEEDS_CONTEXT / BLOCKED
- Commit hash
- Any concerns

Return to me: status, commit hash, one-line summary. Do NOT dispatch subagents.
