# 🤖 AgentPulse — AI Agents, LLM Judges & Copilot Subsystem
**Branch:** `ai` | **Team:** `HTF26-012-AI-Developers` | **Hack the Future 26**

---

## 📖 Component Overview

The **AI Subsystem** of AgentPulse contains autonomous agent implementations, the Model-as-a-Judge evaluation infrastructure (Anthropic Claude 3.5, OpenAI GPT-4o, and mock fallback judges), and the diagnostic AI Copilot.

### Core Architecture

1. **Autonomous AI Agents** ([`src/agent/`](file:///src/agent/)):
   - `customer_support_agent.py`: Multi-turn stateful conversational agent with policy routing, sentiment checking, and order escalation.
   - `customer_support_tools.py` & `tools.py`: Tool definitions for order lookups, refund processing, inventory checks, and knowledge base search.
   - `demo_agent.py`: Deterministic reference agent for baseline latency and accuracy benchmarking.
   - `custom_agent_template.py`: Boilerplate template for onboarding external LangGraph, CrewAI, AutoGen, or custom Python agents.
   - [`HOW_TO_ADD_YOUR_AGENT.md`](file:///HOW_TO_ADD_YOUR_AGENT.md): Step-by-step developer onboarding manual.

2. **LLM-as-a-Judge Evaluation Engine** ([`src/evaluation/llm_judge.py`](file:///src/evaluation/llm_judge.py), [`src/evaluation/judges/`](file:///src/evaluation/judges/)):
   - **Provider Integrations**:
     - `AnthropicJudge` (`anthropic_judge.py`): Leverages Claude 3.5 Sonnet / Haiku for deep chain-of-thought semantic verification.
     - `OpenAIJudge` (`openai_judge.py`): Leverages GPT-4o for cross-model validation and consistency arbitration.
     - `MockJudge` (`mock_judge.py`): Zero-API-cost deterministic grading engine for local testing, CI pipelines, and offline environments.
   - **Evaluation Criteria**: Groundedness, factual consistency, hallucination risk, safety guardrails, and tone adherence.

3. **Diagnostic AI Copilot** ([`src/analysis/copilot.py`](file:///src/analysis/copilot.py)):
   - Synthesizes failed test runs, stack traces, and tool telemetry.
   - Generates actionable developer recommendations (prompt tweaks, schema adjustments, temperature tuning) to resolve regressions.

4. **Integration Examples** ([`examples/`](file:///examples/)):
   - `quickstart_external_agent.py`: Demonstrates connecting an external agent via webhook or SDK.
   - `verify_sdk_integration.py`: Live integration test script verifying bidirectional telemetry streaming.

---

## 🚀 Running an Agent Demo

```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Run the customer support agent verification
python examples/quickstart_external_agent.py
```