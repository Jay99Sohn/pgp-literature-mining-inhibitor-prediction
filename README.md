# Literature-Derived P-gp Inhibitor Prediction

A portfolio-style reconstruction of a personal research project on **P-glycoprotein (P-gp/ABCB1) inhibitor prediction**.

This project started from a literature-driven workflow for organizing P-gp-related compound interactions and later evolved into a curated inhibitor prediction pipeline using molecular feature engineering and traditional machine learning benchmarking.

---

## Project Summary

### What I built
- A **compound-level aggregation workflow** for literature-derived P-gp interaction records
- Multiple curated downstream datasets for:
  - **inhibitor vs non-inhibitor** classification
  - **inhibitor/substrate-oriented** problem reformulation
- A **final 522-compound inhibitor dataset** with recovered SMILES
- A **traditional machine learning benchmark** using Morgan fingerprints and RDKit descriptors
- A **graph-model comparison** (GCN, GAT, GINE) scored on the baseline’s own folds

### Why this project matters
P-glycoprotein is a major ATP-dependent efflux transporter involved in **drug disposition, multidrug resistance, and transporter-mediated pharmacokinetic behavior**.

This project focused on turning noisy literature-derived interaction information into a structured and model-ready dataset for inhibitor prediction.

---

## Key Outputs

### Curated datasets
- **`output_prefname_count.txt`**
  - Aggregated compound-level interaction table
  - **2,895 compounds**

- **`pgp_dataset_inhibitor_vs_non.tsv`**
  - Early high-confidence inhibitor vs non-inhibitor dataset
  - **350 compounds**

- **`pgp_dataset_for_inhibitor_model_v2.csv`**
  - Expanded inhibitor-focused dataset
  - **523 compounds**

- **`pgp_dataset_for_substrate_model_v2.csv`**
  - Expanded substrate-focused dataset
  - **540 compounds**

- **`pgp_dataset_for_inhibitor_model_with_smiles_522.csv`**
  - Final curated inhibitor dataset with recovered SMILES
  - **522 compounds**

### Benchmark

522 compounds, nested 5-fold stratified cross-validation, bootstrap 95 %
confidence intervals over the five fold values. Tabular and graph models are
scored on **identical outer folds**, so the comparison is paired.

| Model | Representation | ROC-AUC | 95 % CI |
|---|---|---|---|
| **RandomForest** | Morgan 2048 + 12 RDKit descriptors | **0.8044** | 0.7550–0.8450 |
| GAT | molecular graph, atom + bond features | 0.7564 | 0.7260–0.7907 |
| GCN | molecular graph, atom features only | 0.7126 | 0.6889–0.7363 |
| GINE | molecular graph, atom + bond features | 0.6333 | 0.5917–0.6782 |

**No graph model reached the descriptor baseline.** Per fold the Random Forest
wins 5 of 5 against GCN, 5 of 5 against GINE and 4 of 5 against GAT. GCN and GINE
fall below it by a margin five folds can resolve (paired t, p = 0.012 and p = 0.003);
GAT, at p = 0.114, is not separated from the baseline either way. The claim the
comparison supports is that none of the three improved on the baseline.

GINE is the weakest despite carrying the richest representation — bond features
and an MLP aggregator. On 522 molecules the extra capacity costs more than the
representation returns, which is the same direction the whole comparison points:
on this dataset the constraint is not how the molecule is represented.

The labels are counts of how a compound is described across published abstracts,
not assay measurements, so a ceiling of this kind is what one would expect. That
is the question the benchmark leaves open — whether a richer representation would
help at all, or whether the labels are the binding constraint.

Full numbers in [`results/phase1/`](results/phase1/); the Phase 0 tabular-only
run is in [`results/phase0/`](results/phase0/).

> The Phase 0 baseline published 0.8065 [0.7581, 0.8481]. Re-running it inside the
> Phase 1 notebook returns 0.8044 [0.7550, 0.8450] — a 0.002 difference
> attributable to library versions — which is what confirms the two sets of
> numbers sit on the same scale.

---

## Workflow Overview

### 1. Literature-derived interaction aggregation
The original project began with literature-based extraction and organization of P-gp-related compound interactions into a structured compound-level table.

### 2. Dataset curation
From the aggregated interaction records, I built multiple downstream datasets:
- an early **high-confidence inhibitor set**
- a later **inhibitor/substrate reformulation**
- a final **522-compound inhibitor modeling dataset**

### 3. Molecular representation
For the later benchmark stage, the final curated dataset was paired with:
- **Morgan fingerprints (ECFP-like features)**
- **RDKit molecular descriptors**

### 4. Baseline benchmarking
I benchmarked traditional ML models and selected the best saved baseline based on nested cross-validation performance.

### 5. Graph-model comparison (Phase 1)
Molecular graphs built from the same 522 structures, scored on the same folds as
the baseline: GCN, GAT and GINE against the Morgan + descriptor Random Forest.
The notebook history also holds earlier exploratory work on inhibitor/substrate
dual modelling and interpretability (XAI) visualisation.

---

## Repository Structure

- `README.md`
- `LICENSE`
- `.gitignore`
- `data/`
  - `README_data.md`
  - `processed/`
- `docs/`
  - `project_story.md`
  - `data_dictionary.md`
  - `limitations.md`
- `AI_USAGE.md`
- `notebooks/`
  - `01_sohnproject1_origin_archive.ipynb`
  - `02_newpgp_dual_model_expansion.ipynb`
  - `03_8_15_all_newpgp_main.ipynb`
  - `pgp_phase1_benchmark.ipynb`
- `results/`
  - `phase0/`
  - `phase1/`
  - `xai/`

---

## Notebook Guide

### `01_sohnproject1_origin_archive.ipynb`
Original literature-mining-oriented workflow and early inhibitor-focused modeling history.

### `02_newpgp_dual_model_expansion.ipynb`
Later expansion of the project toward inhibitor/substrate-oriented problem framing.

### `03_8_15_all_newpgp_main.ipynb`
The most polished later-stage notebook, centered on the final **522-compound inhibitor dataset** and cleaner benchmark reporting.

### `pgp_phase1_benchmark.ipynb`
Phase 1. Rebuilds the Phase 0 baseline as a protocol check, then scores GCN, GAT
and GINE on the same folds. Reads the dataset from this repository over HTTPS and
checkpoints each stage, so an interrupted session resumes. Written with AI
assistance — see [`AI_USAGE.md`](AI_USAGE.md).

---

## Included Results

### `results/phase0/`
Saved outputs for the traditional ML benchmark stage, including:
- benchmark summary JSON
- final report text file
- performance matrix
- learning curve data
- benchmark visualization figure

### `results/phase1/`
Graph-model comparison against the Phase 0 baseline:
- `phase1_benchmark_results.csv` — summary metrics with confidence intervals
- `phase1_fold_auc.csv` — per-fold ROC-AUC for every model
- `phase1_report.txt` — protocol, results and the protocol check

### `results/xai/`
Representative interpretability output images from later exploratory analysis.

---

## Limitations

- Labels in this repository are **literature-derived**, not assay-standardized ground truth labels.
- This repository is a **portfolio-style reconstruction**, not a full raw archive of every intermediate file generated during the project.
- The graph models were written and trained in July 2025, but their outputs were cleared before the notebooks were archived and the Phase 1 result directories were left empty. The graph figures reported here come from a **re-run under the Phase 0 protocol** and should be read as a reproduction, not as the original results. The earlier AttentiveFP runs were not reproduced.
- Five outer folds give the comparison limited resolution: it can show that no graph model reached the baseline, but not that each one is significantly below it.
- See [`AI_USAGE.md`](AI_USAGE.md) for how the Phase 1 notebook was written.

---

## Skills Demonstrated

- Literature-driven dataset construction
- Compound normalization and data curation
- Label engineering for bioactivity-related classification
- Molecular feature extraction with RDKit-style workflows
- Traditional ML benchmarking with nested cross-validation
- Research iteration and portfolio-oriented project packaging

---

## Notes
This repository was reorganized from an exploratory personal research archive into a cleaner, portfolio-friendly format while preserving the main development stages of the project.
