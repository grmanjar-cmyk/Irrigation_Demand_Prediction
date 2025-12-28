# 🚜 Pajaro Valley Irrigation Demand Model

**Status:** Demo (Proof of Concept)
**Region:** Pajaro Valley, Central California
**Objective:** Predict agricultural irrigation demand using local CIMIS weather data.

## 📖 Overview
This project explores the feasibility of using Machine Learning (Random Forest) to forecast water demand for an irrigation district. By analyzing historical delivery data against local weather patterns, we aim to provide a potential baseline for predictive planning.

The current prototype demonstrates that **Weather Data alone accounts for ~89% of the variance** in monthly water demand, validating the approach.

## 📂 Data Sources
*   **Water Deliveries:** Historical monthly delivery records (Recycled + Blend water) for 2021-2023 from publicly available PVWMA annual reports.
*   **Weather:** Monthly microclimate data from CIMIS Station #129 (Pajaro).

## ⚙️ Methodology
1.  **Data Integration:** Merged water delivery records with CIMIS weather station data.
2.  **Feature Selection:**
    *   **Net ET:** Calculated as `Total ETo - Total Precipitation` to represent the "Water Deficit."
    *   **Soil Temperature:** Acts as a proxy for the growing season/dormancy.
    *   **Solar Radiation:** Captures the intensity of atmospheric demand.
3.  **Modeling:** Trained a Random Forest Regressor on 70% of the data; tested on 30%. Validated against a "Kitchen Sink" model (all variables) to analyze potential overfitting.

## 📊 Key Results
*   **R² Score:** 0.89 (Model explains 89% of demand fluctuations).
*   **Feature Importance Discovery:**
    1.  **Soil Temp (~48%)** is the primary driver, identifying the "Seasonal Regime" (Wet/Dormant vs. Dry/Active).
    2.  **Atmospheric Demand (Net ET + Solar)** accounts for the remaining intensity adjustments.

## 🚀 Next Steps (Operational Roadmap)
To transition this from a study to an operational tool:

1.  **Daily Granularity:** Ingest daily SCADA flow meter data to capture short-term spikes.
2.  **System Inertia:** Add "Autoregressive Features" (e.g., Demand Yesterday, Demand Last Week).
    *   *Why?* Operational history is often a better predictor of immediate future behavior than weather alone.
3.  **Automation:** Connect to the CIMIS API for live daily inference.a

   ## 🛠️ Implementation Notes
*   **Language:** Python 3.10+
*   **Libraries:** Pandas, Scikit-Learn, Seaborn, Matplotlib
*   **Development Environment:** Google Colab
*   **AI Assistance:** Large Language Models (LLMs) were utilized for code generation, debugging, and documentation drafting. All hydrological logic, feature engineering choices, and model validation interpretations were verified by the human author to ensure physical accuracy.
