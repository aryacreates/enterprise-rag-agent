<img width="937" height="398" alt="image" src="https://github.com/user-attachments/assets/fa522d65-d924-418c-9e59-0fa9cecde8a1" />


# Enterprise RAG Agent

A local-first enterprise RAG agent demonstrating production-inspired GenAI engineering patterns including retrieval-augmented generation, tool orchestration, role-based access control, audit logging, and prompt-injection defenses.

## Overview

This project demonstrates how an enterprise AI assistant can answer questions from internal knowledge while applying access controls, restricting tool execution, and recording agent activity for auditability.

The application is designed to run locally without requiring AWS, Google Cloud, Azure, or paid AI APIs.

## Key Features

* Retrieval-Augmented Generation (RAG)
* Agent and tool orchestration
* Role-Based Access Control (RBAC)
* Prompt-injection detection and defenses
* Audit logging
* Input validation
* Controlled tool execution
* FastAPI backend
* Interactive web UI
* Docker support
* Automated tests
* Local LLM inference through Ollama
* Mock mode for reproducible execution

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
        │         │   │           │   │  Tools   │
        └─────────┘   └─────┬─────┘   └────┬─────┘
                            │              │
                            ▼              ▼
                     ┌────────────┐   ┌─────────────┐
                     │ Knowledge  │   │ Audit Logs  │
                     │   Base     │   └─────────────┘
                     └────────────┘

                         ┌──────────────────┐
                         │ Local LLM/Ollama │
                         └──────────────────┘
```

## RAG and Agent Workflow

```text
User Query
    ↓
Input Validation
    ↓
Security Checks
    ↓
Access Control
    ↓
Document Retrieval
    ↓
Relevant Context
    ↓
Agent / LLM
    ↓
Controlled Tool Execution
    ↓
Response + Sources
    ↓
Audit Event
```

The workflow separates retrieval, security checks, access control, and tool execution so that the assistant does not treat retrieved content as executable instructions.

## Security

The project demonstrates several enterprise AI security concepts:

* Role-based access control
* Input validation
* Prompt-injection detection
* Restricted tool execution
* Audit logging
* Separation of retrieved context from executable instructions
* Controlled access to protected resources

The security controls are implemented as a portfolio demonstration. A production deployment would require additional identity management, secrets management, network controls, monitoring, policy enforcement, security testing, and governance.

## RAG Pipeline

The retrieval workflow provides relevant knowledge to the agent before generating a response.

```text
Query
  ↓
Validation
  ↓
Security Filtering
  ↓
Retrieval
  ↓
Relevant Documents
  ↓
Context Construction
  ↓
LLM / Agent
  ↓
Grounded Response
```

The architecture is designed to keep retrieved knowledge separate from executable agent instructions and tools.

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

Replace `YOUR_USERNAME` with your GitHub username:

```bash
git clone https://github.com/YOUR_USERNAME/enterprise-rag-agent.git
cd enterprise-rag-agent
```

### 2. Create a virtual environment

**Windows:**

```bash
python -m venv .venv
.venv\Scripts\activate
```

**Linux/macOS:**

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

Open the application at:

```text
http://127.0.0.1:8000
```

FastAPI documentation:

```text
http://127.0.0.1:8000/docs
```

## Optional Local LLM

The application can use a locally running Ollama model for inference.

This provides a local execution path without requiring a paid cloud AI API.

Mock mode is also available for demonstrations and testing without downloading or running a local model.

## Docker

The project includes Docker support for containerized local execution.

Build the image:

```bash
docker build -t enterprise-rag-agent .
```

Run the container:

```bash
docker run -p 8000:8000 enterprise-rag-agent
```

Then open:

```text
http://127.0.0.1:8000
```

## Testing

Run the automated test suite:

```bash
pytest -q
```

The tests cover core application behavior and provide reproducible validation during development.

## Engineering Focus

This project focuses on enterprise GenAI engineering patterns rather than only demonstrating a basic chatbot.

Key areas include:

* RAG architecture
* Agent and tool orchestration
* Security controls
* RBAC
* Prompt-injection defenses
* Auditability
* Controlled tool execution
* API design
* Local deployment
* Testability
* Governance considerations

## Project Scope and Limitations

This is a portfolio project designed to demonstrate enterprise AI architecture and engineering patterns.

It does not claim:

* Production deployment
* Production-grade security certification
* Real enterprise customer data
* Production SLAs
* Proprietary cloud deployment
* Production-scale infrastructure

A production implementation would require additional identity and access management, secrets management, observability, networking, infrastructure security, evaluation, governance, and operational controls.

## Future Improvements

* Replace the local retrieval layer with Qdrant
* Add streaming responses
* Add LLM and RAG evaluation datasets
* Add OpenTelemetry tracing
* Add more granular policy enforcement
* Add PostgreSQL persistence
* Add Kubernetes deployment manifests
* Add optional cloud deployment adapters
* Add automated retrieval-quality evaluation
* Add stronger agent-policy enforcement
