# Custom Model Confusion Matrix

This confusion matrix summarizes the classification results of the 10 held-out test images evaluated on our Google Teachable Machine image model.

## Confusion Matrix Data

| | Predicted: Phishing | Predicted: Legitimate |
|---|---|---|
| **Actual: Phishing** | True Positives (TP) = 3 | False Negatives (FN) = 2 |
| **Actual: Legitimate** | False Positives (FP) = 3 | True Negatives (TN) = 2 |

## Performance Metrics

- **Accuracy**: 50%
- **Precision**: 50%
- **Recall**: 60%
- **F1 Score**: 54.55%

## Analysis of Errors

1. **False Positives (FP = 3)**: The model incorrectly flagged 3 legitimate email screenshots as phishing attacks.
2. **False Negatives (FN = 2)**: The model missed 2 actual phishing screenshots, misclassifying them as safe. 

In our threat classification pipeline, minimizing false negatives is the highest priority to ensure that zero malicious emails bypass initial automated filters.
