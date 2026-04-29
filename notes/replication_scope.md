# Replication Scope

## Goal
Reproduce the key quantitative results of Toubia et al. (2025) using the published replication package in `orig/MktS_2025/`, specifically the pre-computed LLM simulation outputs in `Marketing-Science-Submission-Simulation-Replication-Files/`.

---

## Target 1: Table 2 / Figure 2 — Individual-Level Task Accuracy

**What it is:**
Table 2 reports the overall MAD-based accuracy for each of the 12 persona-simulation approaches. Figure 2 shows per-task accuracy (bar chart) for the primary model (Text Persona - GPT4.1-mini), comparing LLM accuracy, test-retest accuracy, and random baseline across all 17 holdout tasks.

**Key numbers to reproduce:**
- Text Persona GPT4.1-mini: LLM accuracy = **71.72%**, test-retest = **81.72%**, random = **59.17%**
- Ratio (LLM / test-retest) ≈ **87.67%**
- Per-task accuracy bar chart sorted by LLM/test-retest ratio

**How to reproduce:**
Run `evaluation/mad_accuracy_evaluation.py` for each of the 12 model directories using their `evaluation_config.yaml` files, or use the batch script `scripts/evaluate_all_replication_models.sh`. Each run reads the three pre-computed CSVs and writes `mad_accuracy_summary.xlsx` + `accuracy_dist.png` to `<model_dir>/accuracy_evaluation/`.

**Files involved:**
- Script: `orig/MktS_2025/evaluation/mad_accuracy_evaluation.py`
- Batch runner: `orig/MktS_2025/scripts/evaluate_all_replication_models.sh`
- Inputs (per model): `csv_comparison/csv_formatted/responses_{llm_imputed,wave1_3,wave4}_formatted.csv`
- Outputs (per model): `accuracy_evaluation/mad_accuracy_summary.xlsx`, `accuracy_dist.png`

---

## Target 2: Table 3 — Aggregate-Level Replication of Heuristics and Biases

**What it is:**
Table 3 shows whether each of the 16 heuristics-and-biases experiments (11 between-subject + 5 within-subject) is replicated by (a) human data from Waves 1–3, (b) human data from Wave 4, and (c) LLM digital twin simulations. A ✓ or ✗ is reported for each cell.

**Key numbers to reproduce:**
- Between-subject: 10 effects replicated by humans; 5 (or 5.5 with anchoring split) replicated by twins
- Within-subject: 5 effects replicated by humans; 2 replicated by twins
- Notable twin failures: outcome bias, sunk cost, Allais, less is more, omission bias, probability matching

**How to reproduce:**
Run `evaluation/within_between_subjects.py` for each model configuration. This script loads the labeled wave CSVs from `data/wave_csv/` and the LLM label-formatted CSV (`csv_formatted_label/responses_llm_imputed_label_formatted.csv`) from each model directory.

**Files involved:**
- Script: `orig/MktS_2025/evaluation/within_between_subjects.py`
- Inputs (wave data): `orig/MktS_2025/data/wave_csv/wave_{1,2,3,4}_labels_anonymized.csv`
- Inputs (LLM): `<model_dir>/csv_comparison/csv_formatted_label/responses_llm_imputed_label_formatted.csv`
- Outputs: Excel workbook with per-experiment test statistics and replication status

---

## Target 3: ML Baseline (XGBoost / Fine-tuning)

**What it is:**
Paper footnote 6 mentions an XGBoost machine learning baseline and a fine-tuning benchmark in the Online Appendix. These use a portion of the holdout data as a training subsample.

**Scope caveat:**
The published replication package does **not** contain a dedicated `ml_prediction/` directory (the INSTRUCTIONS reference this path, but it does not exist in `orig/MktS_2025/`). The repo contains `text_simulation/` for the LLM simulation pipeline and there is no separate XGBoost pipeline directory. The Online Appendix results may have been run on proprietary infrastructure or were not included in the public replication package.

**Plan:**
- Confirm whether any XGBoost code exists elsewhere in the repo (e.g., inside `text_simulation/` or `scripts/`).
- If no XGBoost code is present, document this gap explicitly and treat the ML baseline as **out of scope for this replication** (the primary replication targets are Targets 1 and 2 above).
- If found, run the pipeline and compare against the LLM accuracy numbers to confirm it serves as a lower-performance non-LLM baseline.

---

## Summary Table

| Target | Paper Location | Script | Status |
|--------|---------------|--------|--------|
| Individual-level MAD accuracy | Table 2, Figure 2 | `evaluation/mad_accuracy_evaluation.py` | **In scope — primary target** |
| Aggregate heuristics replication | Table 3 | `evaluation/within_between_subjects.py` | **In scope — primary target** |
| XGBoost ML baseline | Online Appendix | Not found in repo | **Investigate; likely out of scope** |

---

## Evaluation Environment

- Python: 3.12.3 via Poetry virtual env at `/home/rhino/.cache/pypoetry/virtualenvs/digital-twin-simulation-EDJg5I4g-py3.12`
- Run prefix: `/home/rhino/.local/bin/poetry -C /home/rhino/projects/ai_assessment_7/orig/MktS_2025 run python`
- Working directory for scripts: `orig/MktS_2025/`
