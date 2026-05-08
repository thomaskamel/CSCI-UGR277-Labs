# Week 7: RAG Security Knowledge Assistant

## 1. Setup Summary
* [cite_start]**LLM:** llama-3.3-70b-versatile via Groq [cite: 55, 244]
* [cite_start]**Embeddings:** sentence-transformers/all-MiniLM-L6-v2 via HuggingFace [cite: 146, 245]
* [cite_start]**Vector Store:** In-Memory Vector Store [cite: 156, 245]
* [cite_start]**Documents Loaded:** 3 MITRE ATT&CK technique text files [cite: 74, 80]

## 2. Test Results

| # | Question | Used Documents? | Quality | Notes |
| :--- | :--- | :--- | :--- | :--- |
| 1 | What are common techniques for credential access? | Yes | Good | [cite_start]Accurately cited techniques from the uploaded text[cite: 185]. |
| 2 | How does phishing relate to initial access? | Yes | Good | [cite_start]Correctly identified the link between the two[cite: 204]. |
| 3 | What is lateral movement and what techniques are used? | Yes | Good | [cite_start]Listed specific techniques directly from sources[cite: 185]. |
| 4 | What does the NIST framework recommend for "Detect"? | Yes | Partial | [cite_start]Answered based on provided excerpts[cite: 205]. |
| 5 | Difference between spearphishing attachment and link? | Yes | Good | [cite_start]Clearly distinguished based on document context[cite: 204]. |

## 3. Edge Case Observations
* [cite_start]**Unrelated Question (Weather):** When asked "What is the weather today?", the chatbot admitted it does not have real-time info[cite: 214].
* [cite_start]**Topic not in documents:** The bot admit it did not have the information for topics outside the uploaded scope[cite: 214].

## 4. Reflection
* [cite_start]**What surprised you about RAG?** I was surprised by how it finds specific sentences to prevent hallucinations[cite: 215, 265].
* [cite_start]**How could you improve this for real-world use?** I would use a persistent vector store like Pinecone[cite: 157, 237, 266].
* [cite_start]**Capstone Connection:** This serves as a functional prototype for my project's knowledge base[cite: 337, 343].

---
[cite_start]**Chatbot Share Link:** https://cloud.flowiseai.com/chatbot/175a7e0b-1bd5-4508-afbf-649ac149dcf7 [cite: 270]
