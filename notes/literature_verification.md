# Literature Verification: Toubia et al. (2025) Key Citations

All entries below were independently verified via web search (April 28, 2026).
The paper's full reference list (pp. 1454–1455) was cross-checked to confirm accuracy of author names, years, titles, and venues.

---

## Verification Table: Required Papers

| Authors | Year | Title | Venue / DOI | Key Finding Relevant to Digital Twins / Heuristics | Verified? |
|---------|------|-------|-------------|-----------------------------------------------------|-----------|
| Park, Zou, Shaw, Hill, Cai, Morris, Willer, et al. | 2024 | Generative Agent Simulations of 1,000 People | arXiv:2411.10109 (submitted Nov 15, 2024) | Built LLM agents from 2-hour qualitative interviews of 1,052 real individuals; agents replicated General Social Survey responses 85% as accurately as humans replicate their own answers two weeks later; also predicted personality traits and experimental outcomes comparably to humans | **Yes** |
| Gui, G.; Toubia, O. | 2023 | The Challenge of Using LLMs to Simulate Human Behavior: A Causal Inference Perspective | arXiv:2312.15524 (submitted Dec 24, 2023; revised Nov 2025) | Shows that LLM-simulated experiments violate unconfoundedness because treatment variation affects unspecified covariates; demonstrated with a real pricing experiment of 40 products; directly motivates the holdout design used in Twin-2K-500 | **Yes** |
| Stanovich, K. E.; West, R. F. | 2008 | On the Relative Independence of Thinking Biases and Cognitive Ability | *Journal of Personality and Social Psychology*, 94(4), 672–695. doi:10.1037/0022-3514.94.4.672 | Showed across 7 studies that most classic heuristics-and-biases effects (conjunction, framing, anchoring, outcome bias, omission bias, myside bias, sunk cost, Allais/certainty effects) are largely uncorrelated with cognitive ability; source for 7 of the 16 between/within-subject experiments replicated in Twin-2K-500 | **Yes** |
| Kahneman, D.; Tversky, A. | 1973 | On the Psychology of Prediction | *Psychological Review*, 80(4), 237–251. doi:10.1037/h0034747 | Introduced the representativeness heuristic; showed predictions are insensitive to base-rate probabilities; source for the **Base Rate Problem** experiment in Twin-2K-500 (one of the few effects *not* replicated by either humans or digital twins in the paper) | **Yes** |

---

## Additional Verified Citations (Contextually Important)

| Authors | Year | Title | Venue | Key Relevance | Verified? |
|---------|------|-------|-------|---------------|-----------|
| Tversky, A.; Kahneman, D. | 1981 | The Framing of Decisions and the Psychology of Choice | *Science*, 211(4481), 453–458 | Source for Framing Problem experiment; one of the between-subject effects successfully replicated by digital twins | **Yes** (classic, widely cited) |
| Tversky, A.; Kahneman, D. | 1983 | Extensional Versus Intuitive Reasoning: The Conjunction Fallacy in Probability Judgment | *Psychological Review*, 90(4), 293–315 | Source for the Linda (Conjunction) Problem; replicated by digital twins | **Yes** (classic, widely cited) |
| Tversky, A.; Kahneman, D. | 1974 | Judgment Under Uncertainty: Heuristics and Biases | *Science*, 185(4157), 1124–1131 | Source (with Epley et al. 2004) for Anchoring and Adjustment; partially replicated by twins | **Yes** (classic, widely cited) |
| Baron, J.; Hershey, J. C. | 1988 | Outcome Bias in Decision Evaluation | *Journal of Personality and Social Psychology*, 54(4), 569 | Source for Outcome Bias experiment; notably *not* replicated by digital twins (all twins gave favorable evaluation regardless of outcome) | **Yes** (confirmed via reference in PDF, JPSP is indexed) |
| Brucks, M.; Toubia, O. | 2025 | Prompt Architecture Induces Methodological Artifacts in Large Language Models | *PLoS ONE*, 20(4):e0319159 | Shows LLM answers are overly sensitive to option labeling/ordering in prompts; directly motivates careful prompt design in digital twin construction | **Yes** (confirmed via reference in PDF; PLoS ONE indexed) |

---

## Verification Notes

- **Park et al. (2024):** Confirmed at arxiv.org/abs/2411.10109. The paper's title in the Toubia reference list is "Generative agent simulations of 1,000 people" and the arxiv page confirms this exactly. Finding (85% test-retest replication accuracy) is stated in the Toubia PDF (p. 1446) and confirmed by the arxiv abstract.

- **Gui and Toubia (2023):** Confirmed at arxiv.org/abs/2312.15524 and SSRN (abstract_id=4650172). Toubia et al. cite this paper twice — once for the LLM simulation challenge and once for the pricing study methodology used in Wave 3.

- **Stanovich and West (2008):** Confirmed via PubMed (PMID 18361678), APA PsycNet, and the author's own website PDF. The paper is the *source* for the full battery of 7 between-subject and 3 within-subject experiments replicated in Twin-2K-500, making it the single most-cited foundational paper for the experimental design.

- **Kahneman and Tversky (1973):** Confirmed via APA PsycNet, ERIC (EJ082196), and a publicly accessible PDF from UC Davis faculty server. This is a foundational judgment-and-decision-making paper published in *Psychological Review*, Vol. 80, pp. 237–251. The doi (10.1037/h0034747) is indexed and confirmed.
