# Model Equations

## 1. Simple Regression Equations

**Simple Model 1 — monthly_sales vs marketing_spend**

monthly_sales = 560,777.35 + 2.1296 × marketing_spend

**Simple Model 2 — monthly_sales vs footfall**

monthly_sales = 446,410.58 + 35.6780 × footfall

## 2. Multiple Regression Equation (Final Model)

monthly_sales = 152,070.64
  + 1.1798 × marketing_spend
  + 33.8479 × footfall
  − 43,853.50 × avg_discount_pct
  + 2,916.36 × inventory_availability_pct
  + 8,466.88 × region_North
  + 18,874.81 × region_South
  + 18,571.88 × region_West
  − 22,299.88 × store_type_High Street
  − 10,264.68 × store_type_Mall
  − 38,855.22 × store_type_Residential

## 3. Explanation of Each Coefficient

- **Intercept (152,070.64):** The baseline predicted monthly sales when all numeric
  predictors are 0 and the store is in the reference categories (East region,
  Airport store type). Not very meaningful on its own since marketing_spend and
  footfall are never actually 0 in practice — it's mainly there to anchor the line.

- **marketing_spend (+1.1798):** For every additional ₹1 spent on marketing in a
  month, predicted sales increase by about ₹1.18, holding all other factors
  constant. Statistically significant (p < 0.001).

- **footfall (+33.8479):** Each additional customer visiting the store is
  associated with about ₹33.85 more in monthly sales, holding other factors
  constant. This is the strongest individual driver in the model and is highly
  significant (p < 0.001).

- **avg_discount_pct (−43,853.50):** Suggests higher average discounting is
  associated with lower sales, but this is **not statistically significant**
  (p = 0.235), so this relationship should not be relied on — it could easily be
  noise rather than a real effect.

- **inventory_availability_pct (+2,916.36):** For each 1 percentage point increase
  in inventory availability, predicted sales increase by about ₹2,916, holding
  other factors constant. Statistically significant (p < 0.001) and a meaningful,
  actionable lever for leadership.

- **region_North (+8,466.88):** North region stores sell about ₹8,467 more per
  month than East region stores (the reference), holding other factors constant —
  but this is **not statistically significant** (p = 0.232), so it shouldn't be
  treated as a confirmed regional effect.

- **region_South (+18,874.81):** South region stores sell about ₹18,875 more per
  month than East region stores, holding other factors constant. Statistically
  significant (p = 0.009).

- **region_West (+18,571.88):** West region stores sell about ₹18,572 more per
  month than East region stores, holding other factors constant. Statistically
  significant (p = 0.004).

- **store_type_High Street (−22,299.88):** High Street stores sell about ₹22,300
  less per month than Airport stores (the reference), holding other factors
  constant. Statistically significant (p = 0.018).

- **store_type_Mall (−10,264.68):** Mall stores sell about ₹10,265 less per month
  than Airport stores, holding other factors constant — but this is **not
  statistically significant** (p = 0.293).

- **store_type_Residential (−38,855.22):** Residential stores sell about ₹38,855
  less per month than Airport stores, holding other factors constant. This is the
  largest store-type effect in the model and is highly significant (p < 0.001).

## 4. Explanation of Dummy Variables

Two categorical variables — `region` and `store_type` — were converted into dummy
(0/1) columns since regression requires numeric inputs. For each, one category was
dropped and used as the reference group, so the dummy coefficients represent the
difference from that baseline rather than an absolute value. Including all
categories alongside the intercept would create perfect multicollinearity (the
"dummy variable trap"), which is why one category was always left out.

- `region` → dummies for North, South, West (3 dummies for 4 categories)
- `store_type` → dummies for High Street, Mall, Residential (3 dummies for 4
  categories)

## 5. Reference Category Used

- **region:** East
- **store_type:** Airport

All region and store_type coefficients in the model should be read as "compared to
East" and "compared to Airport" respectively.

## 6. Final Model Selected

The **multiple regression model** (Model 3) was selected as the final model:

monthly_sales ~ marketing_spend + footfall + avg_discount_pct +
inventory_availability_pct + region (dummy) + store_type (dummy)

## 7. Reason for Selecting the Final Model

The multiple regression model was chosen over either simple regression because it
explains far more of the variation in sales (R² = 0.828 vs. 0.167 for
marketing_spend alone and 0.736 for footfall alone) and because it isolates the
effect of each factor while controlling for the others. The simple models risk
overstating a single variable's importance since they ignore everything else going
on — for example, marketing_spend on its own looks weaker than it really is partly
because it's correlated with footfall, and the simple footfall model can't say
anything about how store type or region also affect sales. The multiple regression
model gives leadership a single, more trustworthy picture that separates real,
statistically significant drivers (footfall, marketing spend, inventory
availability, region, store type) from ones that don't hold up (avg_discount_pct,
region_North, store_type_Mall).
