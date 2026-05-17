# AI Core Component & Process Integration
**System Hub:** Financial Fraud Detection System  
**Author:** Thomas Kamel  

## 1. System Overview
The AI Core component serves as the central orchestration engine for the Financial Fraud Detection System. It intercepts raw, unstructured transaction anomalies and system events pushed via webhooks, coordinates a multi-layered large language model inference pipeline to grade the security risk, and structures the intelligence outputs into machine-readable incident responses.

## 2. Multi-Chain Flowise Architecture
The orchestration pipeline leverages three isolated asymmetric LLM chains powered by `llama-3.3-70b-versatile` via the Groq API:

* **Chain 1: Alert Classifier:** Consumes raw text payloads from system log webhooks and maps the event to a strict classification output (`CRITICAL`, `HIGH`, `MEDIUM`, `LOW`).
* **Chain 2: Threat Analyzer:** Parses the classified indicators to extract specific attack patterns, impacted infrastructure targets, and historical anomalies.
* **Chain 3: Response Recommender:** Accepts the full threat intelligence payload and outputs concrete, structured playbook steps (`containment_steps`, `eradication_steps`).

## 3. n8n Data Pipeline Integration
Data is routed through automated HTTP Request nodes within a unified master n8n workflow canvas.

* **Inputs:** Receives raw JSON records from the Ingestion component (Ergi) when rows match a database status state of `pending_triage`.
* **Outputs:** Writes structured text blocks and JSON schemas back to the central database, modifying the tracking field state to `analyzed` to trigger downstream Specialist automation (Andrew).

## 4. Environment Setup & Configuration
To stand up this component, configure an n8n HTTP Request node with the following settings:
* **Method:** POST
* **URL:** Your Flowise API Endpoint URL
* **Authentication:** Header Auth (using your Flowise API Account Key)
* **JSON Body:** Must use an expression sequence to serialize inputs.

## 5. Known Limitations & Mitigation
* **Formatting Break Bug:** Unstructured conversational payloads containing pre-existing internal double quotes (`"`) and raw newline characters (`\n`) originally broke the execution container's JSON parser.
* **Mitigation Step:** Bypassed raw variable nesting blocks by implementing a structural serialization string helper wrapper. All pass-through parameters are sanitized using:
`={ "question": {{ jsonStringify($json.text) }} }`