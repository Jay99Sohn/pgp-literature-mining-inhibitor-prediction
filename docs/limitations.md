# Limitations

- Labels in this repository are literature-derived and should not be interpreted as assay-standardized ground truth labels. They count how a compound is described across published abstracts, so the models rank hypotheses rather than predict measured activity.
- The graph models were written and trained in July 2025, but their scores were printed to notebook output rather than written to disk, and the output was cleared before the notebooks were archived. The Phase 1 directories in Drive contain only empty AttentiveFP folders. The graph figures in `results/phase1/` are therefore a re-run under the Phase 0 protocol, not a recovery of the original results; see `AI_USAGE.md`.
- The earlier AttentiveFP work was not reproduced. Only GCN, GAT and GINE were re-run.
- Five outer folds give the comparison limited resolution. It supports the statement that no graph model reached the baseline, but not that each one is significantly below it: only GINE separates unambiguously.
- This repository is a portfolio-style reconstruction, not a full raw archive of every intermediate file generated during the project.
