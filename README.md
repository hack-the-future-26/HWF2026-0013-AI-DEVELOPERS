# 🎨 AgentPulse — Frontend Observability & Evaluation Console
**Branch:** `frontend` | **Team:** `HTF26-012-AI-Developers` | **Hack the Future 26**

---

## 📖 Component Overview

The **Frontend Subsystem** of AgentPulse delivers an executive observability console and interactive evaluation workbench for AI development teams. Designed with a luxury dark mode aesthetic (`Plus Jakarta Sans` typography, `JetBrains Mono` code telemetry, and glassmorphic cards), it provides deep real-time visibility into agent runs, traces, tools, and evaluations.

### Core Architecture

- **Main Dashboard Shell** ([`dashboard/app.py`](file:///dashboard/app.py)):
  - Custom dark theme CSS design tokens, sidebar navigation hierarchy, and global filter controls (Agent, Version, Dataset, Model, Status, and Date Range).
  - Single-pass cached data loader (`@st.cache_data`) for instant page switches and zero N+1 database queries.

- **14 Analytical View Modules** ([`dashboard/views/`](file:///dashboard/views/)):
  1. **Overview** (`overview.py`): Executive KPI scorecard, health pills, pass rates by dimension, latency trend chart, and live run feed.
  2. **Evaluation Runs** (`eval_runs.py`): Run-by-run inspection, score distributions, and detailed evaluator assertion results.
  3. **Failures & RCA** (`failures.py`): Automated error taxonomy triage (hallucination, schema failure, timeout, grounding violation).
  4. **Traces** (`traces.py`): Multi-span hierarchical trace waterfall visualization with execution timelines.
  5. **Experiments / Versions** (`experiments.py`): Side-by-side regression comparison between prompt and agent model versions.
  6. **Connect Agent** (`connect_agent.py`): Self-service agent connection wizard with real-time test query verification.
  7. **Agents** (`agents.py`): Agent registry, active versions, and sandboxed AST security inspection summaries.
  8. **Datasets** (`datasets.py`): Benchmark dataset management, test case binding, and batch execution.
  9. **Test Cases** (`test_cases.py`): Test case catalog, ground-truth expectation editor, and on-demand test execution.
  10. **AI Copilot** (`copilot.py`): LLM-assisted failure diagnosis, prompt recommendations, and regression remediation.
  11. **Metrics** (`metrics.py`): Evaluator metric registry and scoring weight sliders.
  12. **RAG Analytics** (`rag_analytics.py`): Retrieval-augmented generation observability (context relevance, recall, and groundedness).
  13. **Tool Analytics** (`tool_analytics.py`): MCP tool invocation logs, argument validation accuracy, and latency breakdown.
  14. **Cost & Performance** (`cost_performance.py`): Token usage tracking, model pricing economics, and budget burn-down.
  15. **Reports** (`reports.py`): Multi-format diagnostic export (Markdown, JSON, and executive audit summaries).

---

## 🚀 Quick Start (Frontend)

```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Launch Streamlit Console
streamlit run dashboard/app.py --server.port 8501
```

Access the live console in your browser at `http://localhost:8501`.