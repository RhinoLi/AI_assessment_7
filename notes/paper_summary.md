# Paper Summary: Twin-2K-500

## Citation
Toubia, O., Gui, G. Z., Peng, T., Merlau, D. J., Li, A., & Chen, H. (2025). Database Report: Twin-2K-500: A Data Set for Building Digital Twins of over 2,000 People Based on Their Answers to over 500 Questions. *Marketing Science*, 44(6), 1446–1455. https://doi.org/10.1287/mksc.2025.0262

---

## Task 1.1: Core Concepts

### 1. Research Question

The central question is: **Can LLM-based digital twins accurately replicate the behavior of real individuals at both the individual and aggregate levels?**

More specifically: Given a rich, individual-level profile derived from survey responses (personality, cognitive ability, economic preferences, demographics), can an LLM simulate that individual's answers to holdout behavioral-economics questions—questions the LLM has never seen—as accurately as the person themselves would reproduce their own answers two weeks later?

A secondary question is which types of behavior (normative vs. nonnormative, factual vs. opinion-based) are more or less replicable by digital twins.

### 2. Methodology / Identification Strategy

**Holdout Design:**
The 500+ survey questions are split into training and holdout sets. Waves 1–3 contain 500 questions total; the **heuristics-and-biases battery** (88 questions across 17 tasks) is withheld from persona construction and used purely for evaluation. The persona is built from all non-holdout content in Waves 1–3.

**Test-Retest Accuracy Benchmark:**
Wave 4, administered ~2 weeks after Wave 3, repeats the exact same 88 holdout questions under the same experimental conditions. This gives an empirical ceiling for prediction accuracy: if humans achieve X% test-retest accuracy, a digital twin achieving X% would be perfect by this standard.

**Accuracy Metric (MAD-based):**
For each holdout question:
- *Binary questions:* accuracy = 1 if answers match, 0 otherwise.
- *Numerical questions:* `accuracy = 1 − |prediction − ground_truth| / range`
- Anchoring questions (unbounded) are decile-normalized before deviation is computed.

Within each task, question-level accuracies are averaged. Each respondent then receives one task-level accuracy score per task. The grand mean and SE across respondents are the reported headline numbers.

**Three-Way Comparison:**
Every evaluation contrasts three predictors against the Wave 1–3 ground truth:
1. **Wave 4 (test-retest)** — human self-replication benchmark (~81.72% average)
2. **LLM digital twin** — model prediction (~71.72% average)
3. **Random baseline** — uniform random draw within each question's range (~59.17%)

**Aggregate-Level Evaluation:**
Beyond individual accuracy, the paper also tests whether LLM-simulated responses replicate the *average treatment effects* from 11 between-subject and 5 within-subject behavioral economics experiments (Table 3).

### 3. Data Sources: The Twin-2K-500 Dataset

| Attribute | Value |
|-----------|-------|
| Final N | 2,058 participants (completed all 4 waves) |
| Recruitment | Prolific; representative U.S. sample (age, sex, ethnicity) |
| Total questions | 500+ across Waves 1–3; 88 repeated in Wave 4 |
| Avg. total time | ~145 minutes per participant |
| Wave 1 | Demographics (14 Q), personality (Big 5, Need for Cognition, etc.), cognitive tests, economic preferences |
| Wave 2 | Additional personality, cognitive, economic preference measures |
| Wave 3 | More personality measures, pricing study (40 products) |
| Wave 4 | Repeat of all 88 holdout heuristics-and-biases questions + pricing study |

**Holdout tasks (88 questions, 17 tasks):**
- 11 between-subject experiments: base rate, outcome bias, sunk cost, Allais, framing, conjunction (Linda), anchoring, absolute vs. relative savings, myside bias, less is more, WTA/WTP-Thaler
- 5 within-subject experiments: false consensus, nonseparability, omission bias, probability matching, dominator neglect
- 1 pricing study (40 binary choices)

### 4. Core Findings (Section 5)

**Individual Level (Table 2 / Figure 2):**
- Average LLM digital twin accuracy across 17 tasks: **71.72%** (for text-persona GPT4.1-mini)
- Average test-retest accuracy: **81.72%**
- Ratio (digital twin / test-retest): **~87.67%** — the "relative accuracy" headline figure
- Results are broadly consistent across 12 model variants (range: 67.88%–71.92% LLM accuracy)
- Random baseline: **59.17%**

**Aggregate Level (Table 3):**
- Between-subject experiments: **5 of 10 replicated** effects are also replicated by digital twins (framing, conjunction, absolute vs. relative savings, myside bias, WTA/WTP-Thaler; plus one of two anchoring questions)
- Failures occur where twins: (a) "know" the correct answer (anchoring: African countries in UN), (b) behave more normatively than humans (outcome bias, sunk cost, Allais, Less is More), or (c) differ in political/medical domain opinions
- Within-subject experiments: **2 of 5 replicated** (false consensus and dominator neglect)
- Notable failures: omission bias (only 4% of twins refused vaccine vs. ~45% of humans), probability matching (twins always chose normative option vs. ~30% humans), nonseparability (only 1 of 4 items)

**Pricing Study:**
- Demand curves from twins are broadly downward-sloping but show artifacts at free products, consistent with Gui and Toubia (2023).

---

## Task 1.2: Mapping Paper Concepts to Replication Files

### Key Variables → CSV Files

| Paper Concept | CSV File | Role |
|---------------|----------|------|
| Ground truth (Wave 1–3 holdout answers) | `responses_wave1_3_formatted.csv` | Reference against which all predictions are scored |
| Test-retest benchmark (Wave 4 answers) | `responses_wave4_formatted.csv` | Human self-replication ceiling |
| LLM digital twin predictions | `responses_llm_imputed_formatted.csv` | Model output to be evaluated |

All three CSVs reside in `<model_dir>/csv_comparison/csv_formatted/` for each of the 12 model configurations in `Marketing-Science-Submission-Simulation-Replication-Files/`.

Each CSV shares a `twin_id` column identifying respondents; only respondents present in all three files (`common_ids`) are used in evaluation.

### Main Specifications → Evaluation Scripts

**`evaluation/mad_accuracy_evaluation.py` → Table 2 / Figure 2 (Individual-Level MAD):**
1. Loads all three CSVs; restricts to `common_ids`.
2. Drops `WAVE` column; uppercases column names; coerces to numeric.
3. Decile-normalizes anchoring columns (Q164, Q166, Q168, Q170) relative to Wave 1–3 distribution.
4. Filters to ~140 columns with known `[min, max]` ranges (defined in `get_default_column_ranges()`), covering all 17 holdout tasks.
5. Per respondent × column: `norm_diff = |prediction − truth| / range`; `accuracy = 1 − norm_diff`.
6. Columns are grouped by task; task-level accuracy = mean across all questions in the task.
7. Per respondent: mean task accuracy across all tasks they participated in.
8. Reports mean ± SE and 95% CI for three comparisons: wave4 vs. wave1_3, llm vs. wave1_3, random vs. wave1_3.
9. Outputs: `mad_accuracy_summary.xlsx` (3 sheets) + `accuracy_dist.png` bar chart.

**`evaluation/within_between_subjects.py` → Table 3 (Aggregate-Level Heuristics & Biases):**
- Loads the four wave CSVs from `data/wave_csv/wave_N_labels_anonymized.csv` plus the LLM label-formatted CSV (`csv_formatted_label/responses_llm_imputed_label_formatted.csv`).
- For each between-subject experiment: runs t-tests or chi-square tests comparing condition means/proportions across conditions, for humans (waves 1–3 and wave 4 separately) and LLM twins.
- For each within-subject experiment: runs within-person statistical tests (e.g., Pearson correlation for nonseparability, binomial tests for false consensus, proportion tests for omission bias and probability matching).
- Uses `PanelOLS` for panel-level regressions where appropriate.
- Outputs: a multi-sheet Excel workbook summarizing which effects are replicated/not replicated for each source.

**`text_simulation/` (LLM Simulation Pipeline, not `ml_prediction/`):**
- Note: The INSTRUCTIONS reference `ml_prediction/` but the actual repo directory is `text_simulation/`. It contains the scripts to run LLM simulations (`run_LLM_simulations.py`, `postprocess_responses.py`, etc.) that *produced* the pre-computed CSVs in `Marketing-Science-Submission-Simulation-Replication-Files/`. The XGBoost ML baseline is referenced in paper footnote 6 as part of the Online Appendix but does not appear to have a dedicated directory in the published replication package.
