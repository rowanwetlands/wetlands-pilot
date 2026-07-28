# wetlands-pilot — System Overview
Canonical reference. Update this file (not just chat history) whenever infrastructure or scope decisions change. Intended for both the repo and upload into any Claude Project supporting this work.

---

## Project scope
Book section (1 of 4 wetland case studies + 2 methodological sections) modelling speculative ecological/landscape futures at Montrose Basin, Scotland, using a Forensic Architecture-derived methodology (ground truth, cartographic regression, remote sensing, fluid dynamics/simulation, situated testimony, 3D modelling — repurposed future-facing rather than past-facing, framed through belief/uncertainty rather than single deterministic prediction). Digital supplement accompanies the printed book.

**Current phase: Phase 1 — Ground truth + regression only.**
No foundation models (TESSERA/AlphaEarth), no hydrodynamics, no ML training, no agent layer until Phase 1's evidence package is complete and versioned. This boundary has been restated multiple times and should not drift.

## Standing principle
Absence/uncertainty is a first-class category, not a gap to silently interpolate over. Data gaps get recorded and labelled (e.g. `evidence status: structural gap`), not smoothed away for a cleaner-looking output.

---

## Key decisions made (Phase 1)
- Terrain output is an **authoritative raster package** (elevation + uncertainty + source-date + source-ID + gap-mask bands), not a mesh — mesh is a derived visualisation product only.
- Vertical/horizontal reference: **EPSG:7405** (OSGB36 / British National Grid + ODN height), compound CRS, not tracked separately.
- **Tidal-frame elevation zones** (position in tidal frame) and **hydroperiod proxy** (actual inundation frequency, accounting for connectivity/barriers/lag) are kept as two distinct layers, not conflated.
- **Dynamic Coast excluded as a basin-interior source** — its own Montrose report states it covers the open coast/Links only, not the Montrose Basin coast. Valid only for open-coast/estuary-mouth boundary conditions.
- Bathymetry source order: Montrose Port Authority first, then SEPA, Angus Council, Marine Directorate, UKHO, field survey last.
- Local saltmarsh accretion rate: **not confirmed for Montrose** (UKCEH's 2023-24 rSET-MH network doesn't name Montrose among its sites) — treat as open/structural gap, do not substitute another site's rate without labelling it an external analogue.
- Historic edge/channel data kept as **separate feature families** (cartographic tidal line / vegetation edge / saltmarsh edge / channel geometry / seagrass extent) — not merged into one line. Rate calculated via **weighted regression across all available epochs**, not two-point endpoint calculation.

## Data governance rule
Three-tier separation:
1. **External source** (national archives — SRSP, Sentinel, NLS, etc.) — referenced by URL + checksum, not duplicated wholesale
2. **Raw project archive** — exact received/downloaded files, stored in R2 and mirrored to B2
3. **DVC-tracked derived data** — cleaned, cropped, interpreted, model-ready datasets only

---

## Infrastructure — current state

GitHub (github.com/rowanwetlands/wetlands-pilot)
    code, config, docs, DVC pointers, history
        |
        | dvc push/pull
        v
Cloudflare R2
    wetlands-dvc-rowan/dvc/   -- DVC-managed cache (active remote)
    wetlands-raw-rowan/        -- raw archive
        |
        | rclone (manual, milestone-based)
        v
Backblaze B2
    wetlands-archive-raw       -- independent backup, separate credentials from R2

**Tested and confirmed working (checksummed restore, not just upload success):**
- Git -> GitHub push/clone
- DVC -> R2 (wetlands-dvc-rowan) push, plus fresh-clone recovery test passed
- B2 backup: upload -> verify -> delete local -> restore -> checksum match, passed

**Not yet done:**
- wetlands-products-rowan bucket (for readable reviewed outputs) -- not yet created
- Old DVC test objects in wetlands-raw-rowan/dvc/ -- not yet cleaned up
- Docker -- deliberately deferred until real data exists to containerize

**Acquired datasets (Phase 1):**
- SRSP LiDAR Phase 1 DTM -- acquired, verified R2+B2, band C (2026-07-28)
- SRSP LiDAR Phase 2 DTM -- acquired, verified R2+B2, band C (2026-07-28)

**Local environment:** Linux Mint 22.2, x86_64, Python 3.12.3, project venv at ~/Documents/wetlands-pilot/.venv, DVC 3.67.1, credentials for R2 stored in local AWS profile r2-dvc (outside git), B2 credentials via dedicated rclone remote b2-archive:.

---

## Immediate next steps
1. BODC tide gauge -- unblocked, foundational for tidal frame
2. NLS historic maps -- needed for cartographic regression, server issue unresolved
3. Resolve untracked files in repo (boundary/derived, data/, metadata/, qgis/) -- add to .gitignore or track deliberately
4. Clean up old DVC test objects in wetlands-raw-rowan/dvc/
5. Create wetlands-products-rowan bucket
6. Only after more datasets through the chain: design the core Docker container

---

*Last updated: 2026-07-28 -- LiDAR Phase 1+2 acquired. Update this file directly rather than letting chat history be the source of truth.*
