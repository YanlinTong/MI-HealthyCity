# Coronary Heart Disease (CHD) – Census-Tract-Level Analysis

This folder documents our analysis of **coronary heart disease (CHD) prevalence** across Michigan cities using indicators from the MI-HealthyCity project. We here summarize the indicators, demographic measures, visualization, and the **piecewise spatial linear model** that quantifies associations between CHD prevalence and social/environmental determinants while adjusting for demographics.

> MI-HealthyCity overview: https://sph.umich.edu/ideas/mi-healthycity-tool.html

---

## Data: Indicators & Demographics

- **Indicators:** 9 indicators spanning 6 domains, including:
  - Uninsured rate (%)
  - Homeownership rate (%)
  - Green space proportion (%)
  - PM2.5 concentration (µg/m³)
  - Transit cost proportion (%)
  - Vacant housing rate (%)
  - Unemployment rate (%)
  - High school graduate proportion (%)

- **Demographics:**
  - Population density
  - Black population proportion (%)
  - Population aged 18 to 64 proportion (%)
  - Female population proportion (%)

- **Outcome:** CHD prevalence (%).

---

## Methods

1. **Spatial visualization**
   - We mapped the geographic distribution of selected indicators via interactive heatmaps to contextualize spatial patterns across MI census tracts. Darker shades indicate higher values.

2. **City-level summaries**
   - For CHD prevalence, we use **boxplots** to display the distribution across **24 MI cities** (median, IQR, whiskers, and outliers defined as >1.5×IQR beyond Q3 or below Q1).

3. **Piecewise spatial linear regression**
   - We built a **piecewise spatial linear regression** that accounts for cross-city spatial dependence.
   - **Uninsured rate breakpoint:** Visual inspection of partial effects suggested a slope change around **8%**; we therefore used **8%** as the **piecewise knot** (two linear segments: \<8% and ≥8%).

---

## Results

### Boxplot of CHD prevalence (%) by city
Each box shows the **IQR** for city-specific CHD prevalence across tracts; the **horizontal line** denotes the median; **dots** are outliers (>1.5×IQR beyond Q3 or below Q1); **whiskers** extend to the most extreme non-outlier values.

![Boxplot of CHD prevalence by city](images/boxplot_coronary_heart_disease.png)

- **City distributions (Figure 1 & Table 2):**
  - The **highest median** CHD prevalence: **Flint**, followed by **Detroit** and **Dearborn**.  
  - The **lowest median**: **Ann Arbor**, followed by **Novi** and **Canton Charter Township**.  
  - **Largest IQRs:** **Detroit** and **Kalamazoo** (≈2.5%).  
  - **Smallest IQR:** **Livonia** (≈1.1%), indicating tighter clustering around the median.

---

## Results (Highlights)


- **Piecewise spatial linear regression (Table 3; outcome = CHD %, adjusted for demographics):**
  - **Health care domain – Uninsured rate**  
    - **\< 8% uninsured:** +1% uninsured → **+0.031%** CHD (95% CI: −0.009%, 0.071%; *p* = 0.132; not significant).  
    - **≥ 8% uninsured:** +1% uninsured → **−0.059%** CHD (95% CI: 0.021%, 0.098%; *p* = 0.002; significant decrease).
  - **Neighborhood & environmental exposures:**  
    - **Transportation cost (% income):** +1% → **−0.115%** CHD (95% CI: 0.051%, 0.179%; *p* \< 0.001).  
    - **Vacant housing rate:** +1% → **+0.013%** CHD (95% CI: 0.003%, 0.024%; *p* = 0.013).  
    - Other indicators in this domain showed no statistically significant associations.
  - **Income & employment:**  
    - **Unemployment rate:** +1% → **+0.048%** CHD (95% CI: 0.035%, 0.062%; *p* \< 0.001).
  - **Human development:**  
    - **High school graduates (%):** +1% → **−0.049%** CHD (95% CI: 0.037%, 0.062%; *p* \< 0.001).

> **Interpretation note:** Coefficients represent the absolute percentage-point change in **CHD prevalence (%)** per one-unit change in the predictor (in the units defined above), holding other variables constant. PM2.5 effects are relative to the **reference group** (**PM2.5 > 9.66 µg/m³**).

---

## Model Results Table

**Table 3. Spatial piecewise linear regression results**  
*Outcome:* CHD prevalence (%)  
*Predictors:* All indicators (including PM2.5 quartile groups), with **PM2.5 > 9.66 µg/m³** as the reference group; adjusted for demographics.

![Spatial piecewise linear regression table](images/model_coronary_heart_disease.png)

*File:* `images/table_piecewise_spatial_linear_model.png`

---

## Reproducibility (Optional)

If you wish to reproduce figures:
