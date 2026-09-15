# 🧠 AgentPulse — Machine Learning, RAG Metrics & Regression Analytics
**Branch:** `ml` | **Team:** `HTF26-012-AI-Developers` | **Hack the Future 26**

---

## 📖 Component Overview

The **Machine Learning Subsystem** of AgentPulse handles semantic similarity calculations, RAG (Retrieval-Augmented Generation) groundedness metrics, multi-objective score optimization, and statistical model regression analytics.

### Core Architecture

1. **Semantic Metrics & NLP Correctness** ([`src/evaluation/metrics.py`](file:///src/evaluation/metrics.py)):
   - **Semantic Distance**: Vector embeddings and cosine similarity scoring between model outputs and ground truth answers.
   - **Lexical & Token Overlap**: Token-level F1, ROUGE-L, and normalized substring matching.
   - **Probabilistic Accuracy**: Calibrated confidence scores with dynamic threshold gating.

2. **RAG Faithfulness & Retrieval Metrics** ([`src/evaluation/rag_evaluators.py`](file:///src/evaluation/rag_evaluators.py)):
   - **Context Groundedness**: Measures whether agent assertions are strictly derived from retrieved reference contexts or hallucinated.
   - **Context Relevance**: Measures noise-to-signal ratio within retrieved chunks.
   - **Answer Relevancy**: Quantifies semantic alignment between the user's question and the generated answer.

3. **Multi-Objective Optimization Scoring** ([`src/evaluation/scoring.py`](file:///src/evaluation/scoring.py)):
   - Configurable weighted balance across 6 evaluation dimensions:
     - `Task Success` (0.30 weight)
     - `Tool Accuracy` (0.20 weight)
     - `Groundedness` (0.20 weight)
     - `Answer Quality` (0.15 weight)
     - `Latency Budget` (0.10 weight)
     - `Cost Budget` (0.05 weight)
   - Specialized scoring profiles: `Quality-First`, `Efficiency-Optimized`, and `Balanced`.

4. **Statistical Regression Analytics** ([`src/analysis/regression.py`](file:///src/analysis/regression.py)):
   - Side-by-side comparative analytics evaluating performance delta ($\Delta$) between baseline agent versions and candidate releases.
   - Z-score anomaly detection flags regressions in latency distributions and quality degradation.

5. **Token Consumption & Cost Modeling** ([`src/cost/analytics.py`](file:///src/cost/analytics.py)):
   - Token growth regression curves and predictive inference cost modeling across workload scales.

6. **Ground-Truth Benchmark Datasets** ([`src/dataset/`](file:///src/dataset/)):
   - Golden benchmark datasets (`golden_tasks.json`, `knowledge_base.json`, `customer_support_kb.json`, `customer_support_tasks.json`).

---

## 🚀 Running Semantic & RAG Evaluations

```python
from src.evaluation.rag_evaluators import ContextGroundednessEvaluator
from src.evaluation.scoring import ScoringConfig, calculate_case_scores

# 1. Evaluate context groundedness
evaluator = ContextGroundednessEvaluator()
result = evaluator.evaluate(
    prediction="The return window is 30 days.",
    context="Returns are accepted within 30 days of delivery.",
)
print(f"Groundedness Score: {result.score:.2f} (Passed: {result.passed})")
```