# Risk Register: Customer Churn Baseline

| Risk | Likelihood | Impact | Mitigation / safeguard | Owner / status |
|---|---|---|---|---|
| Dataset too small (12 rows) | High | High | Treat all metrics as a demonstration; collect a much larger sample before any deployment. | Project owner — open |
| Unknown provenance, consent, or license | Medium/Unknown | High | Confirm data owner, source, lawful basis/consent, and permitted use before sharing or deployment. | Data owner — open |
| Churn label is ambiguous | High | High | Define churn event, label horizon, and snapshot date in writing. | Business owner — open |
| Temporal/data leakage | Medium | High | Ensure every feature was available before prediction time; use a temporal holdout for real evaluation. | ML developer — open |
| False negative | Medium | Medium/High | Keep normal support available; monitor recall and review missed churn cases. | Customer success — open |
| False positive | Medium | Medium | Human-review outreach, use respectful messaging, allow opt-out, and monitor unnecessary contacts. | Customer success — open |
| Proxy bias from spend, plan, usage, or support history | Medium | High | Review feature necessity and subgroup outcomes when data and lawful basis permit; do not use for punitive decisions. | Responsible AI reviewer — open |
| Privacy exposure | Medium | High | Minimize access and retention; remove IDs from public outputs; do not publish row-level customer data. | Data owner — open |
| Poor calibration / unstable threshold | High | Medium | Do not rely on probabilities from 12 rows; validate on larger independent data before threshold selection. | ML developer — open |
| Model or pipeline unavailable | Low/Medium | Medium | Fall back to normal support process and documented non-ML baseline; do not block customer service. | Operations — open |
