# Residual Analysis

This analysis uses the final multiple regression model
(`monthly_sales ~ marketing_spend + footfall + avg_discount_pct +
inventory_availability_pct + region dummies + store_type dummies`) to calculate
predicted sales for every store-month record, then looks at where the model is
furthest off.

Residual = Actual `monthly_sales` − Predicted `monthly_sales`.
A positive residual means the model **under-predicted** actual sales; a negative
residual means the model **over-predicted** actual sales.

## 5 Records with the Largest Positive Residuals (Under-Predicted)

| Store ID | Month | Region | Store Type | Actual Sales | Predicted Sales | Residual |
|---|---|---|---|---|---|---|
| STR-1073 | 2025-03 | East | Residential | 813,316.71 | 702,328.37 | +110,988.34 |
| STR-1028 | 2025-04 | East | Mall | 713,611.16 | 606,503.36 | +107,107.80 |
| STR-1026 | 2025-04 | East | Mall | 625,514.04 | 526,670.87 | +98,843.17 |
| STR-1050 | 2025-04 | North | Residential | 735,786.64 | 636,997.20 | +98,789.44 |
| STR-1019 | 2025-03 | East | Residential | 788,087.68 | 690,046.76 | +98,040.92 |

## 5 Records with the Largest Negative Residuals (Over-Predicted)

| Store ID | Month | Region | Store Type | Actual Sales | Predicted Sales | Residual |
|---|---|---|---|---|---|---|
| STR-1017 | 2025-03 | West | High Street | 685,379.08 | 852,087.69 | −166,708.61 |
| STR-1023 | 2025-02 | South | Mall | 627,171.90 | 763,598.54 | −136,426.64 |
| STR-1012 | 2025-01 | West | Residential | 595,467.60 | 724,344.94 | −128,877.34 |
| STR-1007 | 2025-02 | West | Mall | 800,451.94 | 911,200.54 | −110,748.60 |
| STR-1014 | 2025-01 | West | High Street | 463,534.25 | 563,910.32 | −100,376.07 |

## Business Interpretation of Residuals

- **Under-predicted stores (positive residuals):** These stores outperform expectations based on marketing spend, footfall, inventory, and store type, suggesting unmodeled factors such as strong management, local events, reduced competition, or higher brand loyalty. *Example:* **STR-1073** and **STR-1019** (East-region Residential stores).
- **Over-predicted stores (negative residuals):** These stores underperform relative to model expectations, likely due to factors not captured by the data, such as increased competition, operational issues, or temporary slowdowns. *Example:* **STR-1017**, with the largest error (≈ **₹166,000** over-predicted).

## Are Certain Store Types Being Under- or Over-Predicted?

- **No systematic bias:** Mean residuals are close to zero across all store types, indicating no consistent over- or under-prediction.
- **Higher prediction variability:** Mall and Residential stores have the largest residual spread (SD ≈ **₹46,000** and **₹45,600**), compared to Airport and High Street stores (≈ **₹40,000**).
- **Largest errors:** Most extreme prediction errors (positive and negative) occur in Mall and Residential stores, with West-region stores overrepresented among over-predicted cases.
- **Insight:** Mall/Residential stores and the West region likely have store-specific or local-market factors not captured by the current predictors.
