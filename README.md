# 🚜 Pajaro Valley Irrigation Demand Model

**Status:** Demo (Proof of Concept)  
**Region:** Pajaro Valley, Central California  
**Objective:** Predict agricultural irrigation demand using local CIMIS weather data.

---

## 📖 Overview
This project explores the feasibility of using Machine Learning (Random Forest) to forecast water demand for an irrigation district. By analyzing historical delivery data against local weather patterns, we aim to provide a potential baseline for predictive planning.

The current prototype demonstrates that **Weather Data alone accounts for ~72% of the variance** in monthly water demand, validating the approach.

## 📂 Data Sources
*   **Water Deliveries:** Historical monthly delivery records (Recycled + Blend water) for 2021-2023 from publicly available PVWMA annual reports.
*   **Weather:** Monthly microclimate data from **CIMIS Station #129 (Pajaro)**.

## ⚙️ Methodology
1.  **Data Integration:** Created water delivery table from annual report graphics and merged with downloaded CIMIS weather station data.
2.  **Feature Engineering:** Selected key drivers based on initial correlation matrix of weather data to total delivered water:
    *   `Total ETo` (Evapotranspiration)
    *   `Total Precipitation`
    *   `Solar Radiation`
    *   `Soil Temperature`
    *   *Excluded:* Recycled/Blend splits to prevent target leakage.
3.  **Modeling:** Trained a **Random Forest Regressor** (Scikit-Learn) on 70% of the data; tested on 30%.

## 📊 Results (Prototype)
*   **R² Score:** `0.72` (Model explains 72% of demand fluctuations).
*   **Key Insight:** Total Precipiation and Soil Temp were the strongest predictors.

## 🚀 Next Steps (Operational Roadmap)
To transition this from a study to an operational tool:
1.  **Daily Granularity:** Ingest daily SCADA flow meter data to capture short-term spikes.
2.  **System Inertia:** Add "Autoregressive Features" (e.g., *Demand Yesterday*, *Demand Last Week*).
    *   *Why?* Operational history may be a better predictor of immediate future behavior. Combining **System State** with **Weather Forecasts** may boost accuracy.
3.  **Automation:** For real time prediction would need ability to connect to the CIMIS API for live daily inference.

---
*Author: grmanjar-cmyk*
