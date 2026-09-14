# AI · Tool Usage Disclosure

## 1. Generative-AI use

This repository used generative AI (Anthropic Claude) as an **assistive tool**
for one file: `notebooks/pgp_phase1_benchmark.ipynb`, added in September 2026.

- **Scope of use:** code writing and debugging for that notebook, and drafting
  its documentation.
- **Author's role:** the study design — which architectures to compare, and the
  protocol to compare them under; the evaluation code, carried over unchanged
  from the author's own Phase 0 notebook so that both sets of numbers sit on one
  scale; directing and running the benchmark, including the decision to reproduce
  the published baseline first as a check on the implementation; and the
  interpretation and final judgment of the results.

Everything else in this repository — the literature-mining pipeline, the dataset
construction and the Phase 0 benchmark in `notebooks/01`, `02` and `03` — is the
author's own work from July–August 2025.

## 2. Why the notebook exists

GCN, GAT and GINE were implemented and tuned with Optuna during the July 2025
visiting research at Kyoto University; that code and its Colab execution records
are in `notebooks/01_sohnproject1_origin_archive.ipynb` and
`02_newpgp_dual_model_expansion.ipynb`. Those runs printed their scores to
notebook output rather than writing them to disk, and the output was cleared when
the notebooks were archived, so the figures did not survive — the Phase 1
directories in Drive hold only empty folders.

The comparison is therefore re-run here under the original protocol, rather than
quoted from numbers that can no longer be shown. The model code in this notebook
was written for the re-run and is not the July 2025 code.

## 3. Verification

Cell 5 reproduces the published Phase 0 baseline — 0.8065 against 0.8044, a
difference of 0.002 — before any graph model is reported. That is what
establishes that this implementation measures what the original protocol
measured, and it is the check applied before any of the figures below it were
accepted.

Every number in `results/phase1/` is output from executing the notebook. None was
written by hand or produced by a language model.

## 4. Other tools

The extraction step of the literature-mining pipeline calls the OpenAI Batch API
(`o3-mini`) to read compound–transporter relationships out of PubMed abstracts.
That is a component of the method, described in the README — not assistance with
writing code.
