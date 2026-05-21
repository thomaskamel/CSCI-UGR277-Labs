# Confidence-Based Routing & Severity Gateway

## Routing Threshold Justification
Our pipeline uses a dynamic **Severity & Confidence Gateway** following our multi-model evaluation phase. 

* **High-Confidence Path (True):** Records with a computed `risk_score >= 0.8` or flagged with structural anomaly codes automatically pass to the Specialist escalation queue, moving to `status = "processed"`.
* **Low-Confidence/Human Triage Path (False):** Records returning ambiguous telemetry, mixed classifications, or borderline parameters ($0.5 \le \text{risk\_score} < 0.8$) are diverted to a manual investigation queue, marked as `status = "needs_review"`.

## Justification Metric
A threshold boundary of `0.8` ensures high operational accuracy while reducing alert fatigue. It filters out routine cross-border transactions or minor travel anomalies ($< 0.8$) into human review queues, protecting downstream case managers from being flooded with benign entries.
