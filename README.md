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
