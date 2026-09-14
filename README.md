# 🔍 AgentPulse — Observability, Distributed Tracing & MCP Inspection
**Branch:** `observability` | **Team:** `HTF26-012-AI-Developers` | **Hack the Future 26**

---

## 📖 Component Overview

The **Observability Subsystem** of AgentPulse provides end-to-end distributed execution tracing, Model Context Protocol (MCP) telemetry, and automated root cause error diagnosis for complex multi-agent architectures.

### Core Architecture

1. **Distributed Execution Tracer** ([`src/tracing/`](file:///src/tracing/)):
   - **Span-Level Tracking** (`tracer.py`): Sub-millisecond timing, parent-child trace trees, token counts, and input/output payload capture.
   - **MCP Protocol Observability** (`mcp_tracer.py`): Real-time interception and structural validation of Model Context Protocol tool requests, tool responses, server handshakes, and capability negotiation.
   - **Hierarchy & Timeline Utilities** (`hierarchy.py`): Assembles flat event logs into navigable span DAGs with latency attribution.

2. **Automated Root Cause Analysis (RCA)** ([`src/analysis/`](file:///src/analysis/)):
   - **Failure Classifier** (`root_cause.py`): Automatically classifies test failures into standardized error taxonomies:
     - `HALLUCINATION`: Grounding violations and unfaithful claims against context.
     - `TOOL_SCHEMA_VIOLATION`: Invalid parameter types or missing required fields.
     - `TOOL_EXECUTION_ERROR`: Remote MCP server exceptions or HTTP timeouts.
     - `CONTEXT_OVERFLOW`: Exceeded model token context budgets.
     - `LOGICAL_DEVIATION`: Divergence from specified test case reasoning path.
   - **Failure Analysis & Triage** (`failure_analysis.py`): Aggregates failure patterns across batches to identify systemic regressions.

3. **Client Telemetry SDK** ([`src/sdk/`](file:///src/sdk/), [`agentpulse/`](file:///agentpulse/)):
   - Lightweight, zero-overhead client library (`pip install -e .`).
   - Non-blocking asynchronous background flushing to ensure agent inference is never throttled.

---

## 🚀 Integrating the Telemetry SDK

```python
from agentpulse import AgentPulseTracer

# 1. Initialize tracer
tracer = AgentPulseTracer(agent_name="FinancialAnalyst", agent_version="v2.1")

# 2. Trace agent execution
with tracer.trace("PortfolioOptimization") as trace:
    with trace.span("FetchMarketData", span_type="tool") as s:
        s.set_attribute("symbol", "AAPL")
        data = fetch_prices("AAPL")
        s.set_output({"price": 220.5})

    with trace.span("GenerateThesis", span_type="llm") as s:
        response = call_llm("Generate allocation...")
        s.set_output(response)
```