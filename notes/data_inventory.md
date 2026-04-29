# Data Inventory

## Date
2026-04-28

## Base Path
`orig/MktS_2025/Marketing-Science-Submission-Simulation-Replication-Files/`

## Model Configurations (12 total)

| # | Model Directory | Presence of 3 Critical CSVs |
|---|-----------------|------------------------------|
| 1 | JSON Persona (Predicted Output) - GPT4.1-mini | ✓ |
| 2 | JSON Persona (Predicted Output) - GPT4.1 | ✓ |
| 3 | JSON Persona - GPT4.1-mini | ✓ |
| 4 | JSON Persona - GPT4.1 | ✓ |
| 5 | LLM Finetuning (500 training samples) - GPT4.1-mini | ✓ |
| 6 | Persona Summary - GPT4.1-mini | ✓ |
| 7 | Persona Summary - JSON Persona - GPT4.1-mini | ✓ |
| 8 | Text Persona (Default Temperature) - GPT4.1-mini | ✓ |
| 9 | Text Persona (Reasoning) - GPT4.1-mini | ✓ |
| 10 | Text Persona (Repeating Questions) - GPT4.1-mini | ✓ |
| 11 | Text Persona - GPT4.1-mini | ✓ |
| 12 | text-base-simulation-Gemini-flash2.5 | ✓ |

**All 12 model directories have all 3 required CSVs present.**

---

## Critical CSV File Sizes (per model)

Each model's CSVs are located at:
`<model_dir>/csv_comparison/csv_formatted/`

| Model | responses_llm_imputed_formatted.csv | responses_wave1_3_formatted.csv | responses_wave4_formatted.csv |
|-------|------------------------------------|---------------------------------|-------------------------------|
| JSON Persona (Predicted Output) - GPT4.1-mini | 920K | 768K | 768K |
| JSON Persona (Predicted Output) - GPT4.1 | 924K | 768K | 768K |
| JSON Persona - GPT4.1-mini | 476K | 396K | 396K |
| JSON Persona - GPT4.1 | 764K | 768K | 768K |
| LLM Finetuning (500 training samples) - GPT4.1-mini | 592K | 592K | 592K |
| Persona Summary - GPT4.1-mini | 748K | 752K | 748K |
| Persona Summary - JSON Persona - GPT4.1-mini | 768K | 752K | 748K |
| Text Persona (Default Temperature) - GPT4.1-mini | 768K | 768K | 768K |
| Text Persona (Reasoning) - GPT4.1-mini | 768K | 768K | 768K |
| Text Persona (Repeating Questions) - GPT4.1-mini | 768K | 768K | 768K |
| Text Persona - GPT4.1-mini | 768K | 768K | 768K |
| text-base-simulation-Gemini-flash2.5 | 764K | 768K | 768K |

---

## Drill-Down: Text Persona - GPT4.1-mini

Full paths:
- `orig/MktS_2025/Marketing-Science-Submission-Simulation-Replication-Files/Text Persona - GPT4.1-mini/csv_comparison/csv_formatted/responses_llm_imputed_formatted.csv` — **768K**
- `orig/MktS_2025/Marketing-Science-Submission-Simulation-Replication-Files/Text Persona - GPT4.1-mini/csv_comparison/csv_formatted/responses_wave1_3_formatted.csv` — **768K**
- `orig/MktS_2025/Marketing-Science-Submission-Simulation-Replication-Files/Text Persona - GPT4.1-mini/csv_comparison/csv_formatted/responses_wave4_formatted.csv` — **768K**

`evaluation_config.yaml` for this model:
```yaml
trial_dir: "Marketing-Science-Submission-Simulation-Replication-Files/Text Persona - GPT4.1-mini/"
model_name: "text-persona-gpt4.1-mini"
evaluation:
  output_dir: "${trial_dir}/accuracy_evaluation"
  mad_plot_title: "Digital Twin Simulation - Text Persona (GPT-4.1-mini)"
```

---

## Additional CSV Files (some models)
Some model directories also contain `csv_formatted_label/` subdirectories with label variants:
- `responses_llm_imputed_label_formatted.csv`
- `responses_wave1_3_label_formatted.csv`
- `responses_wave4_label_formatted.csv`

And some (e.g. `Persona Summary - GPT4.1-mini`) include raw (un-formatted) CSVs directly in
`csv_comparison/`:
- `responses_llm_imputed.csv`
- `responses_wave1_3.csv`
- `responses_wave4.csv`
- `randdollar_breakdown.csv`

---

## Conclusion
All critical CSVs required for MAD evaluation are present and non-empty across all 12 model
configurations. The data is intact and ready for evaluation.
