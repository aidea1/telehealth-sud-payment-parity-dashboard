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

For more details contact: Akshaya Bhagavathula, PhD | Associate Professor of Epidemiology | North Dakota State University | Fargo, ND| Email: akshaya.bhagavathula@ndsu.edu 
