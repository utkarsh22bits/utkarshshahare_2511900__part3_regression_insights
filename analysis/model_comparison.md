# Model Comparison

This file compares the two simple regression models against the final multiple
regression model, using `monthly_sales` as the dependent variable throughout.

## Model 1 – Simple Regression: marketing_spend

- **Model name:** Simple Regression 1 (marketing_spend)
- **Variables used:** Dependent = `monthly_sales`; Independent = `marketing_spend`
- **R-squared:** 0.167
- **Significant variables:** `marketing_spend` (p < 0.001) — statistically significant
- **Business usefulness:** Confirms marketing spend has a real, positive relationship
  with sales, but on its own it only explains about 17% of the variation in sales —
  not enough to rely on alone for planning.
- **Limitations:** Ignores every other factor (footfall, inventory, store type,
  region, etc.) that also affects sales, so the coefficient is likely picking up some
  of the effect of correlated variables like footfall.

## Model 2 – Simple Regression: footfall

- **Model name:** Simple Regression 2 (footfall)
- **Variables used:** Dependent = `monthly_sales`; Independent = `footfall`
- **R-squared:** 0.736
- **Significant variables:** `footfall` (p < 0.001) — statistically significant
- **Business usefulness:** Footfall alone explains nearly 74% of the variation in
  monthly sales, making it by far the single strongest individual predictor in the
  dataset. Useful as a quick, high-level indicator of expected sales.
- **Limitations:** Still a single-variable model — doesn't show how store type,
  region, marketing, or inventory availability layer on top of footfall, and footfall
  itself isn't always something leadership can directly control month to month.

## Model 3 – Multiple Regression (Final Model)

- **Model name:** Multiple Regression
- **Variables used:** Dependent = `monthly_sales`; Independent = `marketing_spend`,
  `footfall`, `avg_discount_pct`, `inventory_availability_pct`, region dummies
  (North/South/West vs. East), store_type dummies (High Street/Mall/Residential vs.
  Airport)
- **R-squared:** 0.828 (Adjusted R-squared: 0.822)
- **Significant variables:** `marketing_spend` (p < 0.001), `footfall` (p < 0.001),
  `inventory_availability_pct` (p < 0.001), `region_South` (p = 0.009),
  `region_West` (p = 0.004), `store_type_High Street` (p = 0.018),
  `store_type_Residential` (p < 0.001)
- **Business usefulness:** This is the most complete and reliable model. It explains
  about 83% of the variation in monthly sales and shows how multiple factors combine —
  not just footfall and marketing, but also inventory stocking and structural
  differences between store types/regions. This is the model leadership should use
  for planning.
- **Limitations:** `avg_discount_pct` and `region_North` were not statistically
  significant (p = 0.235 and p = 0.232 respectively), so no strong claim should be
  made about discounting driving sales based on this data. The model also doesn't
  capture causation — it's possible high-footfall stores get more marketing budget
  *because* they're already strong performers, not the other way around.

## Overall Model Comparison

| Model               | Independent Variables                                                             | R²    | Business Usefulness |
| ------------------- | --------------------------------------------------------------------------------- | ----- | ------------------- |
| Simple Regression 1 | Marketing Spend                                                                   | 0.167 | Low                 |
| Simple Regression 2 | Footfall                                                                          | 0.736 | High                |
| Multiple Regression | Marketing Spend, Footfall, Avg Discount %, Inventory Availability %, Region_North | 0.828 | Very High           |

## Overall Takeaway

Moving from a single-variable model to the multiple regression model nearly doubles
explanatory power (R² goes from 0.17–0.74 up to 0.83) and gives a much more
business-usable picture, since real store performance is driven by a combination of
factors rather than any single one.
