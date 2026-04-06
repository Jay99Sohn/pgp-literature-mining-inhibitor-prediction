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
- Exploratory notebook history for later **GNN / XAI follow-up analysis**

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

### Best saved benchmark
**Traditional ML baseline**
- **Dataset:** 522 compounds
- **Features:** Morgan fingerprints + RDKit descriptors
- **Model:** RandomForest
- **Evaluation:** Nested 5-fold stratified cross-validation
- **ROC-AUC:** **0.8065**
- **95% CI:** **0.7581–0.8481**

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

### 5. Follow-up exploration
The notebook history also includes exploratory follow-up work related to:
- inhibitor/substrate dual modeling
- graph-based modeling attempts
- interpretability / XAI visualization

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
- `notebooks/`
  - `01_sohnproject1_origin_archive.ipynb`
  - `02_newpgp_dual_model_expansion.ipynb`
  - `03_8_15_all_newpgp_main.ipynb`
- `results/`
  - `phase0/`
  - `xai/`

---

## Notebook Guide

### `01_sohnproject1_origin_archive.ipynb`
Original literature-mining-oriented workflow and early inhibitor-focused modeling history.

### `02_newpgp_dual_model_expansion.ipynb`
Later expansion of the project toward inhibitor/substrate-oriented problem framing.

### `03_8_15_all_newpgp_main.ipynb`
The most polished later-stage notebook, centered on the final **522-compound inhibitor dataset** and cleaner benchmark reporting.

---

## Included Results

### `results/phase0/`
Saved outputs for the traditional ML benchmark stage, including:
- benchmark summary JSON
- final report text file
- performance matrix
- learning curve data
- benchmark visualization figure

### `results/xai/`
Representative interpretability output images from later exploratory analysis.

---

## Limitations

- Labels in this repository are **literature-derived**, not assay-standardized ground truth labels.
- This repository is a **portfolio-style reconstruction**, not a full raw archive of every intermediate file generated during the project.
- Exploratory GNN / AttentiveFP work is included as notebook history, but **not presented as a headline benchmark** because the current saved archive does not contain final Phase1 result files.

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
