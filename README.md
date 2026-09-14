# ⚡ AgentPulse — Backend Evaluation Engine & API Server
**Branch:** `backend` | **Team:** `HTF26-012-AI-Developers` | **Hack the Future 26**

---

## 📖 Component Overview

The **Backend Subsystem** of AgentPulse powers the automated evaluation, grading, scoring, and telemetry ingestion for autonomous AI agents. Built with high-throughput Python asynchronous pipelines and FastAPI, it delivers real-time assertions, model-graded evaluations, and deterministic benchmarking.

### Core Modules

1. **FastAPI Ingestion & Telemetry Server** ([`src/server.py`](file:///src/server.py)):
   - High-throughput REST API endpoints for agent run ingestion (`POST /runs`), trace ingestion (`POST /traces`), and live step streaming (`POST /steps`).
   - Health check probe (`GET /health`) and exportable ASGI handlers compatible with production ASGI servers (Uvicorn) and serverless runtimes.

2. **Core Entities & Evaluation Engine** ([`src/core/`](file:///src/core/)):
   - Standardized entity models: `Run`, `Step`, `EvaluationResult`, `Trace`, `Span`, and `TestCase`.
   - Dynamic evaluator interfaces and pluggable rule engines.

3. **Evaluation & LLM Judges** ([`src/evaluation/`](file:///src/evaluation/)):
   - **Deterministic Evaluators**: Exact match, regex patterns, keyword checks, JSON schema validators, tool selection accuracy, and argument structure validators.
   - **Model-Graded Judges** (`llm_judge.py`): Multi-provider LLM judges (Claude 3.5 Haiku / Sonnet, OpenAI GPT-4o, and deterministic mock judge fallbacks) for groundedness, hallucination detection, and semantic quality.
   - **Domain Evaluators**: Specialized evaluators for RAG faithfulness, context recall, and Model Context Protocol (MCP) tool execution.
   - **Weighted Scoring Engine** (`scoring.py`): Configurable scoring matrices (Task Success, Tool Accuracy, Groundedness, Quality, Latency Budget, and Cost Budget).

4. **Token & Cost Calculator** ([`src/cost/`](file:///src/cost/)):
   - Real-time token tracking and financial analytics across Claude, OpenAI, and custom fine-tuned models.

5. **Batch Evaluation Runner** ([`src/runner.py`](file:///src/runner.py)):
   - Multi-agent benchmark runner with concurrent execution, error recovery, and database logging.

---

## 🚀 Quick Start (Backend)

```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Configure environment
cp .env.example .env

# 3. Launch FastAPI Telemetry Server
uvicorn src.server:app --host 0.0.0.0 --port 8000 --reload
```

Server will be running at `http://localhost:8000`. OpenAPI documentation available at `http://localhost:8000/docs`.