# Autonomous Financial Fraud Detection & Analysis Pipeline

An automated backend data pipeline that ingests financial transactions, evaluates risk profiles using zero-shot text classification, and leverages Large Language Models (LLMs) to generate real-time security explanations—all synced seamlessly to a relational data store.

## 🚀 Architecture Overview

This project orchestrates multiple AI models and data systems into a unified asynchronous loop:

1. **Data Ingestion:** Batch transaction data is processed row-by-row via a loop controller.
2. **Context-Aware Routing:** High-value or cross-border anomalies are dynamically branched away from standard local retail transactions.
3. **LLM Reasoning Engine:** A Llama-3.1 model running on Groq analyzes transaction metadata (Merchant, Location, Amount) to mathematically deduce a risk tier and write a strict, fluff-free security summary.
4. **Data Synchronization:** Real-time updates push risk categories (`High`, `Medium`, `Low`), confidence scores, and explanations directly to an Airtable database while updating row processing states.

[Insert your n8n workflow screenshot here]

## 🛠️ Tech Stack
* **Orchestration:** n8n Workflow Automation
* **AI/Inference Engines:** Groq API (Llama 3.1 8B Instant)
* **Data Store:** Airtable DB / REST API
* **Language/Formatting:** JavaScript (JSON payload structuring & string manipulation)

## 📊 Key Features & Error Handling
* **Dynamic String Splitting:** Bypasses UI parsing limitations by forcing the LLM to output a strict `[RISK_TAG] | [EXPLANATION]` format, separated via native JavaScript runtime splits.
* **Fallback Fault-Tolerance:** Built-in catch blocks safeguard pipeline continuity against API rate limits or mismatched loop schemas.
* **Intelligent Ambiguity Tracking:** Successfully catches edge cases (e.g., unknown merchants in foreign hubs) and routes them into an explicit `Unknown Risk` monitoring tier instead of breaking the execution thread.

## 📖 Sample Pipeline Output
| Transaction ID | Merchant | Location | Amount | Risk Tag | AI Security Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TXN-028 | Wire Transfer | Lagos | $78,500.00 | High Risk | This transaction is an anomaly due to a high-value cross-border wire transfer from an unverified location, increasing the likelihood of money laundering. |
| TXN-036 | ATM Withdrawal | Brooklyn | $200.00 | Low Risk | This transaction is a typical local low-value ATM withdrawal and does not exhibit characteristics commonly associated with financial fraud. |

## ⚙️ Setup Instructions
1. Clone this repository.
2. Import the JSON workflow file from `/pipelines` into your n8n instance.
3. Configure your credentials for Groq (Llama-3.1) and Airtable.
4. Run the trigger to execute the automated data ingestion loop.
