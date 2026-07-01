# utkarshshahare_2511900__part3_regression_insights

# Part 3 – Regression-Based Business Insights & Model Interpretation

## 1. Business Problem Summary

The leadership team at this retail chain wants to know what is actually driving monthly
sales across their stores. Before they commit budget to things like extra marketing
spend, better inventory availability, discounting, staffing changes, or opening more
stores of a particular type, they want evidence on which of these factors really move
the needle. This analysis uses regression to test that, and ends with a business
recommendation backed by the numbers.

## 2. Dataset Description

The dataset (`business_regression_data.xlsx`) contains 320 monthly records for 80 stores
(4 months of data per store, Jan–Apr 2025). Each row represents one store-month and
includes operational metrics (marketing spend, footfall, discounting, staffing,
inventory availability, competitor distance, customer rating) along with the sales and
profit outcome for that month.

Two columns had a small number of missing values:
- `competitor_distance_km` – 6 missing values
- `customer_rating` – 8 missing values

Both were filled with the column median rather than dropping rows, since the missing
count was small (under 2% of records) and dropping them would have removed otherwise
complete data unnecessarily.

## 3. Dependent and Independent Variables

**Dependent variable:** `monthly_sales`

**Independent variables considered:**

| Variable | Type | Notes |
|---|---|---|
| marketing_spend | Numerical | Monthly marketing budget spent by the store |
| footfall | Numerical | Number of customers visiting the store |
| avg_discount_pct | Numerical | Average discount offered that month |
| staff_count | Numerical | Number of staff at the store |
| inventory_availability_pct | Numerical | % of catalog in stock |
| competitor_distance_km | Numerical | Distance to nearest competitor |
| holiday_flag | Numerical (binary, 0/1) | Whether the month included a major holiday |
| customer_rating | Numerical | Average customer rating |
| region | Categorical | East / North / South / West |
| store_type | Categorical | High Street / Mall / Residential / Airport |

**Variables that needed cleaning/transformation:** `competitor_distance_km` and
`customer_rating` (missing value imputation); `region` and `store_type` needed to be
converted into dummy variables since regression cannot use text categories directly.

**Variables that may not be useful for regression:** `store_id` and `month` are
identifiers/timestamps, not predictors — they don't represent a measurable business
factor leadership can act on, so they were excluded from the regression itself
(though `month` is useful for sorting/context). `monthly_profit` was also left out of
the predictor set since it's really another outcome variable (closely tied to sales),
not a driver of sales — including it would be circular.

## 4. Regression Approach

Two simple linear regressions were run first (one independent variable at a time)
to get a baseline read on individual factors, followed by one multiple regression
model combining the strongest numerical predictors with the categorical dummy
variables. This mirrors how you'd normally explore a dataset — start simple, then
build up to a fuller model once you know which variables matter.

## 5. Dummy Variable Approach

`region` and `store_type` are both categorical, so each was converted into dummy
(0/1) columns, dropping one category from each as the reference group to avoid the
dummy variable trap (perfect multicollinearity if all categories are included
alongside an intercept):

- `region` → `region_North`, `region_South`, `region_West` (reference = **East**)
- `store_type` → `store_type_High Street`, `store_type_Mall`, `store_type_Residential`
  (reference = **Airport**)

Full detail is in `outputs/model_equations.md`.

## 6. Model Comparison Summary

The multiple regression model substantially outperforms either simple model
(R² ≈ 0.83 vs ≈ 0.17–0.74 for the simple models), because it accounts for footfall,
marketing spend, inventory availability, and store/region differences together
instead of in isolation. Full comparison is in `analysis/model_comparison.md`.

## 7. Final Model Selected

The multiple regression model (`monthly_sales ~ marketing_spend + footfall +
avg_discount_pct + inventory_availability_pct + region dummies + store_type dummies`)
was selected as the final model, since it captures the combined effect of operational
factors and store characteristics rather than looking at one variable at a time.

## 8. Business Recommendation

See `outputs/final_recommendation.md` for the full write-up. In short: footfall and
marketing spend are the strongest, most reliable levers on sales, and inventory
availability also has a real (smaller) positive effect. Store type and region matter
too — Residential and High Street stores underperform Airport stores of similar size,
holding other factors constant.

## 9. Assumptions and Limitations

- This is observational, cross-sectional-ish data (4 months per store) — regression
  shows association, not proof of causation.
- Only 4 months of data per store means seasonal effects can't really be separated
  out from store-level effects.
- `avg_discount_pct` was not statistically significant in the final model, so no
  strong conclusion is drawn about discounting's effect on sales from this dataset.
- Multicollinearity between some predictors (e.g., footfall and marketing spend) may
  slightly affect individual coefficient stability, though overall model fit remains
  strong.

## 10. Screenshots Included

- `screenshots/simple_regression_output.png` – simple regression output
- `screenshots/multiple_regression_output.png` – multiple regression output
- `screenshots/residuals_preview.png` – predicted values and residuals
- `screenshots/model_comparison_preview.png` – model comparison table
