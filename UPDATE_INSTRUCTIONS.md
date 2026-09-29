# Update to 7.8.0-conditional-projection

1. Unzip `NKPI_Conditional_Projection_v7_8_GitHub.zip` and upload the extracted contents at your GitHub repository root. Preserve the folders and replace matching files.
2. Include **all** release files, especially `requirements.txt`, `nkpi/projection.py`, `research/projection_model.json`, `research/projection_model.sha256`, `components/schema.js`, `components/app.js`, `components/progression_summary.js`, `components/index.html`, `components/app.css`, `nkpi/service.py` and `kcn_dual_calculator_app.py`.
3. Keep `kcn_dual_calculator_app.py` as the Streamlit entry point. Reboot Streamlit so the added NumPy dependency is installed.
4. Reload and confirm **7.8.0-conditional-projection** in the footer. This version has a fresh component key and cache suffix.
5. Import the visits, calculate, then open **Progression summary · Both eyes** below the NKPI results.

Eligible paired results now display a calculated count and an assumption range. This is a conditional research projection, not a percentage probability. Unsupported comparisons show a specific reason and preserve available observed measurements. Single visits cannot produce a trend.

To inspect the design before deploying, open `docs/OUTLOOK_PREVIEW.html` locally after extraction. Its two synthetic eyes use the same backend calculation and renderer as the app.

If the old “Six-month estimate withheld” card persists, this release has not fully replaced the deployed files: check the footer, repository, branch and entry point, then reboot/reload. No patient-specific information belongs in the GitHub repository.
