# Codebase Review: MAD Accuracy Evaluation

## Date
2026-04-28

## Script
`orig/MktS_2025/evaluation/mad_accuracy_evaluation.py`

---

## 1. Command-Line Arguments

The script supports three execution modes:

### Mode A: Config-file based (primary mode for replication)
```
python mad_accuracy_evaluation.py --config <path/to/evaluation_config.yaml>
```
Optional flags:
- `--output-excel-filename` (default: `mad_accuracy_summary.xlsx`)
- `--output-plot-filename` (default: `accuracy_dist.png`)
- `--plot-title` (default: `"Task-Level Accuracy"`)
- `--verbose` — prints CSV dir, output dir, and model name

The YAML config is expected to have:
```yaml
trial_dir: "<path to model directory>"
model_name: "<label string>"
evaluation:
  output_dir: "${trial_dir}/accuracy_evaluation"
  mad_plot_title: "<figure title>"
```

### Mode B: CLI flags
```
python mad_accuracy_evaluation.py --csv-dir <dir> --output-dir <dir>
```

### Mode C: Legacy positional arguments
```
python mad_accuracy_evaluation.py <csv_dir> <output_excel> <output_fig> [--title <title>]
```

---

## 2. How MAD Score Is Calculated

The **Mean Absolute Deviation (MAD)** accuracy metric is computed as follows:

### Data Inputs
Three CSV files from `<trial_dir>/csv_comparison/csv_formatted/`:
- `responses_wave1_3_formatted.csv` — **ground truth** (survey responses from Waves 1–3)
- `responses_wave4_formatted.csv` — **test-retest benchmark** (same humans, Wave 4)
- `responses_llm_imputed_formatted.csv` — **LLM digital twin predictions**

Each CSV has a `twin_id` column (respondent identifier) and numeric survey-response columns.
Row index 1 (description row) is skipped on load.

### Pre-processing
1. All column names are uppercased.
2. `WAVE` column is dropped.
3. All values are coerced to numeric.
4. Only respondents present in all three files (`common_ids`) are kept.
5. Anchoring columns (Q164, Q166, Q168, Q170) are **decile-normalized**: raw values are
   replaced with their decile rank (1–10) relative to the Wave 1–3 distribution.

### Column Filtering
Only columns with known min/max ranges (defined in `get_default_column_ranges()`) are used.
These cover ~140+ survey items grouped into 13 behavioral/cognitive tasks:
false consensus, base rate, framing problem, conjunction problem, outcome bias,
anchoring and adjustment, less is more, sunk cost fallacy, absolute vs. relative savings,
WTA/WTP-Thaler, Allais, myside, prob matching vs. max, non-separability, omission,
denominator neglect, pricing.

### Normalized Difference
For each respondent × column:
```
norm_diff = |prediction - ground_truth| / range
```
where `range = max - min` for that column.

**Accuracy** for a single observation = `1 - norm_diff`  
(1.0 = perfect match, 0.0 = maximally wrong)

### Random Baseline
A random baseline is drawn once per respondent × column:
```python
random_baseline[col] = np.random.randint(int(min), int(max) + 1, size=N)
```

### Aggregation Levels
**Column-level MAD** (`compute_column_mad`):
- Per-column mean accuracy and 95% CI across respondents.

**Task-level MAD** (`compute_task_mad`):
- Columns are grouped by task; mean accuracy computed across all respondents × all columns
  in the task.

**Task-level summary** (primary reported metric):
- For each respondent, compute their average task-level MAD across all tasks they participated in.
- Report mean ± SE and 95% CI across all respondents.
- This is done for three comparisons: `wave4 vs. wave1_3` (test-retest), `llm vs. wave1_3`
  (digital twin), `random_baseline vs wave1_3`.

---

## 3. Outputs

### Excel file (`mad_accuracy_summary.xlsx`)
Three sheets:
1. **Accuracy Summary - task level** — headline numbers (mean accuracy, SE, CI, N respondents)
   for each of the three comparisons.
2. **Accuracy - task level** — per-task breakdown with all three comparisons side-by-side.
3. **Accuracy - column level** — per-question-column breakdown.

### Figure (`accuracy_dist.png`)
Horizontal bar chart sorted by `llm accuracy / wave4 accuracy` ratio, showing per-task
accuracy for test-retest, digital twin, and random baseline, with dashed average lines.

Both outputs are written to `<trial_dir>/accuracy_evaluation/` by default.

---

## 4. Other Scripts in `evaluation/`

| Script | Purpose |
|--------|---------|
| `within_between_subjects.py` | Within- vs. between-subjects accuracy analysis |
| `pricing_analysis.py` | Pricing question-specific analysis |
| `json2csv.py` | Converts raw JSON simulation outputs to the formatted CSV structure |
| `evaluation_basic.yaml` | Basic config template |
| `column_mapping.csv` | Maps column names to human-readable labels |

---

## 5. Pipeline Entry Points

`scripts/evaluate_all_replication_models.sh` — iterates over all model config YAMLs in
`Marketing-Science-Submission-Simulation-Replication-Files/` and calls the evaluation script
for each, producing Excel + PNG outputs in each model's `accuracy_evaluation/` folder.
