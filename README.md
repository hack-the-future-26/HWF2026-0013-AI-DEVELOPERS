# 🧪 AgentPulse — Testing, QA & Automated CI/CD Pipelines
**Branch:** `testing` | **Team:** `HTF26-012-AI-Developers` | **Hack the Future 26**

---

## 📖 Component Overview

The **Testing & QA Subsystem** of AgentPulse maintains rigorous test coverage, automated regression detection, and continuous integration workflows. The suite contains **249 tests** across 27 distinct test modules covering core engines, LLM judges, evaluators, MCP observability, security hardening, and data persistence.

### Test Suite Architecture ([`tests/`](file:///tests/))

| Category | Test Modules | Focus |
|---|---|---|
| **Core & Engine** | `test_core_engine.py`, `test_batch_runner.py` | Agent execution loop, step capture, async pipeline |
| **Evaluators** | `test_evaluators.py`, `test_hackathon_evaluators.py` | Deterministic exact match, regex, keyword, schema checks |
| **LLM Judges** | `test_llm_judge.py`, `test_rag_evaluators.py` | Model-graded semantic evaluation, grounding, faithfulness |
| **Tool & MCP** | `test_tool_evaluators.py`, `test_mcp_observability.py` | Tool accuracy, argument schemas, MCP protocol spans |
| **Failure & RCA** | `test_failure_analysis.py`, `test_root_cause_analysis.py` | Automated failure taxonomy classification & clustering |
| **Scoring & Cost** | `test_weighted_scoring.py`, `test_cost_calculator.py` | Quality matrices, token accounting, pricing engines |
| **Security & Sandbox**| `test_security_hardening.py`, `test_sandbox.py`, `test_env_validator.py` | AST code inspection, subprocess isolation, authorization gates |
| **Datasets & Registry**| `test_dataset_manager.py`, `test_test_case_manager.py`, `test_registry.py` | Benchmark suites, test case fixtures, version tracking |
| **Telemetry & SDK**| `test_observe_sdk.py`, `test_tracer_hierarchy.py`, `test_sdk.py` | Zero-overhead SDK decorator, span propagation, hierarchy |

### Automated Scripts ([`scripts/`](file:///scripts/))

- `run_eval.py`: Automated command-line evaluation runner.
- `seed_demo_data.py`: Pre-populates database with synthetic multi-turn customer support runs and ground-truth assertions.
- `run_customer_support_demo.py`: End-to-end live agent demo runner.

### CI/CD Workflow ([`.github/workflows/`](file:///.github/workflows/))

- Automated GitHub Actions test pipeline (`ci.yml`) triggered on pull requests and pushes across Python 3.10, 3.11, and 3.12.

---

## 🚀 Running the Test Suite

```bash
# Install dependencies
pip install -r requirements.txt

# Run all 249 tests
pytest tests/ -v

# Run with coverage report
pytest tests/ --cov=src --cov-report=term-missing
```