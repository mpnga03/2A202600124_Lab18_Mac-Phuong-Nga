# Lab Results Summary
## My FullName: Mac Phuong Nga
## Student ID: 2A202600124
Executed on 2026-05-04.

## Environment checks
- `python`: 3.10.11
- `scripts/verify_lite.py`: PASS
- `scripts/generate_data_lite.py` (200,000 rows): PASS

## Notebook evidence (executed from Jupytext `.py`)
1. `notebooks/01_delta_basics.py`
- Delta table created.
- Schema enforcement blocked bad write (`age="thirty"`).
- `schema_mode="merge"` added column `tier`.

2. `notebooks/02_optimize_zorder.py`
- Files before optimize: 200
- Files after optimize+zorder: 55
- Speedup: 8.8x (target >= 3x)
- Files-pruned ratio: 55.0x (target >= 10x)

3. `notebooks/03_time_travel.py`
- MERGE 100K: 0.21s (target < 60s)
- RESTORE to v2: 0.03s (target < 30s)
- `score < 0` rows after restore: 0
- Total versions in history: 5 (target >= 5)

4. `notebooks/04_medallion.py`
- Bronze rows: 200,000
- Silver rows: 190,052 (dedup drop: 9,948)
- Gold distinct dates: 8 (target >= 7)
- Gold distinct models: 3

## Screenshot checklist (to capture manually)
- `_lakehouse/.../_delta_log/*.json` visible
- NB2 metrics block (speedup/files-pruned)
- NB3 final history including RESTORE row
- NB4 Gold metrics block (dates/models)
