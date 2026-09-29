# NKPI 7.8 — Conditional six-month projection

The **Progression summary · Both eyes** dropdown now calculates a six-month research projection. Each dark-purple eye card shows:

- Projected domain crossings, **0–4**, under the central noise assumption.
- A range across four explicit scan-noise assumptions.
- The actual observed **0–4** count over the selected scan interval.
- The existing four-domain measurement details, expanded below the card.

The forecast reference is **the latest scan → 183 days later**. It estimates further threshold crossings from that new reference; it does not add the previously observed count or stretch the observed interval to six months. The dropdown stays closed until clicked. There are no new eye maps or measurement-outlook charts.

**This is a functioning conditional research calculation, not a validated probability model.** It combines the recent change with a joint trend distribution fitted to **179 eligible eye pairs / 101 patients**. The dataset has no third scans to validate forecasts made from two visits. Scan noise is explicitly assumed and varied; it was not measured in this dataset. A broad range such as 0–4 is retained when the comparison cannot resolve the two-domain criterion.

Read [the model specification](docs/SIX_MONTH_PROJECTION.md) for equations, noise assumptions, exclusions and limitations. Open [the synthetic preview](docs/OUTLOOK_PREVIEW.html) after unzipping to inspect the production renderer with computed research projections. Its values are fictional, and its counts are calculated by the shipped code.

## What stays the same

The 19-file browser extraction workflow, automatic consistency checks, bilateral import, frozen **3.1.0-interval-half NKPI model**, model score and observed biological thresholds are preserved. The model's existing limitations remain. Age does not automatically slow the new projected trend. A high NKPI score does not add domain crossings.

The existing PDF remains an NKPI report. The audited JSON now includes a separately labelled `projection` object with the model hash, input hash, assumptions, counts, ranges and projected values. Raw patient data are not included in the GitHub package; only aggregate fitted parameters are shipped.

## Install or update

1. Extract **NKPI_Conditional_Projection_v7_8_GitHub.zip**.
2. Upload its **contents** to the repository root, replacing matching files and preserving folders. Do not upload the ZIP itself.
3. Use `kcn_dual_calculator_app.py` as the Streamlit main file. Include the updated `requirements.txt`, both `models/` and `research/`, and all `components/` files. NumPy is now needed for projection inference.
4. Reboot Streamlit and refresh the page. Confirm **7.8.0-conditional-projection** in the footer.
5. Import and calculate as before, then open **Progression summary · Both eyes** below NKPI.

Unused historical viewer assets and their tests were removed from this distribution to keep it under 100 files. The shared map and numerical-schema helpers used by the importer remain. Old unused files may remain in an existing repository; the calculator does not load those viewers.

## Eligibility and uncertainty

Two complete, verified, same-eye visits are required. Explicit poor scan quality, prior/interval treatment, unsupported age, measurements outside the fitted range, or physically implausible simulated values withhold the projection with a specific reason. Valid observed domains remain visible independently.

When treatment history or scan quality is unknown, the card explicitly describes an **assumed untreated/comparable-scan scenario**; it does not mark those facts as confirmed. Histories shorter than 90 days show an extrapolation warning. No new mandatory per-measurement verification is added.

The range combines central 90% simulation ranges across assumed noise scenarios. It is **not** an empirically calibrated confidence interval, individual progression probability, or a treatment recommendation. The full assumptions are expandable inside each card.

## Observed-domain rules — unchanged

| Domain | Strict crossing threshold |
|---|---|
| Anterior curvature | ARC decrease >0.106 mm **or** Kmax increase >1.0 D |
| Posterior curvature | PRC decrease >0.085 mm |
| Pachymetric | Thinnest thickness decrease >2% of reference **or** ARTmax decrease >44.24 |
| Composite deviation | BAD-D increase >0.42 |

Each domain counts once. Equality does not cross. The observed calculation uses the earlier visit as reference; the projection uses the latest visit. Two domains meet the numerical SOURCE research criterion, subject to its comparison requirements; neither count diagnoses progression. The structural 0–3 sensitivity check continues to exclude overlapping BAD-D. SOURCE eligibility requires a pretreatment comparison at least six calendar months apart; the 183-day forecasting approximation does not change that eligibility rule.

## Run and test

```bash
pip install -r requirements.txt
streamlit run kcn_dual_calculator_app.py
python tools/verify_package.py
python tests/test_projection.py
node tests/test_progression_summary.cjs
python tests/test_model_interval.py
node tests/test_extraction_integrity.cjs
node tests/test_bilateral_import.cjs
node tests/test_bilateral_review.cjs
```

Projection-fitting tests additionally require pandas. Historical domain-training tests require pandas and scikit-learn. Deployment never trains on patient inputs. See [the engineering test report](docs/TEST_REPORT.md) and [the earlier probability-model results](docs/DOMAIN_TRAINING_REPORT.md). Earlier probability candidates remain withheld; the new conditional trend calculation does not overturn their failed performance checks.
