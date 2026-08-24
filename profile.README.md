# Team 1 — CTF Intern Challenge

> Building a **Compliance Document Review App** as part of the Capture the Flag Intern Challenge.

## 👥 Team

| Member                       | Role                 |
| ---------------------------- | --------------------- |
| **Basamsetti Venkata Vamsi** | AI Engineer                   |
| **Kashish Agarwal**          | Backend Engineer               |
| **Daniel Ojo**               | Frontend Engineer              |
| **Jemarco Briz**             | Data Engineer    |
| **DevOps / Platform**        | Shared responsibility |

## 🚀 Project

### Compliance Document Review App

Financial advisors create client-facing materials such as marketing emails, brochures, social posts, meeting notes, and proposal letters. These documents need to be reviewed by a compliance officer before they can be released.

We are building a web application that closes this workflow by providing a shared platform where:

* Advisors can submit documents and track their review status.
* Compliance officers can review submissions through a centralized queue.
* AI provides a summary and identifies potential compliance issues.
* Every AI flag is traceable to the relevant passage and compliance rule.
* Officers make the final decision — **AI never makes the decision**.
* Revisions remain linked to the original submission as one document history.
* Every important action is recorded through an audit trail.

## 🔄 Document Lifecycle

```text
Advisor
   │
   ▼
Submit Document
   │
   ▼
Pending Review
   │
   ├──────────────► Approved
   │
   ├──────────────► Rejected
   │
   └──────────────► Needs Revision
                          │
                          ▼
                     Resubmission
                          │
                          └──────► Pending Review
```

AI analysis and the audit trail run alongside the document lifecycle.

## 🧠 AI & Data Engineering

The AI-assisted review system uses retrieval rather than asking a general-purpose model to determine compliance.

### AI

* Server-side PII masking before external API calls
* Document summarization
* Potential compliance issue detection
* Passage-level explanations for every flag
* Integration with a free-tier third-party LLM API
* Graceful degradation when the AI service is unavailable
* Cached analysis to avoid unnecessary API calls

### Data Engineering

* PDF / DOCX / XLSX text extraction
* Clean text processing
* PII-masked document pipeline
* Document chunking
* Embedding generation
* Vector storage and similarity search
* Compliance rule retrieval
* Missing-disclosure detection
* Precedent document retrieval
* Retrieval quality tuning

The recommended architecture uses **PostgreSQL + pgvector**, keeping structured application data and vector search within the same data platform.

## 🏗️ Engineering Tracks

### Backend

Owns authentication, role enforcement, document uploads, document state transitions, revisions, audit events, and notifications.

### Frontend

Owns the advisor and compliance officer dashboards, review interface, AI assist panel, filtering, and error/empty/degraded states.

### AI

Owns PII masking, LLM integration, summaries, compliance flags, and reasoning associated with each flag.

### Data Engineering

Owns document ingestion, text extraction, chunking, embeddings, vector search, compliance-rule retrieval, disclosure detection, and precedent retrieval.

### DevOps / Platform

Owns reproducible development setup, containerization, database initialization, corpus seeding, environment configuration, and CI.

## 🔐 Security & Privacy

Privacy is a core requirement of the project.

* PII is masked **before** data leaves the application.
* Raw PII must never be sent to external AI or embedding APIs.
* PII mappings remain server-side.
* All document data requires an authenticated session.
* Role enforcement is performed on the backend.
* Advisors cannot access officer functionality.
* Officers cannot submit advisor documents.
* No real client data is used.
* API keys are managed through environment variables and never committed.

## 🧪 Quality Requirements

The project must:

* Support the complete advisor → review → decision workflow.
* Enforce role boundaries at the API level.
* Test the PII masking system.
* Provide traceable AI flags.
* Support revision and resubmission history.
* Maintain an append-only audit trail.
* Continue functioning when the AI API is unavailable.
* Run from a clean checkout using documented setup instructions.
* Pass the project's automated test suite.

## 📅 One-Month Development Plan

| Week       | Focus                                                                                           |
| ---------- | ----------------------------------------------------------------------------------------------- |
| **Week 1** | Authentication, roles, backend permissions, uploads, dashboards, document workflow              |
| **Week 2** | Text extraction, PII masking, rule corpus, vector retrieval, AI summary and flags               |
| **Week 3** | Disclosure detection, precedent search, revisions, audit trail, filtering, graceful degradation |
| **Week 4** | Testing, clean-checkout setup, hardening, integration, and final preparation                    |

## 🛠️ Technology

The final stack is determined by the team, with the following recommended technologies:

* **PostgreSQL**
* **pgvector**
* **Backend API**
* **Frontend web application**
* **Python-based data / AI services**
* **Docker**
* **CI/CD**
* **Gemini / Groq / OpenRouter** for AI assistance

## 📌 Project Constraints

* Two fixed roles: **Advisor** and **Compliance Officer**
* PDF / DOCX / XLSX uploads
* Maximum file size: **10 MB**
* In-app notifications only
* Any officer can review any submission
* AI assists but **never makes the final decision**
* No production Anthropic credits
* No real client data
* No fine-tuning or self-hosted models
* Vector retrieval is required

---

**Capture the Flag Intern Challenge — Project Phase**

*Team 1 • Backend • Frontend • AI • Data Engineering • DevOps*
