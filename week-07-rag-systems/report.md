# Week 7: RAG Security Knowledge Assistant

## 1. Setup Summary
* **LLM:** llama-3.3-70b-versatile via Groq
* **Embeddings:** sentence-transformers/all-MiniLM-L6-v2 via HuggingFace
* **Vector Store:** In-Memory Vector Store
* **Documents Loaded:** 3 MITRE ATT&CK technique text files

## 2. Test Results

| # | Question | Used Documents? | Quality | Notes |
| :--- | :--- | :--- | :--- | :--- |
| 1 | What are common techniques for credential access? | Yes | Good | Accurately cited techniques from the uploaded text. |
| 2 | How does phishing relate to initial access? | Yes | Good | Correctly identified the link between the two. |
| 3 | What is lateral movement and what techniques are used? | Yes | Good | Listed specific techniques directly from sources. |
| 4 | What does the NIST framework recommend for "Detect"? | Yes | Partial | Answered based on provided excerpts. |
| 5 | Difference between spearphishing attachment and link? | Yes | Good | Clearly distinguished based on document context. |

## 3. Edge Case Observations
* **Unrelated Question (Weather):** When asked "What is the weather today?", the chatbot admitted it does not have real-time information.
* **Topic not in documents:** For topics outside of the MITRE/NIST scope, the bot admits it lacks specific information.

## 4. Reflection
* **What surprised you about RAG?** I was surprised by how effectively the system finds specific sentences to prevent hallucinations.
* **How could you improve this for real-world use?** I would implement a persistent vector store like Pinecone so the documents are saved permanently.
* **Capstone Connection:** This serves as a functional prototype for building a specialized knowledge assistant for my project.

---
**Chatbot Share Link:** https://cloud.flowiseai.com/chatbot/175a7e0b-1bd5-4508-afbf-649ac149dcf7
