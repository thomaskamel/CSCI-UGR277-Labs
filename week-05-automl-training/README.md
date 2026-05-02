# Week 5: AutoML & No-Code Model Training

Trained a custom image classifier with Google Teachable Machine and compared generic vs fine-tuned Hugging Face models for the **Automated Threat Classification Pipeline** component of our capstone project.

## Custom Model Training
- Built a **Phishing vs Legitimate** email screenshot classifier with Google Teachable Machine.
- Achieved **50%** accuracy on 10 held-out test images.
- Precision: **50%** | Recall: **60%** | F1 Score: **54.55%**

## Fine-Tuned Model Comparison
Compared 3 models (1 generic + 2 fine-tuned) on 5 test inputs:
- **Generic:** `distilbert-base-uncased-finetuned-sst-2-english` (Sentiment analysis)
- **Fine-Tuned A:** `cybersectony/phishing-email-detection-distilbert_v2.4.1`
- **Fine-Tuned B:** `phishbot/ScamLLM`

## Findings
I recommend **cybersectony/phishing-email-detection-distilbert_v2.4.1** for the **Automated Threat Classification Pipeline** component because it demonstrated highly reliable performance on technical administrative and log data without misinterpreting routine system actions as threats. 

Fine-tuned models showed higher overall performance with more relevant labels, better handling of technical edge cases, and significantly higher confidence scores than the generic sentiment baseline.

See `report.md` for the full training and metrics analysis.
