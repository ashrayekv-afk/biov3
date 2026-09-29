# Release 7.8 engineering verification

These checks verify implementation and workflow. They do not establish clinical accuracy, probability calibration or future range coverage.

## Passed

- Eight projection tests: zero-noise recovery of raw extrapolation; conditional covariance checked against an independent 180,000-case three-scan simulation; recovery of known correlated slopes on synthetic data; positive covariance and short-interval uncertainty; all strict component boundaries and OR rules; deterministic bilateral output and latest-scan reference; held/unknown/missing input behavior; and artifact checksum rejection.
- Actual parent-app event handlers tested against real Python responses: both-eye calculation, per-eye edits, source invalidation, stale response rejection, patient reset, projection checksum/snapshot checks and independent projected-value/domain checks.
- Existing exact observed-domain thresholds, structural sensitivity, study scope, disabled/single/missing eyes and overlapping domain votes.
- Original model interval tests: frozen 50% interval amendment and score/impact audit unchanged.
- Original extraction-integrity, bilateral import, bilateral review, automatic merge and map-identification tests.
- Historical domain-training tests: endpoint boundaries, patient grouping, no follow-up predictor leakage and retained research-only probability artifacts.
- Headless Chromium preview checks at 1200, 760 and 390 pixels: two calculated cards, no horizontal overflow and working calculation disclosures. Desktop and mobile screenshots visually inspected.
- Streamlit 1.50 AppTest startup: no exception or error elements.
- All 19 extractor files and all three frozen NKPI artifact files are byte-identical to 7.7. The NKPI assessment implementation is byte-identical. PDF calculations are unchanged; only its interface version label is updated to 7.8.0.

## Full-cohort runtime exercise

179 previously eligible paired comparisons were passed through the new service without numerical exceptions. They were used for fitting; this is **not a held-out accuracy test**. Treatment and quality were explicitly set to the assumed eligible scenario for this engineering exercise, not inferred as clinical facts.

- 170 produced conditional counts and ranges.
- 9 withheld a projection because at least one assumed-noise scenario produced unsupported measurement values.
- Every output retained the correct snapshot hash.
- Many ranges crossed the two-domain threshold or spanned 0–4; they were not narrowed to make the display appear more decisive.

## Clinical limits

No new OCR clinical accuracy study was performed. No third visits exist in the provided cohort to test two-visit forecasts. Noise settings, the physical-envelope guard and constant-slope assumption have not been clinically validated. The selected cohort is not a representative natural-history sample. Fitting the slope distribution is not validation of individual projections.

