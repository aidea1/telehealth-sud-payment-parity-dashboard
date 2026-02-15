# Telehealth for SUD/MH + Payment Parity Policy Dashboard

This repository hosts a static, interactive dashboard (GitHub Pages-ready) that links state-level telehealth utilization with SUD and mental health (MH) service rates and a **time-aligned policy intensity index** built from 14 binary telehealth/payment parity policy features.

The dashboard is generated as a single `index.html` file (no server required) using Plotly.js and an embedded JSON payload produced by the Python build script.

## What this dashboard shows

1. **Key indicators (filtered)**
   - Telehealth service rate per 1,000 beneficiaries
   - SUD service rate per 1,000 beneficiaries
   - MH service rate per 1,000 beneficiaries
   - Policy intensity (0–14), computed as the sum of 14 policy binaries

2. **Trends over time**
   - Time series for the selected state + telehealth type:
     - Telehealth rate
     - SUD rate
     - MH rate
     - Policy intensity (secondary axis, 0–14)

3. **State comparison map**
   - US choropleth by selected month and metric:
     - Telehealth rate, SUD rate, MH rate, or policy intensity

4. **Policy intensity wheel**
   - A 14-wedge policy “wheel” for the selected state + month
   - Each wedge encodes a policy feature (0/1); total intensity is displayed in the center

## Policy intensity index (0–14)

The dashboard computes **Policy_Intensity_Recalc** as the sum of these 14 binary features:

- Audio-Only Reimbursed
- Video-Only Reimbursed
- Audio-Video Reimbursed
- Store-and-Forward Reimbursed
- RPM Reimbursed
- All Modalities Reimbursed
- Telehealth Covers SUD
- Initial In-Person Visit Required
- Out-of-State Providers Allowed
- Payment Parity Law
- Home Allowed as Originating Site
- School Allowed as Originating Site
- Licensed Behavioral Health Providers Allowed
- Policy Permanent

### Time alignment rule (critical)
If a row includes **Policy Start Date**, then for any month **before** that start date, **all 14 policy flags are forced to 0** so that intensity reflects policy availability at that time.

## Data requirements

Input file (CSV) must include at minimum:

Required identifiers:
- `State`
- `TelehealthType`

Time fields (any one of these patterns):
- `YearMonth` (e.g., `201801` or `2018-01`)
OR
- `Year` and `Month`
OR
- `Date_y` or `Date_x` (parseable dates)

Rate fields (must exist):
- `TelehealthServiceRatePer1000Beneficiaries`
- `SUD_RatePer1000 Beneficiaries`
- `MH_RatePer1000Beneficiaries`

Policy fields (must exist; 0/1 expected but coerced to int):
- all 14 features listed above

Optional:
- `Policy Start Date` (used for time alignment)

## How to build / update the dashboard

1. Install Python dependencies:
   - numpy
   - pandas

2. Set the input CSV path in the script:
   - `INFILE = Path(r"...Merged_Telehealth_and_Policy_Data.csv")`

3. Run the script:
   - `python telehealth_policy_dashboard_v2.py`

4. The script writes:
   - `index.html` into the same folder as your CSV (or wherever `OUTFILE` points)

5. Copy `index.html` into the **repository root** (recommended), commit, and push.

## Publishing on GitHub Pages

1. Go to: **Settings → Pages**
2. Source: **Deploy from a branch**
3. Branch: `main`
4. Folder: `/ (root)`
5. Save

Your site will serve `index.html` automatically.

## Recommended repository structure

.
├── index.html
├── telehealth_policy_dashboard_v2.py
├── README.md
├── LICENSE (optional)
└── data/
    ├── README.md (document data sources/variables)
    └── sample_data.csv (optional; de-identified)

## Notes on privacy and reproducibility

- If your CSV includes any sensitive fields, do **not** commit the raw file to GitHub.
- Consider committing either:
  - a de-identified sample dataset, or
  - only aggregated outputs suitable for public release.

## Citation / attribution

If you use this dashboard in reports or briefs, cite the repository and note:
- “Policy intensity is computed as the sum of 14 binary policy features with time-alignment via Policy Start Date.”
