# System Design: Chhatra-Sahayak

## 1. High-Level Architecture
Chhatra-Sahayak uses an **Agentic Workflow** architecture. It is not just a chatbot; it is a system that "Listens, Analyzes, and Acts." The core orchestration handles voice processing, legal reasoning, and document generation seamlessly.

### 1.1. Architecture Diagram Flow
`[Student]` -> `[Voice/Image Input]` -> `[AWS Lambda]` -> `[Bedrock Agent]` -> `[Amazon Q (RAG)]` -> `[Action: Draft & Email]`

## 2. Technical Components

### 2.1. Frontend (User Layer)
* **Interface:** React Native (Mobile App) / React (Web Dashboard).
* **Input Channels:** WhatsApp Business API integration for low-friction access.

### 2.2. The "AI Brain" (Agent Layer)
* **Orchestrator:** **Amazon Bedrock Agents**. This manages the multi-step logic:
    1.  Receive Input.
    2.  Invoke **Severity Classifier**.
    3.  Query Knowledge Base.
    4.  Generate Document.
* **Development Tool:** **AWS Kiro** was used to prototype the agentic workflow and generate the initial spec-to-code structure.

### 2.3. AI Models & Services
* **Reasoning & Drafting:** **Amazon Bedrock (Claude 3.5 Sonnet)**. Chosen for its superior reasoning in Indian contexts and legal drafting capabilities.
* **Knowledge Retrieval (RAG):** **Amazon Q Business**. Indexed with:
    * UGC Anti-Ragging Regulations 2009.
    * Bharatiya Nyaya Sanhita (BNS) / IPC.
    * Consumer Protection Act 2019.
* **Voice Processing:** **Amazon Transcribe** (Speech-to-Text) and **Amazon Polly** (Text-to-Speech) for vernacular interaction.
* **Vision:** **Amazon Textract** for reading uploaded physical notices or handwritten letters.

### 2.4. Backend & Data
* **Compute:** AWS Lambda (Serverless) for executing business logic and routing emails.
* **Database:** Amazon DynamoDB (Single-table design) for storing User Profiles and Case Histories.
* **Storage:** Amazon S3 for storing generated PDF complaints and user-uploaded evidence (encrypted).

## 3. Data Flow: The "Voice-to-Legalese" Pipeline

1.  **Ingestion:** User speaks in Hindi: *"Mera landlord security deposit wapas nahi kar raha."*
2.  **Transcription:** Amazon Transcribe converts audio to Hindi text -> Translate to English context.
3.  **Classification:** Bedrock Agent identifies intent: `Dispute_Type: Tenancy`, `Severity: Civil`.
4.  **Retrieval:** Amazon Q retrieves "Model Tenancy Act" and "Consumer Court" templates.
5.  **Drafting:** Claude 3.5 Sonnet drafts a formal notice: *"Subject: Demand for Refund of Security Deposit under Section..."*
6.  **Delivery:** The PDF is generated and sent to the user via WhatsApp/App.

## 4. Security & Compliance
* **IAM Roles:** Strict least-privilege access for the AI Agent to access user data.
* **PII Redaction:** Amazon Comprehend is used to detect and mask names/phones in the "Anonymous Shield" mode before data storage.