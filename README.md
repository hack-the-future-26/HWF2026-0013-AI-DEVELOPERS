# 🗄️ AgentPulse — Database, Storage Layer & Dataset Registry
**Branch:** `database` | **Team:** `HTF26-012-AI-Developers` | **Hack the Future 26**

---

## 📖 Component Overview

The **Database Subsystem** of AgentPulse handles persistence, relational schema management, benchmark dataset cataloging, and agent registry lifecycle. Designed for both high-concurrency local development and resilient cloud deployment (Render, PostgreSQL, SQLite with WAL mode).

### Core Architecture

1. **Storage & Engine Abstraction** ([`src/storage/db.py`](file:///src/storage/db.py)):
   - Pluggable SQLAlchemy session management supporting both SQLite (`sqlite:///./eval_framework.db`) and PostgreSQL (`postgresql://...`).
   - SQLite Concurrency Hardening: Automatic `PRAGMA journal_mode=WAL;`, `PRAGMA synchronous=NORMAL;`, and `PRAGMA busy_timeout=30000;` to eliminate write contention and database locks.
   - Idempotent schema initialization (`init_db()`) and retry handlers.

2. **Relational Data Models** ([`src/storage/models.py`](file:///src/storage/models.py)):
   - `Run`: Agent execution metadata (agent name, model, duration, token usage, cost, status).
   - `Step`: Chronological execution steps within a run (user input, LLM response, tool invocation).
   - `EvaluationResult`: Assertion scores, binary pass/fail flags, evaluator types, and explanatory evidence.
   - `Trace` & `Span`: Distributed OpenTelemetry-compatible trace trees and sub-operation spans.
   - `TestCase`: Expected ground truth, input parameters, system prompt variations, and assertion criteria.
   - `Dataset`: Named benchmark collections with semantic versioning.
   - `AgentRecord` & `AgentVersion`: Registered agents, deployment environments, endpoints, and configuration versions.

3. **Dataset & Catalog Management** ([`src/dataset/`](file:///src/dataset/)):
   - Version-controlled benchmark suites for regression testing and CI/CD gates.

4. **Agent Registry** ([`src/registry/`](file:///src/registry/)):
   - Unified catalog of AI agents, connection configurations, provider models, and active deployment stages.

---

## 🚀 Database Initialization

```python
from src.storage.db import init_db, get_session
from src.storage.models import AgentRecord

# Initialize tables
init_db()

# Query session
session = get_session()
agents = session.query(AgentRecord).all()
print(f"Registered agents: {len(agents)}")
session.close()
```