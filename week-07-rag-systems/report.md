# Week 7: RAG Security Knowledge Assistant

## 1. Setup Summary
* [cite_start]**LLM:** llama-3.3-70b-versatile via Groq [cite: 55, 174]
* [cite_start]**Embeddings:** sentence-transformers/all-MiniLM-L6-v2 via HuggingFace [cite: 146]
* [cite_start]**Vector Store:** In-Memory Vector Store [cite: 156]
* **Documents Loaded:** * `mitre-initial-access.txt` 
    * `mitre-credential-access.txt` 
    * `mitre-lateral-movement.txt`

## 2. Test Results

| # | Question | Used Documents? | Quality | Notes |
| :--- | :--- | :--- | :--- | :--- |
| 1 | What are common techniques for credential access? | Yes | Good | Correctly identified techniques like Brute Force and OS Credential Dumping. |
| 2 | How does phishing relate to initial access? | Yes | Good | Linked phishing to the delivery of malicious attachments/links. |
| 3 | What is lateral movement and what techniques are used? | Yes | Good | Cited Remote Services and Exploitation of Remote Services. |
| 4 | What does the NIST framework recommend for "Detect"? | Yes | Partial | Answered based on specific Detect category excerpts provided. |
| 5 | Difference between spearphishing attachment and link? | Yes | Good | Clearly explained the technical distinction found in the documents. |

## 3. Edge Case Observations
* [cite_start]**Unrelated Question (Weather):** When asked "What is the weather today?", the chatbot admitted it does not have access to real-time information[cite: 214]. This confirms the RAG system is successfully constrained to the knowledge base.
* [cite_start]**Topic not in documents:** For topics outside of the MITRE/NIST scope, the bot admits it lacks specific information rather than hallucinating[cite: 215].

## 4. Reflection
* [cite_start]**What surprised you about RAG?** I was surprised by how the system converts text into numerical vectors (embeddings) to find similarity between questions and documents[cite: 115, 117].
* [cite_start]**How could you improve this for real-world use?** I would implement a persistent vector store like Pinecone so document embeddings are saved permanently instead of being lost when the session ends[cite: 157, 237].
* [cite_start]**Capstone Connection:** This setup serves as a functional prototype for building a specialized knowledge assistant for my capstone project documentation[cite: 337, 343].

---

[cite_start]**Chatbot Share Link:** https://cloud.flowiseai.com/chatbot/175a7e0b-1bd5-4508-afbf-649ac149dcf7 [cite: 231]
