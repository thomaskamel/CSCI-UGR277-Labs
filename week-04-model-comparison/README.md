# Week 4: Model Comparison
Tested 4 AI models on 5 Cybersecurity text samples to evaluate their suitability for the Alert Classifier component of our Capstone project.

## Models Tested
- **HF Sentiment:** distilbert-base-uncased-finetuned-sst-2-english
- **HF Zero-Shot:** facebook/bart-large-mnli
- **HF NER:** dslim/bert-large-NER
- **Groq LLM:** Llama 3 8B (llama-3.1-8b-instant)

## Finding
I recommend the **Zero-Shot (BART)** model for the Alert Classifier component because it consistently and accurately categorized technical logs into security-relevant buckets without the mapping complexities of an LLM.

See `report.md` for the full analysis of results and failure cases.

## Reflection
I was most surprised by the complete failure of the Sentiment model in a technical context. Even though a "brute force attack" is objectively a negative security event, the model assigned every record a positive sentiment score of 0.7481. This likely happened because the model was trained on general conversational text rather than technical logs, where words like "successful" or "completed" are common. This taught me that for a Cybersecurity capstone, using domain-specific classification (like Zero-Shot) is far more reliable than using a general-purpose model that doesn't understand the context of a "successful" breach.
