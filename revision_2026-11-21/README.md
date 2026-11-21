# Revision 2026-11-21 (manuscript rev6)

The revised manuscript is titled *A reproducible GATK-based feature-engineering pipeline for machine learning on single-cell RNA-seq expressed variants: quality control, filter sensitivity, computational cost and leakage-controlled validation*. This folder holds its supplementary materials, figures and the scripts behind every number in it.

The revision replaces the classification and biomarker claims of the earlier manuscript. Those claims did not reproduce once the condition labels were reconciled with GEO and validation was grouped by sample (see `../REPRODUCIBILITY.md`).

## Contents

| Path | What it is |
|---|---|
| `supplementary/NANRK_rev6_Supplementary_Materials.docx` | Notes S1–S2, Tables S1–S5 |
| `supplementary/NANRK_S*.csv` | the same tables as CSV |
| `figures/` | Figures 1–5 of the manuscript (600 dpi) and per-run QC counts |
| `scripts/` | analysis scripts (below) |

## Scripts

| Script | Purpose |
|---|---|
| `light_00_cache_vcfs.py` | caches per-run PASS VCFs as compact NumPy arrays |
| `light_01_descriptive.py` | run similarity, recurrence-threshold sweep, coverage dependence, GATK runtime |
| `light_02_identity_check.py` | genotype concordance between runs at depth ≥ 10 and ≥ 20 |
| `light_03_exact_null.py` | exact permutation null over all 35 labelings of the 7 samples (sample- and person-level grouping) |
| `light_04_article_figures.py` | manuscript figures |
| `light_05_observed_predictions.py` | held-out predictions per run and per sample under the GEO labels |
| `run_combined_three_design_benchmark.py` | model definitions shared with the main benchmark |

The models (`light_03`, `light_05`) must run with scikit-learn 1.9.0 and XGBoost 3.2.0. With other versions the random-forest and XGBoost values change. The full pipeline (STAR, GATK, cohort filter, gene burden) is in https://github.com/dauletulyaidyn/somatic-like-scrna-variants-ml-pipeline (stage `07_ml_control_vs_disease`).

## Key results

- PASS calls per run range from 608,759 to 1,549,617. The hard filters flag 16.7–23.6% of raw records.
- PASS-call counts follow sequencing depth (Spearman ρ = 0.89), not tissue state.
- No recurrence threshold k = 1–14 produces a condition effect.
- GATK calling took about 170 wall-clock hours for 14 runs.
- Sc_Skin1 (GSM5364333) and Sc_W2 (GSM5364338) have identical genotypes, so the 7 samples come from 6 people.
- With sample- or person-grouped validation and training-only loci, every model reaches balanced accuracy 0.500. No design is significant on the exact test (minimum p = 0.200).
