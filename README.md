# Enterprise GenAI Knowledge Assistant

> Production-oriented Generative AI Knowledge Assistant for context-grounded enterprise document Q&A using Retrieval-Augmented Generation (RAG).

![Python](https://img.shields.io/badge/Python-3.12-blue)
![FastAPI](https://img.shields.io/badge/FastAPI-API-green)
![React](https://img.shields.io/badge/React-Frontend-61DAFB)
![RAG](https://img.shields.io/badge/GenAI-RAG-purple)
![ChromaDB](https://img.shields.io/badge/Vector_DB-ChromaDB-orange)
![Docker](https://img.shields.io/badge/Docker-Containerized-blue)

---

## Overview

The **Enterprise GenAI Knowledge Assistant** is a production-oriented Generative AI application that enables users to interact with enterprise documents using natural language.

Instead of sending a user's question directly to an LLM, the system first retrieves relevant information from an enterprise knowledge base and then provides that context to the LLM.

This Retrieval-Augmented Generation (RAG) approach helps produce responses that are grounded in the organization's available knowledge rather than relying solely on the LLM's general knowledge.

### Example

**User question:**

> Can employees work from home?

**Retrieved knowledge:**

> Eligible employees may work remotely up to three days per week, subject to manager approval and business requirements.

**Source:**

> Employee Handbook → Section 2: Remote Work

---

# Business Problem

Enterprise organizations often have large amounts of information distributed across:

- Employee handbooks
- IT policies
- Security documentation
- HR documentation
- Benefits guides
- Travel policies
- Operational procedures
- Internal knowledge bases

Traditional keyword-based search can make it difficult for employees to find the exact information they need.

The objective of this project is to provide a natural-language interface over enterprise knowledge while maintaining:

- Context grounding
- Relevant document retrieval
- Source traceability
- Controlled responses
- Scalable architecture

---

# Solution

The solution implements a Retrieval-Augmented Generation architecture.

```text
                         Enterprise Documents
                                  |
                                  v
                         Document Ingestion
                                  |
                                  v
                           Text Chunking
                                  |
                                  v
                         Embedding Model
                                  |
                                  v
                            Vector DB
                           (ChromaDB)
                                  |
                                  |
User Question -------------------+
        |
        v
   Query Embedding
        |
        v
   Semantic Search
        |
        v
 Relevant Context
        |
        v
      LLM
        |
        v
 Grounded Response
        |
        v
 Source Citations

```
# Architecture

The Enterprise GenAI Knowledge Assistant follows a modular, production-oriented architecture designed to separate the user interface, API layer, retrieval pipeline, vector storage, and LLM inference.

```text
┌─────────────────────────────────────────────────────────────┐
│                         User                                │
│              Natural Language Question                      │
└───────────────────────────┬─────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                     React Frontend                          │
│                                                             │
│  • Chat Interface                                           │
│  • Conversation History                                     │
│  • Source / Citation Display                                │
└───────────────────────────┬─────────────────────────────────┘
                            │ REST / JSON
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                     FastAPI Backend                         │
│                                                             │
│  • API Endpoints                                            │
│  • Request Validation                                       │
│  • Error Handling                                           │
│  • Application Services                                     │
└───────────────────────────┬─────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                       RAG Engine                            │
│                                                             │
│  1. Query Processing                                        │
│  2. Query Embedding                                         │
│  3. Semantic Retrieval                                      │
│  4. Context Construction                                    │
│  5. Prompt Assembly                                         │
└───────────────┬─────────────────────────────┬───────────────┘
                │                             │
                ▼                             ▼
┌───────────────────────────┐     ┌───────────────────────────┐
│      Embedding Model      │     │       ChromaDB            │
│                           │     │                           │
│ all-MiniLM-L6-v2          │────▶│ Vector Embeddings        │
│ 384-dimensional vectors   │     │ Document Chunks           │
└───────────────────────────┘     │ Metadata                  │
                                  └─────────────┬─────────────┘
                                                │
                                                │ Relevant Context
                                                ▼
                                  ┌───────────────────────────┐
                                  │          LLM              │
                                  │                           │
                                  │ Context + User Question   │
                                  │           ↓               │
                                  │ Grounded Response         │
                                  └─────────────┬─────────────┘
                                                │
                                                ▼
                                  ┌───────────────────────────┐
                                  │ Response + Sources        │
                                  │                           │
                                  │ Returned to React UI      │
                                  └───────────────────────────┘
```
# Technology Stack
```text
| Layer               | Technology                     |
| ------------------- | ------------------------------ |
| Frontend            | React                          |
| Backend             | Python / FastAPI               |
| AI                  | Generative AI / LLM            |
| RAG                 | Retrieval-Augmented Generation |
| Embeddings          | Sentence Transformers          |
| Vector Database     | ChromaDB                       |
| Document Processing | PyPDF                          |
| API Communication   | REST / JSON                    |
| Containerization    | Docker                         |
| Version Control     | Git / GitHub                   |
```

# Project Structure
```text

enterprise-genai-knowledge-assistant/
│
├── backend/
│   ├── app/
│   │   ├── api/
│   │   ├── embeddings/
│   │   ├── ingestion/
│   │   ├── models/
│   │   ├── rag/
│   │   ├── services/
│   │   ├── utils/
│   │   ├── vectorstore/
│   │   ├── ingest.py
│   │   ├── search.py
│   │   └── main.py
│   │
│   ├── tests/
│   └── requirements.txt
│
├── frontend/
│   └── src/
│
├── documents/
│
├── docs/
│
├── architecture/
│
├── tests/
│
├── .gitignore
└── README.md
```

# Example Knowledge Base

The demonstration knowledge base contains fictional enterprise documentation including:

- Employee Handbook
- Remote Work Policy
- Information Security Policy
- Password Policy
- Travel Policy
- Expense Reimbursement
- Employee Support

The documents are intentionally fictional and contain no confidential company information.

# Example Queries

The system is designed to support natural-language questions such as:

**Remote Work**

>Can employees work from home?

**Paid Time Off**

>How many vacation days do employees get?

**Security**

>Can I share my company password with a coworker?

**Expenses**

>When do I need to submit business expenses?

**Travel**

>Does business travel require approval?

**Unsupported Information**

>What is the parental leave policy?

The last example demonstrates how the application handles information that is not present in the knowledge base.

# API Architecture

The backend is implemented using FastAPI.

**Example health endpoint:**

>GET /health

>Example response:
```text
{
  "status": "healthy",
  "service": "enterprise-genai-knowledge-assistant",
  "version": "0.1.0"
}
```

**Future API capabilities include:**
```text
POST /documents
POST /search
POST /chat
GET  /documents
GET  /health
```
# Engineering Considerations

The project is designed with production-oriented engineering principles in mind.

- Retrieval Quality
- Section-aware document chunking
- Semantic embeddings
- Vector similarity search
- Configurable retrieval count
- Reliability
- Input validation
- Error handling
- Health checks
- Logging
- Testable service boundaries
- Scalability

# The architecture separates:

- Document ingestion
- Embedding generation
- Vector storage
- Retrieval
- LLM orchestration
- API layer
- Presentation layer

This allows individual components to evolve independently.

# Security Considerations

A production deployment should include:

- Authentication and authorization
- Role-based access control
- Document-level access permissions
- Secure secret management
- Encryption in transit
- Encryption at rest
- Audit logging
- PII detection/redaction
- Prompt-injection protection
- Retrieval access controls

No credentials, API keys, or production secrets are included in this repository.

# Deployment

The application is designed to support containerized deployment using Docker.

**Target deployment architecture:**
```text
                  Load Balancer
                       |
              +--------+--------+
              |                 |
              v                 v
         Frontend           FastAPI
                               |
                         +-----+-----+
                         |           |
                         v           v
                    Vector DB      LLM
```
The architecture can be extended to cloud environments such as:

- AWS
- Microsoft Azure
- Google Cloud Platform
