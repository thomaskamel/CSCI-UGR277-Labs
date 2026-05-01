# Model Comparison Report — Week 4
**Name:** Thomas Kamel
**Date:** April 30, 2026
**Capstone Project:** [Insert Your Project Name]
**My Component:** Cybersecurity Alert Classifier

## Test Setup
**Input dataset:** 5 Cybersecurity text samples covering:
- 2 clearly concerning/high-severity records (Unauthorized login, SSH brute force)
- 1 ambiguous/edge case record (Phishing email)
- 2 routine/benign records (Firewall update, Resource utilization)

**Models tested:**
1. distilbert-base-uncased-finetuned-sst-2-english (sentiment)
2. facebook/bart-large-mnli (zero-shot classification)
3. dslim/bert-large-NER (named entity recognition)
4. Groq Llama 3 8B (LLM classification)

## Results Summary
| Record | Sentiment | Zero-Shot | NER Entities | Groq |
| :--- | :--- | :--- | :--- | :--- |
| 1. Unauthorized login | POSITIVE (0.7481) | possible anomaly | None | Error: Missing Data |
| 2. Routine update | POSITIVE (0.7481) | routine activity | None | Error: Missing Data |
| 3. Phishing email | POSITIVE (0.7481) | possible anomaly | None | Error: Missing Data |
| 4. SSH attempts | POSITIVE (0.7481) | possible anomaly | "SS" (MISC) | Error: Missing Data |
| 5. System normal | POSITIVE (0.7481) | routine activity | None | Error: Missing Data |

## Analysis
**Where models agreed:** The Zero-Shot model correctly distinguished between "routine activity" and "possible anomaly" for all 5 records, effectively identifying which events required further investigation.
**Where models disagreed:** The Sentiment model was ineffective for this domain, labeling critical security threats (like unauthorized logins) as "POSITIVE" with a 0.7481 score. This confirms that sentiment analysis alone cannot determine the severity of a technical security log.
**Most accurate model overall:** The **Zero-Shot (BART)** model provided the most reliable results, as it successfully categorized the threats and routine tasks into the specific cybersecurity labels provided.
**Fastest/most practical:** Zero-Shot is the most practical here because it returns a single, structured category name that can be used to trigger different automated workflows in n8n.

## Recommended Models for My Capstone Component
**Component:** Cybersecurity Alert Classifier
**Primary model:** **facebook/bart-large-mnli (Zero-Shot)** — This model successfully categorized logs into security-relevant buckets without the overhead of a large language model.
**Secondary model:** **dslim/bert-large-NER** — This could be useful for identifying protocols (like "SS" for SSH), though it requires more tuning for technical strings.
**Rejected models and why:**
- **distilbert-sentiment:** Rejected because it cannot distinguish between a "Successful Breach" and a "Successful Update," labeling both as positive.

## Failure Cases and Limitations
A major failure occurred with the **Groq LLM** node, which consistently requested the alert details instead of classifying them. This indicates a technical limitation in the n8n JSON mapping where the input text was not successfully passed to the model. Furthermore, the **NER** model failed to identify IP addresses, which are the most critical entities in a cybersecurity forensic context.

## Next Steps
If I had more time, I would troubleshoot the JSON mapping in n8n to ensure the Groq LLM receives the input text. I would also test specialized cybersecurity models on Hugging Face that are trained specifically to extract IP addresses, port numbers, and CVE codes from raw logs.
