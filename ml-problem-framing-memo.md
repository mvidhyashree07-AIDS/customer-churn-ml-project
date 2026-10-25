# ML Problem-Framing Memo: Customer Churn

## 1. Decision to support
Help a customer-success team decide which customers may benefit from a voluntary, helpful retention check-in or service-support offer.

## 2. Prediction target
`churned`: 1 = churned, 0 = did not churn, as labelled in the supplied training file. Before deployment, confirm the exact business definition of churn and the time period represented by this label.

## 3. Unit of observation
One row per customer (`customer_id`). Confirm that customer IDs are unique and that each row represents one customer at a single, well-defined snapshot date.

## 4. Prediction time and action window
Proposed: score customers at a fixed monthly snapshot using only information available before that snapshot; use the score to prioritize a human-reviewed, non-punitive outreach during the following 30 days. This is a proposed design, not a fact established by the file. The dataset does not provide snapshot dates or label horizons, so these must be clarified before a real evaluation.

## 5. Candidate inputs
- `tenure_months`: customer tenure in months.
- `support_tickets`: number of support tickets; its counting window must be documented.
- `monthly_spend_inr`: monthly spend in INR.
- `last_login_days`: days since last login at the snapshot.
- `plan_type`: Basic, Standard, or Pro plan.
- `customer_id`: identifier; exclude from model features.

## 6. Non-ML baseline
Use a majority-class predictor and a simple transparent rule-based benchmark (for example, flag customers with high recency of login or many support tickets). Define the rule using training data only and compare it against the model. A majority baseline is especially important because the dataset is tiny.

## 7. Metrics and error costs
Report confusion matrix, precision, recall, F1, balanced accuracy, and the positive-class support. Also inspect probability calibration only when there is enough validation data. False negative: a customer at risk is not contacted and may churn. False positive: a customer is contacted unnecessarily, creating annoyance or wasting outreach capacity. Agree with business owners on relative costs before choosing a threshold.

## 8. Split and validation
The file has only 12 rows, so any holdout estimate will be highly unstable. Use a fixed random seed and stratified split for a classroom demonstration, but do not claim generalization from this result. For real use, collect substantially more time-stamped data and use a temporal holdout that prevents future information leaking into training.

## 9. Human oversight and fallback
Do not automatically cancel, price, restrict, or deprioritize services based on a score. If the model or data pipeline is unavailable, use the documented non-ML baseline and normal customer-support process. A human should review outreach decisions.

## 10. Go/no-go recommendation
**No-go for production.** Proceed only as an educational baseline. Reconsider after confirming label definition, data provenance and permissions, snapshot/label timing, representative sampling, sufficient sample size, fairness checks, and operational monitoring.
