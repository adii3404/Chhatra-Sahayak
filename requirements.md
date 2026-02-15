# Requirements: Chhatra-Sahayak (The AI Shield for Student Rights)

## 1. Executive Summary
**Chhatra-Sahayak** is a multilingual, voice-first AI agent designed to democratize legal and administrative justice for Indian students. It acts as a digital lawyer and grievance counselor, converting informal, vernacular student complaints into structured, legally sound documents using Generative AI.

## 2. Problem Statement
* **Under-reporting:** 80% of student grievances (ragging, landlord disputes, academic bias) go unreported.
* **Barriers:** Fear of retaliation, lack of legal knowledge (UGC/IPC norms), and language barriers (English-heavy portals).
* **Complexity:** Existing systems are bureaucratic and intimidating.

## 3. User Personas
* **Student (The Victim):** Needs a safe, anonymous way to report harassment or financial loss without knowing complex laws.
* **University Admin (The Receiver):** Needs structured, actionable complaints rather than vague or emotional emails.

## 4. Functional Requirements

### 4.1. Core Modules
* **FR-01: Voice-to-Legalese Engine**
    * The system must accept voice input in Indian languages (Hindi, Tamil, Marathi, English).
    * It must transcode emotional/informal speech (e.g., *"Sir hostel warden is asking for bribe"*) into formal legal citations (e.g., *"Violation of UGC Anti-Corruption Guidelines..."*).
* **FR-02: Severity Classifier**
    * The AI must analyze the complaint text to classify severity:
        * **Emergency:** Ragging, Physical Harassment (Trigger immediate alert).
        * **Civil:** Refund disputes, Landlord issues (Route to drafting).
* **FR-03: Anonymous Shield System**
    * A privacy toggle that allows filing complaints via a proxy identity.
    * The system must redact PII (Name, Roll No.) from the initial report sent to authorities unless legally required.

### 4.2. Agentic Capabilities
* **FR-04: Document Analysis (OCR)**
    * Users can upload photos of eviction notices or marksheets.
    * The system must extract text and identify legal validity using Amazon Textract.
* **FR-05: Automated Drafting & Routing**
    * The agent must generate a PDF complaint based on the identified issue.
    * It must automatically find the correct recipient email (Proctor, SHO, Consumer Court) based on the institution and issue type.

## 5. Non-Functional Requirements
* **NFR-01: Privacy & Security:** All student data must be encrypted. Anonymity layers must be irreversible by unauthorized admins.
* **NFR-02: Latency:** Voice processing and legal drafting must occur within 10 seconds to maintain user confidence.
* **NFR-03: Accuracy:** Legal citations (IPC Sections, UGC Regulations) must be verified against the Amazon Q Knowledge Base to prevent hallucinations.

## 6. Future Roadmap
* **Phase 1:** Web App & WhatsApp Bot integration.
* **Phase 2:** Direct API integration with National Anti-Ragging Helpline.
* **Phase 3:** Mental Health Counseling Module (AI Therapist).