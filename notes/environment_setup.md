# Environment Setup Notes

## Date
2026-04-28

## Python Version
Python 3.12.3 (system) — `/usr/bin/python3`

## Poetry Installation
Poetry was not pre-installed. Installed via official installer:
```
curl -sSL https://install.python-poetry.org | python3 -
```
Installed Poetry 2.3.4 at `/home/rhino/.local/bin/poetry`.

## Poetry Install Result
Command: `poetry install` (run from `orig/MktS_2025/`)

**Status: Mostly successful — 199 packages installed.**

Virtual environment created at:
`/home/rhino/.cache/pypoetry/virtualenvs/digital-twin-simulation-EDJg5I4g-py3.12`

### Warning / Error
At the very end of installation, Poetry attempted to write a `poetry.lock` file into the
source directory (`orig/MktS_2025/`) but was denied:

```
[Errno 13] Permission denied: '/home/rhino/projects/ai_assessment_7/orig/MktS_2025/poetry.lock'
```

**Impact**: Negligible. The `poetry.lock` file tracks pinned versions for reproducibility, but
all 199 packages were already resolved and installed before this write was attempted. The
virtual environment is fully functional.

**Note**: `pyproject.toml` requires `python = "^3.11.7"`. System Python is 3.12.3, which
satisfies this constraint.

## Core Package Verification
All core packages verified in the virtual environment:

| Package     | Version  | Status |
|-------------|----------|--------|
| pandas      | 2.3.3    | ✓      |
| numpy       | 1.26.4   | ✓      |
| xgboost     | 2.1.4    | ✓      |
| scipy       | 1.17.1   | ✓      |
| matplotlib  | 3.10.9   | ✓      |
| openpyxl    | 3.1.5    | ✓      |
| pyyaml      | 6.0.3    | ✓      |
| scikit-learn| 1.8.0    | ✓      |

## Missing from Expected Structure
The `pyproject.toml` does **not** include a `poetry.lock` in the repo (and the `orig/MktS_2025/`
directory lacks `ml_prediction/` as specified in the INSTRUCTIONS template). The repo contains
`text_simulation/` instead. This is consistent with the replication package as published.

## How to Invoke Python
```bash
/home/rhino/.cache/pypoetry/virtualenvs/digital-twin-simulation-EDJg5I4g-py3.12/bin/python
```
Or via Poetry:
```bash
/home/rhino/.local/bin/poetry -C /home/rhino/projects/ai_assessment_7/orig/MktS_2025 run python
```
