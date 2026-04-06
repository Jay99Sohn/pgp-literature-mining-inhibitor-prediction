# Literature-Derived P-gp Inhibitor Prediction

A portfolio-style reconstruction of a personal research project on P-glycoprotein (P-gp/ABCB1) inhibitor prediction.

## Highlights
- Built a literature-derived compound aggregation workflow for P-gp-related interactions
- Curated multiple downstream datasets, including a final 522-compound inhibitor dataset with recovered SMILES
- Benchmarked traditional machine learning models using Morgan fingerprints and RDKit descriptors

## Best saved benchmark
- Dataset: 522 compounds
- Features: Morgan fingerprints + RDKit descriptors
- Model: RandomForest
- Evaluation: Nested 5-fold stratified CV
- ROC-AUC: 0.8065
- 95% CI: 0.7581–0.8481

## Repository contents
- `notebooks/`: chronological notebooks showing project evolution
- `data/processed/`: curated datasets used in later modeling
- `results/phase0/`: saved benchmark summaries and figures
- `results/xai/`: representative interpretability outputs
- `docs/`: project notes, data dictionary, and limitations

## Notes
This repository is intentionally organized for portfolio clarity.
Only saved and verifiable outputs are presented as headline results.
Exploratory GNN/AttentiveFP work is included as notebook history, but not promoted as a primary benchmark because the current archive does not contain final saved Phase1 result files.
