# Task 5 Brief: Final Consistency Check + Push

## What you are doing

Final consistency verification across all PRD files, then update `index.md` Catatan section, then push.

Files to CHECK (read-only verification, then one targeted edit):
- `C:/Claude/Pervasive/index.md`
- `C:/Claude/Pervasive/UI_PRD.md`
- `C:/Claude/Pervasive/Development.md`
- `C:/Claude/Pervasive/DECISIONS.md`

File to EDIT:
- `C:/Claude/Pervasive/index.md` (Catatan Lintas-Domain section only)

## Global Constraints

- Git binary: `"C:/Program Files/Git/cmd/git.exe"` (use full path)
- Language: Indonesian (English technical terms OK)

## Steps to execute

### Step 1: Verify DECISIONS.md cross-references

Read `C:/Claude/Pervasive/UI_PRD.md`. For every D-ID mentioned (D-020 through D-030), confirm the ID exists as a row in `C:/Claude/Pervasive/DECISIONS.md`. List any D-ID used in UI_PRD.md that is missing from DECISIONS.md.

Read `C:/Claude/Pervasive/Development.md`. For every D-ID mentioned (D-001 through D-008, D-006, P-002), confirm presence in DECISIONS.md.

If any D-ID is missing from DECISIONS.md, add it before continuing.

### Step 2: Verify no [ASSUMPTION] without D-ID in any PRD file

Scan UI_PRD.md and Development.md for any line containing `[ASSUMPTION]` that does NOT also contain a D-ID (pattern: D-0 followed by digits). List any violations.

If violations found, add the missing D-ID. If the assumption doesn't correspond to any existing D-ID, use the closest matching one or note it.

### Step 3: Update Catatan Lintas-Domain in index.md

Read `C:/Claude/Pervasive/index.md`. Find the `## Catatan Lintas-Domain` section at the bottom.

Replace the current content of that section with:

```markdown
## Catatan Lintas-Domain

- Semua keputusan dan sumbernya → [DECISIONS.md](./DECISIONS.md)
- Item bertanda `[ASSUMPTION]` TIDAK boleh diimplementasikan sebelum dikonfirmasi user/designer
- Item bertanda `[DESIGN TBD]` menunggu Figma design file — lihat P-004 di DECISIONS.md
- Nilai threshold per parameter masih nullable — lihat P-002 di DECISIONS.md
- Template PDF laporan (S-05) belum di-lock — lihat P-001 di DECISIONS.md
- Data berjalan lokal (SQLite). Tidak ada koneksi ke server eksternal, SCADA, atau ERP.
```

### Step 4: Final commit + push

```
"C:/Program Files/Git/cmd/git.exe" -C "C:/Claude/Pervasive" add index.md
"C:/Program Files/Git/cmd/git.exe" -C "C:/Claude/Pervasive" commit -m "prd: final consistency pass — all assumptions marked, DECISIONS.md cross-referenced"
"C:/Program Files/Git/cmd/git.exe" -C "C:/Claude/Pervasive" push origin main
```

## Report

Write your report to: `C:/Claude/Pervasive/.superpowers/sdd/2026-09-16-prd-professionalisation/task-5-report.md`

Report must contain:
- Status: DONE / DONE_WITH_CONCERNS / NEEDS_CONTEXT / BLOCKED
- Commit hash
- Results of Step 1 verification (any missing D-IDs?)
- Results of Step 2 verification (any [ASSUMPTION] without D-ID?)
- Confirmation push succeeded

Return to me: status, commit hash, verification results summary. Do NOT dispatch subagents.
