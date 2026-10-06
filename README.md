# Post-MI interferon / oxidative-phosphorylation analysis code

Minimal supplementary code for the longitudinal public-transcriptome study of
within-patient interferon-alpha-response and oxidative-phosphorylation scores
after myocardial infarction, with independent blood, single-cell and LVEF analyses.

## Files and scope

The repository has only this README and `Supplementary_Code_minimal.zip`.
The ZIP contains the executed analysis source, frozen scoring specifications,
software versions, original-data locations and the minimum aggregate inputs for
the portable numerical check. Duplicate independent implementations, figure and
document authoring code, manuscript files, installed libraries, raw matrices and
participant-linked working tables are omitted.

No scientific analysis or statistical method was changed when preparing the
archive. Executed scripts and scoring specifications are unchanged copies.
The random-diagnostic CSV is reduced to its required correlation column (all
1,000 rows retained); the prior comparison JSON is reduced to its status fields.
`SOURCE_MAP.json` identifies these two projections and the original source hashes.

## Directly runnable check

Extract the ZIP into a new empty directory. With Python 3.12, run:

```text
python verify_aggregate_outputs.py
```

This uses only the Python standard library. It verifies file integrity and
selected frozen aggregate calculations, including effect/SE identities,
whole-patient bootstrap intervals, paired IFNA-minus-IFNG correlation difference,
and the random-pair fraction with its Wilson interval. Its output is
`AGGREGATE_VERIFICATION.json`. This check does not refit expression-level models
and is not biological validation.

## Software

`requirements.txt` records the executed numerical versions. Python was 3.12.
Scrublet 0.2.3, scikit-learn 1.9.1 and scikit-image 0.26.0 are needed only for the
single-cell doublet sensitivity. Exact versions may require a compatible package
source; a different environment is not claimed to reproduce every numerical value.

## Public inputs and original analysis order

`PUBLIC_INPUTS.json` gives the GEO entry, expression/count and platform URLs.
Use the original processed scales; do not apply another log transformation or
normalization. Source terms and the original study permissions continue to apply.
The original HGNC snapshot fingerprint and fixed pathway memberships are recorded.

Within `original_code/`, preserve the original project-relative directory layout.
Restore the files from `frozen_protocols/` and `scoring_inputs/` to their matching
project-relative locations in a **fresh workspace**, then obtain the public inputs.
The order represented by the executed scripts is:

1. Primary bulk: `pzxx_execution_20261004/prepare_bulk_and_freeze.py`, then
   `analysis_bulk.py`. Restore the explicit public sample/donor/visit manifest,
   platform annotation, HGNC snapshot and source-admission configuration first.
   The preprocessing script expects the original `SAMPLE_MANIFEST.csv` and
   `PROTOCOL_DRAFT.json` locations; they are not reconstructed by this archive.
2. Expanded bulk: `pzxx_upgrade_execution_20261004/protocol/freeze_addendum.py`,
   then `analysis/run_upgrade_analysis.py`. The first script regenerates the
   mean/SD matching universe from the original processed expression matrix.
3. Independent blood cohort: `protocol/prepare_independent_gse61144.py`, then
   `analysis/run_independent_gse61144.py`. Retrieve the GSE61144 SOFT metadata,
   expression matrix, GPL6106 annotation and original article PMC4536992.
4. Bulk sensitivity: `pzxx_local_first_execution_20261004/analysis/run_D_bulk_additions.py`.
5. Single-cell: `pzxx_execution_20261004/singlecell_localization.py`, then
   `pzxx_upgrade_execution_20261004/singlecell/run_singlecell_upgrade.py`, then
   `pzxx_local_first_execution_20261004/singlecell/run_E_donor_pseudobulk.py`.
   The GSE269269 count archive is required; cells are not independent donors.
6. LVEF: `pzxx_clinical_endpoint_execution_20261004/protocol/scoring_preflight/preflight_gse11947_scoring.py`,
   then `analysis/clinical_20261005/run_frozen_clinical_analysis.py`.
   The local metadata helper `prepare_clinical_admission_and_freeze.py` is supplied
   because the core script imports its `sample_metadata` function. Use the public
   GSE11947 full SOFT source and restore the source-admission/preflight records.

These are executed-source copies with historical gates, fixed fingerprints,
overwrite protection and project-relative inputs. They are **not a self-contained
one-command raw-data pipeline**. The clinical source gate also references original
local execution/admission records; adapting those paths is necessary for a new
workspace. Do not fabricate successful gate records or silently disable scientific
eligibility checks. Original clinical/donor working rows, full expression matrices
and historical execution records are not redistributed in this minimal archive.
No complete expression-matrix rerun is claimed for this public deposit.

## Version

Prepared 7 October 2026. Existing research outputs remain frozen. This repository
is the minimal code deposit; supplementary figures/tables and the completed STROBE
reporting checklist belong to the manuscript submission materials.
