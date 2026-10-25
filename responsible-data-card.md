# Responsible Data Card

## Dataset purpose
This dataset may support an educational experiment that estimates whether a customer may churn, to explore whether a voluntary retention check-in could be useful. It must not make decisions about eligibility, price, service access, or penalties.

## Provenance and permission
The file was supplied as part of the assignment and is named `customer-churn-training.csv`. The actual source, collection process, consent, license, date range, and data owner are not specified in the provided materials. Verify these before any use beyond the classroom exercise. Do not assume permission for production use.

## Population and representation
The file contains 12 customer rows. The sample is far too small to represent a broad customer population reliably. Geography, demographics, acquisition channel, business sector, and sampling method are unknown. No demographic or other protected-group attributes are provided, so subgroup fairness cannot be meaningfully assessed from this file.

## Features and target
- `customer_id`: customer identifier; exclude from model input. IDs may encode ordering or other unintended information.
- `tenure_months`: customer tenure in months.
- `support_tickets`: ticket count; the time window and ticket definition are undocumented.
- `monthly_spend_inr`: monthly spending in Indian rupees.
- `last_login_days`: days since last login; snapshot date and measurement procedure are undocumented.
- `plan_type`: categorical subscription plan (Basic, Standard, Pro).
- `churned`: target label, where 1 indicates churn and 0 indicates no churn according to the file. Exact churn definition and label horizon require confirmation.

Potential leakage: if features are measured after churn or after the prediction cutoff, they may reveal the outcome. Define a prediction timestamp and only use features available before it. Do not include `customer_id` as a predictor.

## Quality checks
- Rows: 12; columns: 7 fields plus header (7 data columns: ID, four numeric features, plan type, target).
- Missing values: none visible in the supplied rows; rerun automated checks on the actual file.
- Duplicate IDs/rows: check programmatically.
- Class balance in the visible data: 5 churned (1) and 7 not churned (0).
- Outliers/ranges: values appear plausible for this small example, but units and allowed ranges need confirmation.
- Train/test separation: use a fixed seed for demonstration. For production evaluation, use a time-based split and ensure preprocessing is fitted on training data only.

## Risks and safeguards
- **Sampling bias:** tiny unknown sample may not reflect customers in general. Gather representative, time-stamped data.
- **Privacy:** customer records can be sensitive even without names. Restrict access, minimize retention, and do not publish raw row-level data publicly.
- **Misuse:** a churn score could be used to disadvantage customers. Limit use to supportive outreach; prohibit automated punitive decisions.
- **False positives:** unnecessary contact or discounts. Use a human-reviewed threshold and respectful opt-out.
- **False negatives:** customers needing help may not be contacted. Keep ordinary support available to everyone.
- **Proxy risks:** plan type, spend, login activity, and support tickets may correlate with socioeconomic circumstances or accessibility needs. Review feature necessity and disparate outcomes when suitable lawful data and sufficient sample sizes exist.
- **Leakage:** confirm features precede the label period and prediction timestamp.

## Intended evaluation
Compare a majority-class baseline with a simple model such as logistic regression. Report confusion matrix, precision, recall, F1, balanced accuracy, and class support. Because there are only 12 records, metrics are illustrative and highly uncertain. Assess calibration, threshold choice, and subgroup fairness only with adequate validation data. Review false positives and false negatives separately.

## Intended users and limitations
Intended users: students and reviewers evaluating a responsible ML workflow. Not suitable for production decisions, individual customer judgments, or claims about real-world churn performance.
