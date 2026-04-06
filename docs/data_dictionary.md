# Data Dictionary

## output_prefname_count.txt
- `input_name`: original compound name in processed outputs
- `desalted_inchikey`: normalized/desalted InChIKey
- `desalted_pref_name`: normalized preferred compound name
- `sum_total_count`: total literature-derived count
- `substrate_count`: substrate-related count
- `inhibitor_count`: inhibitor-related count
- `inducer_count`: inducer-related count
- `other_count`: other-related count

## pgp_dataset_inhibitor_vs_non.tsv
Early high-confidence inhibitor vs non-inhibitor dataset.

Important columns:
- `inhibitor_score`
- `pgp_inhibitor`
- `smiles`

## pgp_dataset_for_inhibitor_model_with_smiles_522.csv
Final curated inhibitor dataset used in the later benchmark stage.

Important columns:
- `inhibitor_score`
- `substrate_score`
- `label`
- `smiles`
- `smiles_source`
