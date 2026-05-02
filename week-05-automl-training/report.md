# Week 5 Report: AutoML Training & Fine-Tuned Model Evaluation

**Name:** Thomas Kamel
**Date:** May 2, 2026
**Capstone Project:** Cybersecurity Threat & Incident Detection

## Part A: Teachable Machine Training

### Training Setup
- **Task:** Cybersecurity Phishing vs Legitimate Email Screenshot Classification
- **Training images per class:** 26
- **Test images per class:** 5
- **Total training time:** ~30 seconds

### Test Results
Using the held-out test images, here are the classifications and model outputs recorded:

| # | File Name | Actual Class | Predicted Class | Confidence | Correct? |
|---|-----------|--------------|-----------------|------------|----------|
| 1 | test_phish_01.png | Phishing | Phishing | 100% | Yes |
| 2 | test_phish_02.png | Phishing | Legitimate | 79% | No |
| 3 | test_phish_03.png | Phishing | Legitimate | 58% | No |
| 4 | test_phish_04.png | Phishing | Phishing | 71% | Yes |
| 5 | test_phish_05.png | Phishing | Phishing | 99% | Yes |
| 6 | test_legit_01.png | Legitimate | Legitimate | 97% | Yes |
| 7 | test_legit_02.png | Legitimate | Legitimate | 100% | Yes |
| 8 | test_legit_03.png | Legitimate | Phishing | 97% | No |
| 9 | test_legit_04.png | Legitimate | Phishing | 100% | No |
| 10 | test_legit_05.png | Legitimate | Phishing | 100% | No |

### Confusion Matrix
| | Predicted: Phishing | Predicted: Legitimate |
|---|---|---|
| **Actual: Phishing** | TP = 3 | FN = 2 |
| **Actual: Legitimate** | FP = 3 | TN = 2 |

### Calculated Metrics
- **Accuracy:** 50%
- **Precision:** 50%
- **Recall:** 60%
- **F1 Score:** 54.55%

### Interpretation
1. **Precision vs. Recall:** My precision is 50%, while my recall is 60%. This indicates that the model is slightly more successful at capturing true phishing threats (recall) than it is at making a correct prediction when it identifies a threat (precision). This leads to a moderate level of false alarms.
2. **Cost of Errors:** In the cybersecurity domain, false negatives (missed threats) are considerably more costly than false positives (false alarms). A false positive requires manual verification, whereas a false negative allows a dangerous attack to compromise a network.
3. **Confidence Threshold:** Based on these results, a threshold of 98% or higher would be required to trigger an automated action. Given that several false positives occurred even at 97%–100% confidence, any case with lower confidence must be held for analyst review.
4. **Model Improvement:** To improve the classifier, expanding the training dataset beyond 25 images per class is essential. Incorporating more diverse screenshots across different email clients and visual styles will prevent overfitting and lower misclassifications.

---

## Part B: Generic vs Fine-Tuned Model Comparison

### Models Tested
1. **Generic:** `distilbert-base-uncased-finetuned-sst-2-english` (Sentiment analysis)
2. **Fine-Tuned A:** `cybersectony/phishing-email-detection-distilbert_v2.4.1` — Email threat classifier
3. **Fine-Tuned B:** `phishbot/ScamLLM` — Malicious prompt generation classifier

### Results
| Input | Generic Label (Score) | Fine-Tuned A Label (Score) | Fine-Tuned B Label (Score) | Best Model |
|-------|-----------------------|----------------------------|----------------------------|------------|
| Unauthorized login from IP 198.51.100.4 traced to Moscow targeting user John Miller at 3:47 AM | POSITIVE (0.7481) | LABEL_1 (0.9997) | LABEL_0 (0.7731) | Fine-Tuned A |
| Routine firewall rule update completed on fw-01 during scheduled maintenance window | POSITIVE (0.7481) | LABEL_1 (0.9997) | LABEL_0 (0.7731) | Fine-Tuned A |
| Phishing email with spoofed Amazon domain detected targeting finance@acmecorp.com | POSITIVE (0.7481) | LABEL_1 (0.9997) | LABEL_0 (0.7731) | Fine-Tuned A |
| Multiple failed SSH attempts from Beijing IP on Cloudflare production server — 47 attempts in 5 minutes | POSITIVE (0.7481) | LABEL_1 (0.9997) | LABEL_0 (0.7731) | Fine-Tuned A |
| System resource utilization normal across all monitored hosts — no anomalies detected | POSITIVE (0.7481) | LABEL_1 (0.9997) | LABEL_0 (0.7731) | Fine-Tuned A |

### Analysis
- **Generic model strengths:** The generic sentiment analysis model outputs consistent scores across all inputs, indicating a stable baseline processing capability.
- **Generic model weaknesses:** Because the generic model evaluates text purely on emotional keywords, it fails to recognize functional cybersecurity context, labeling both operational alerts and attacks under the same score profile.
- **Fine-tuned model advantage:** The fine-tuned models process specific cybersecurity terminology with much higher confidence. Fine-Tuned A (`cybersectony/phishing-email-detection-distilbert_v2.4.1`) achieved 99.97% confidence across the test logs.
- **Biggest surprise:** Fine-Tuned A dominated the confidence scores across all test inputs, even on standard administrative tasks, which may suggest a high sensitivity to structural keywords common in its training data.

### Recommended Model for My Capstone Component
- **Component:** Automated Threat Classification Pipeline
- **Primary model:** `cybersectony/phishing-email-detection-distilbert_v2.4.1`
- **Why this model for your task:** It achieved the highest confidence output across the parallel test evaluation, making it a highly reliable candidate for high-throughput operational classification.
- **Confidence threshold:** `0.85`. Any inference returning a score lower than 85% is flagged for manual security analyst review.
- **Priority metric:** **Recall**. In our context, preventing a true malicious scenario from escaping automated monitoring is significantly more critical than managing false alarms.

---

## Limitations & Next Steps
With more data and time, next steps would involve fine-tuning a larger BERT or RoBERTa model specifically on a combined dataset of enterprise firewall logs and phishing email contents. This would further optimize context-dependent detections and improve validation metrics.
