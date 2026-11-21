# Reproducible GATK-Based Pipeline for Expressed-Variant Gene-Burden Features from Single-Cell RNA-Seq

Support repository for article 1 (NAN RK / ASJCS, submission #9136), version 1.1.0.

**Current manuscript: revision 6 (2026-11-21). Its materials, figures and scripts are in [`revision_2026-11-21/`](revision_2026-11-21/).**

Revision 6 changes the paper from a classification and biomarker study into a reproducible-pipeline study. It covers quality control, filter sensitivity, coverage dependence, computational cost and a grouped validation check against an exact permutation null. The earlier classification results (balanced accuracy 0.97, signed biomarkers) are withdrawn. They did not reproduce for three reasons: the legacy labels were inverted relative to GEO, the cross-validation split runs rather than samples, and recurrent loci were selected on the whole cohort. Everything else in this repository is kept as a historical record of the earlier version.

## Historical package (manuscript rev1–rev5)

The manuscript-specific numerical results of rev1–rev5 have not been reproduced by this package. Archived source files and manuscript-reported claims are separated. Public GSE176415 metadata contain four unwounded-skin and three wound biological samples; the fourteen runs comprise eight UWE and six WE observations. Legacy labels disagree with this mapping. The archived CV uses run-level splits and fixed hyperparameters, not donor/GSM-grouped nested tuning. Cohort-frequency filtering uses the entire cohort. Archived PCA values, coefficients and some classifier summaries differ from the manuscript. Revision 6 repeats the analysis with reconciled labels and training-only feature construction.

## Contents

- `revision_2026-11-21/`: rev6 supplementary materials, figures and analysis scripts (current).
- `supplementary/`: Word supplement, supplementary methods, numbered Tables S1–S3 and source-result tables.
- `archive/`: unchanged historical matrices, metrics, coefficients, metadata and dependency definitions.
- `data/metadata_source_reconciled.csv`: source-derived run labels and GSM groups for future reanalysis.
- `scripts/legacy/`: original pipeline code retained for provenance.
- `provenance.json`: SHA-256 manifest and relative PAD source paths.
- `REPRODUCIBILITY.md`: unresolved claim-to-artifact differences.

## Verify the package

```bash
python scripts/validate_package.py
```

This uses only Python standard-library modules. Success indicates file integrity, not scientific validation.

## Reanalysis prerequisites

Use Linux/WSL with STAR, samtools, bcftools, BEDTools and Python scientific packages described in `archive/requirements-wsl.txt` and `archive/environment.yml`. The historical scripts expect a conventional repository root one level above `scripts`; here they are preserved under `scripts/legacy`, so inspect their `BASE`/`ROOT` variables and pass explicit input/output paths or reconstruct their original layout. Download source FASTQ and compatible GRCh38/GENCODE references separately. Do not run legacy labels as a confirmatory WE/UWE analysis. Preserve GSM groups during evaluation and fit recurrent-locus filtering inside training folds.

## Relationship to the original project

Derived from local PAD source materials. Original general project: https://github.com/dauletulyaidyn/somatic-like-scrna-variants-ml-pipeline. This repository has a separate article-specific name, description and support scope. It does not represent an independent cohort or a new validation study.

## Sources

- [GSE176415](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE176415)
- [PRJNA736095](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA736095)

No manuscript is published here. Code/data licensing has not been newly assigned; consult original owners and source terms.

## Journal and supplied template

Target: [Academic Scientific Journal of Computer Science](https://journals.nauka-nanrk.kz/physics-mathematics/index). Article/template number: 1. Supplied template: `1. article_template_all.docx`. The earlier ETASR/MDPI appearance came from preliminary manuscript files and is not the journal destination. The corrected local manuscripts retain the supplied filled journal versions and now cite this support repository and its supplementary package.

See `JOURNAL_ALIGNMENT.md` for boundaries and submission-file handling.

## Journal attachment contents

`supplementary/` contains only the journal supplement DOCX and Tables S1-S3 (CSV). Historical output copies are kept in `archive/submission_excluded`; the editable supplement source is in `docs/`. Submission ZIP files exclude source code, repository documentation, provenance manifests and historical archives. The manuscript explicitly cites all three supplementary tables and methods.
