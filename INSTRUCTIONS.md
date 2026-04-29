# AI-Generated Academic Paper: Replicating "Database Report: Twin-2K-500: A Data Set for Building Digital Twins of over 2,000 People Based on Their Answers to over 500 Questions"

## Project Overview

You are tasked with producing a complete academic paper by replicating Toubia et al. (2025), published in Marketing Science.

**Your task**: 
1. Replicate the original findings using the authors' published replication data and code


**Original paper**: orig/MktS_2025_Database Report Twin-2K-500 A Data Set for Building Digital Twins of over 2,000 People.pdf
**Original replication materials**: orig/MktS_2025/

---

## IMPORTANT: Stop-and-Check Points

Throughout this project, there are mandatory **STOP AND CHECK** points marked with 🛑. At each of these points, you must:
1. Summarize what you have completed
2. Present key outputs for review
3. List any issues or concerns
4. **Wait for human approval before proceeding**

Do not proceed past a 🛑 checkpoint without explicit approval.

---

## PHASE 0: Environment Setup and Asset Verification

### Task 0.1: Verify Project Structure
Since the replication package and dataset have already been downloaded, verify that the current working directory contains the following core structure:

```text
orig/MktS_2025/
├── data/                                         # Base data files
├── evaluation/                                   # Evaluation scripts (MAD accuracy, within/between subjects)
├── scripts/                                      # Pipeline scripts (e.g., evaluate_all_replication_models.sh)
├── ml_prediction/                                # XGBoost prediction pipeline
├── Marketing-Science-Submission-Simulation-Replication-Files/ # Pre-computed LLM simulation outputs
├── pyproject.toml                                # Poetry dependency definitions
└── poetry.lock                                   # Locked dependencies
```
Create a `notes/` directory if it does not already exist to store your research and execution documentation.

### Task 0.2: Initialize the Python Environment
This project relies on Poetry for dependency management. 
1. Run `poetry install` to initialize the environment and install all necessary dependencies.
2. Verify that core packages (`pandas`, `numpy`, `xgboost`) are successfully installed in the isolated environment.
3. Document any warnings or dependency conflicts in `notes/environment_setup.md`.

### Task 0.3: Inventory the Pre-Computed Simulation Data
Navigate into the `Marketing-Science-Submission-Simulation-Replication-Files/` directory. 
1. List the available model configurations (e.g., `Text Persona - GPT4.1-mini`).
2. Drill down into one of these model directories and verify the existence of the three critical CSV files required for the Mean Absolute Deviation (MAD) evaluation:
   * `responses_llm_imputed_formatted.csv`
   * `responses_wave1_3_formatted.csv`
   * `responses_wave4_formatted.csv`
3. Log the paths and file sizes of these core CSVs in `notes/data_inventory.md` to confirm the data is intact and ready for evaluation.

### Task 0.4: Examine the Evaluation Codebase
Unlike a Stata-to-Python translation project, this codebase is completely Python-native.
Carefully review the main evaluation script (`evaluation/mad_accuracy_evaluation.py`) and document:
1. What command-line arguments it accepts (e.g., the `--config` flag).
2. How it calculates the Mean Absolute Deviation (MAD) score.
3. Where it outputs the final evaluation metrics.
Save this summary in `notes/codebase_review.md`.

---

## 🛑 CHECKPOINT 0: Project Setup and Verification Complete

**Before proceeding, confirm:**
- [ ] Directory structure verified and `notes/` folder created.
- [ ] Python environment successfully initialized via Poetry.
- [ ] Pre-computed simulation data inventoried and critical CSVs located.
- [ ] Native Python evaluation codebase reviewed and understood.

**Present for review:**
1. Contents of `notes/data_inventory.md` proving the required CSVs are present.
2. Contents of `notes/codebase_review.md` summarizing how the MAD evaluation script works.
3. Any dependency errors or environment issues encountered during setup.

**STOP and wait for human approval before proceeding to Phase 1.**


---

## PHASE 1: Paper Understanding and Literature Verification

### Task 1.1: Extract Core Concepts from the Original Paper
Read the provided PDF (`orig/MktS_2025_Database Report Twin-2K-500 A Data Set for Building Digital Twins of over 2,000 People.pdf`). Create a document named `notes/paper_summary.md` and extract the following elements explicitly:

1. **Research Question:** What is the primary hypothesis or question regarding LLM-based digital twins?
2. **Methodology / Identification Strategy:** How do the authors measure the "accuracy" of the digital twins? Explain the use of the "holdout questions" and the "test-retest accuracy benchmark" (comparing Wave 1-3 data, Wave 4 data, and LLM generated data).
3. **Data Sources:** Summarize the "Twin-2K-500" dataset (e.g., $N=2,058$, 500+ questions, 4 waves).
4. **Core Findings:** Summarize the main results from Section 5 (e.g., individual-level relative accuracy of ~88%, and the aggregate-level successes and failures in replicating behavioral economics heuristics).

### Task 1.2: Map Key Variables and Specifications to the Replication Files
Now, connect the theoretical paper to the actual pre-computed files you inventoried in Phase 0. Add a section to `notes/paper_summary.md` detailing:
1. **Key Variables:** How do the paper's concepts map to the data files? (e.g., Ground Truth = `responses_wave1_3_formatted.csv`, Test-Retest Benchmark = `responses_wave4_formatted.csv`, Twin Prediction = `responses_llm_imputed_formatted.csv`).
2. **Main Specifications:** Review the `evaluation/mad_accuracy_evaluation.py` and `evaluation/within_between_subjects.py` scripts. Briefly explain how these scripts calculate the Mean Absolute Deviation (MAD) and compare the between/within-subject effects described in the paper.

### Task 1.3: Literature Review and Verification (Anti-Hallucination)
Search for and summarize the relevant foundational literature cited in the PDF. **CRITICAL: For each paper you cite, you must independently verify that it exists via web search or cross-referencing.** Do not hallucinate publication details. 

Create a file named `notes/literature_verification.md` with a summary table containing at least the following highly relevant papers mentioned in Toubia et al. (2025):
* Park et al. (2024) - *Generative agent simulations of 1,000 people*
* Gui and Toubia (2023) - *The challenge of using LLMs to simulate human behavior*
* Stanovich and West (2008) - *On the relative independence of thinking biases and cognitive ability*
* Kahneman and Tversky (1973) - *On the psychology of prediction*

| Authors | Year | Title | Key Finding Relevant to Digital Twins/Heuristics | Verified Exists? |
|---------|------|-------|--------------------------------------------------|------------------|
| ... | ... | ... | ... | Yes/No |

### Task 1.4: Define the Exact Replication Scope
Based on your reading of the paper and the available codebase, define exactly what you will be replicating in the upcoming phases. Create `notes/replication_scope.md` outlining the goal to reproduce:
1. **Table 2 / Figure 2:** The individual-level task accuracy using the evaluation script on the pre-computed LLM outputs.
2. **Table 3:** The aggregate-level replication of Heuristics and Biases (between-subject and within-subject experiments).
3. **The ML Baseline:** The XGBoost prediction pipeline (found in `ml_prediction/`) to serve as a non-LLM machine learning baseline for comparison.

---

## 🛑 CHECKPOINT 1: Understanding Phase Complete

**Before proceeding, confirm:**
- [ ] `notes/paper_summary.md` generated with research question, methodology, data, and findings.
- [ ] Paper concepts successfully mapped to the codebase and CSV files.
- [ ] `notes/literature_verification.md` created, and all citations rigorously verified to prevent hallucinations.
- [ ] `notes/replication_scope.md` created outlining the specific tables/figures to be reproduced.

**Present for review:**
1. Your summary of the paper's Methodology / Identification Strategy.
2. The verification status of the literature review table.
3. Your defined replication scope (what exact tables/figures we are targeting).

**STOP and wait for human approval before proceeding to Phase 2.**

---

## PHASE 2: Data Validation and Core Replication

### Task 2.1: Load and Validate the Pre-Computed Data
Before running the evaluation scripts, you must refer to replication scope and ensure the data is structurally sound. Please refer to `notes/paper_summary.md` and `notes/replication_scope.md`. Write a temporary Python script or use interactive Python to examine the three core CSV files located in the model directory you selected in Task 0.3 (e.g., `Marketing-Science-Submission-Simulation-Replication-Files/Text Persona - GPT4.1-mini/csv_comparison/csv_formatted/`).

For each of the three CSVs (`responses_wave1_3`, `responses_wave4`, `responses_llm_imputed`), document the following in `notes/data_validation.md`:
1. **Dimensions:** Does the row count match the expected $N=2,058$ participants?
2. **Task Coverage:** Do the columns reflect the 17 tasks (11 between-subject, 5 within-subject, 1 pricing) discussed in the paper?
3. **Data Integrity:** Are there unexpected missing values (NaNs) or formatting errors in the numerical data?

### Task 2.2: Replicate Individual-Level Accuracy (Figure 2 / Table 2)
Execute the Mean Absolute Deviation (MAD) accuracy evaluation pipeline to calculate how closely the digital twins match the human test-retest baseline.
1. Run the script: `poetry run python3 evaluation/mad_accuracy_evaluation.py --config "Marketing-Science-Submission-Simulation-Replication-Files/[CHOSEN_MODEL]/evaluation_config.yaml"`
2. Save the terminal output and any generated CSV/Excel summaries to the `notes/` directory.
3. Extract the **Average Test-Retest Accuracy** and the **Average Digital Twin Accuracy**. 

### Task 2.3: Replicate Aggregate-Level Effects (Table 3)
Execute the within-subject and between-subject behavioral analysis to see if the twins replicate classic economic heuristics (e.g., framing effects, Allais problem).
1. Run the script: `poetry run python3 evaluation/within_between_subjects.py --config "Marketing-Science-Submission-Simulation-Replication-Files/[CHOSEN_MODEL]/evaluation_config.yaml"`
2. Save the output. Identify which specific behavioral effects successfully replicated and which failed (e.g., Sunk Cost Fallacy, Outcome Bias).

### Task 2.4: Explicit Comparison and Discrepancy Protocol
Create a final comparison document named `notes/replication_comparison.md`. You must explicitly compare your generated results against the findings you extracted from the PDF in Phase 1.

**Comparison Table Format:**
| Metric / Task | Original Paper Reported | Agent Replicated | Difference | Status (Pass/Fail/Investigate) |
|---------------|-------------------------|------------------|------------|--------------------------------|
| Average Test-Retest | 81.72% | [Your Result] | [Diff] | [Status] |
| Average Twin Accuracy | 71.72% | [Your Result] | [Diff] | [Status] |
| Outcome Bias Replicated?| No | [Your Result] | N/A | [Status] |

**Discrepancy Tolerance and Fallback Rules:**
* **Strict Tolerance:** Because you are evaluating *pre-computed* CSVs using a deterministic mathematical script, your results should perfectly match the paper. We allow a maximum tolerance of **< 1.0%** absolute difference to account for minor Python versioning or float rounding differences.
* **If divergence is > 1.0% or behavioral replication flags mismatch:** 1. **DO NOT PROCEED to writing.** 2. Document the exact error. 
    3. Verify you ran the script against the exact model variant used for the paper's headline numbers (typically `Text Persona - GPT4.1-mini`). 
    4. Write a diagnostic summary of why the math might be failing (e.g., "The evaluation script is dropping rows with NaNs while the paper included them").

---

## 🛑 CHECKPOINT 2: Validation and Replication Complete

**Before proceeding, confirm:**
- [ ] `notes/data_validation.md` created and dimensions verified ($N=2058$).
- [ ] `mad_accuracy_evaluation.py` successfully executed.
- [ ] `within_between_subjects.py` successfully executed.
- [ ] `notes/replication_comparison.md` created with the explicit comparison table.
- [ ] All discrepancies fall within the < 1.0% tolerance, OR detailed diagnostic notes have been written if they exceed it.

**Present for review:**
1. The Data Validation summary (confirming $N=2058$).
2. The exact text of your Comparison Table from Task 2.4.
3. Your plan to resolve any discrepancies found (if applicable).

**STOP and wait for human approval before proceeding to Phase 3.**

---

## PHASE 3: Write-Up and Documentation Phase

### Task 3.1: Structure the Replication Report
Create a new file named `output/paper/replication_report.md`. Initialize the document with the following standard academic structure:
1. **Abstract** (~150 words)
2. **Introduction** (Context, paper goal, and summary of replication success)
3. **Replication Methodology** (Data sources, LLM variants tested, and evaluation metrics)
4. **Results: Individual-Level Accuracy** (Replication of Figure 2 / Table 2)
5. **Results: Aggregate-Level Behaviors** (Replication of Table 3)
6. **Discussion and Discrepancies** 7. **Conclusion**

### Task 3.2: Draft Methodology and Data Section
Write the Methodology section. You must explicitly detail:
* That this is a computational replication using the authors' pre-generated LLM outputs.
* The specific dataset used ("Twin-2K-500") and its demographics ($N=2058$, 4 waves).
* The primary metric used for evaluation: Mean Absolute Deviation (MAD), and how it bridges binary and numerical survey responses.

### Task 3.3: Present Results and Discrepancy Analysis
Draft the Results and Discussion sections. 
1. **Side-by-Side Presentation:** Present your replicated data immediately adjacent to the original authors' reported numbers using Markdown tables.
2. **Discrepancy Discussion:** If your results matched exactly, state this clearly. If there were discrepancies (even minor <1.0% variations), dedicate a paragraph to hypothesizing why this occurred (e.g., package versioning, float rounding, handling of edge cases in the evaluation script).
3. **Behavioral Divergence:** Highlight the specific behavioral economics experiments where the digital twins failed to match human irrationality (e.g., the Sunk Cost Fallacy and Outcome Bias).

### Task 3.4: Compile Reproducibility Documentation
A successful replication must itself be reproducible. Create/Update the `README.md` in the root directory to include:
1. **Prerequisites:** Note the use of `poetry` and Python 3.x.
2. **Data Access:** Provide the command to download the data (`poetry run python download_dataset.py`).
3. **Execution Steps:** Provide the exact terminal commands required to run the MAD evaluation and the within/between-subjects evaluation.
4. **File Output Map:** Briefly explain where the evaluation scripts output their results so future researchers can find them.

---

## 🛑 CHECKPOINT 3: Final Report Draft Complete

**Before proceeding, confirm:**
- [ ] `replication_report.md` fully drafted according to the requested structure.
- [ ] Results presented side-by-side with original findings.
- [ ] Any discrepancies clearly addressed in the Discussion section.
- [ ] `README.md` updated with clear, copy-pasteable instructions for reproducibility.

**Present for review:**
1. The Abstract and Conclusion of your replication report.
2. The compiled Results tables showing your numbers vs. the original numbers.
3. The updated execution instructions from your `README.md`.

**STOP and wait for final human approval before packaging the deliverables.**