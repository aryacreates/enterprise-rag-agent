# Enterprise RAG Agent

A local-first enterprise RAG agent designed to demonstrate production-oriented GenAI engineering patterns including retrieval-augmented generation, tool orchestration, role-based access control, audit logging, and prompt-injection defenses.

## Overview

This project demonstrates how an enterprise AI assistant can securely answer questions from internal knowledge while controlling access to protected resources and recording agent activity for auditability.

The application is designed to run locally without requiring AWS, Google Cloud, Azure, or paid AI APIs.

## Key Features

* Retrieval-Augmented Generation (RAG)
* Agent and tool orchestration
* Role-Based Access Control (RBAC)
* Prompt-injection detection and defenses
* Audit logging
* FastAPI backend
* Interactive web UI
* Docker support
* Automated tests
* Local LLM support through Ollama
* Mock mode for running without an LLM

## Architecture

```text
                 ┌─────────────────────┐
                 │       Web UI        │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │     FastAPI API     │
                 └──────────┬──────────┘
                            │
             ┌──────────────┼──────────────┐
             ▼              ▼              ▼
        ┌─────────┐   ┌───────────┐   ┌──────────┐
        │  RBAC   │   │ RAG Engine│   │  Agent   │
        └─────────┘   └─────┬─────┘   │  Tools   │
                            │         └────┬─────┘
                            ▼              │
                     ┌────────────┐        │
                     │ Knowledge  │        │
                     │   Base     │        │
                     └────────────┘        │
                                           ▼
                                    ┌─────────────┐
                                    │ Audit Logs  │
                                    └─────────────┘

                         ┌──────────────────┐
                         │ Local LLM/Ollama │
                         └──────────────────┘
```

## Security

The project demonstrates several enterprise AI security concepts:

* Role-based access control
* Input validation
* Prompt-injection detection
* Restricted tool execution
* Audit logging
* Separation of retrieved context from executable instructions

The security controls are implemented as a portfolio demonstration and should be hardened further before production deployment.

## RAG Pipeline

```text
User Query
    ↓
Input Validation
    ↓
Security Checks
    ↓
Document Retrieval
    ↓
Relevant Context
    ↓
Agent / LLM
    ↓
Response + Sources
    ↓
Audit Event
```

## Tech Stack

* Python
* FastAPI
* Pydantic
* Retrieval-Augmented Generation
* Agent/tool orchestration
* Ollama
* Docker
* HTML/CSS/JavaScript
* Pytest

## Running Locally

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/enterprise-rag-agent.git
cd enterprise-rag-agent
```

### 2. Create a virtual environment

Windows:

```bash
python -m venv .venv
.venv\Scripts\activate
```

Linux/macOS:

```bash
python -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Start the application

```bash
uvicorn app.main:app --reload
```

Open:

```text
http://127.0.0.1:8000
```

API documentation:

```text
http://127.0.0.1:8000/docs
```

## Testing

Run:

```bash
pytest -q
```

The repository includes automated tests covering the core application behavior.

## Optional Local LLM

The application can be connected to a locally running Ollama model for inference.

This keeps experimentation local and avoids requiring a paid cloud AI API.

The project also supports mock mode so the application can be demonstrated without downloading a model.

## Engineering Focus

This project was intentionally designed around enterprise GenAI engineering concerns rather than only demonstrating a chatbot.

It focuses on:

* Security
* Governance
* Retrieval quality
* Controlled tool execution
* Observability
* API design
* Local deployment
* Testability

## Why This Project

The project explores the architecture required to move from a basic LLM chatbot toward an enterprise AI assistant capable of working with protected knowledge and controlled tools.

## Future Improvements

* Replace the local retrieval layer with Qdrant
* Add streaming responses
* Add LLM/RAG evaluation datasets
* Add OpenTelemetry tracing
* Add more granular policy enforcement
* Add PostgreSQL persistence
* Add Kubernetes deployment manifests
* Add optional cloud deployment adapters
