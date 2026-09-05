# Topic 5: Evaluation, Observability & Production

## Core Concepts

### LLM Evaluation
- **The problem:** LLM outputs are open-ended — no single ground-truth metric works universally
- **LLM-as-judge:** use a stronger LLM (GPT-4, Claude Opus) to score outputs on rubrics — surprisingly reliable
- **RAGAS metrics** (for RAG systems):
  - *Faithfulness:* is the answer grounded in the retrieved context?
  - *Answer relevancy:* does the answer address the question?
  - *Context recall:* did retrieval surface the right documents?
- **Benchmark suites:** MMLU (knowledge), HellaSwag (reasoning), HumanEval (coding) — use to compare models
- **Task-specific evals:** design your own for your domain — 50 labeled examples is usually enough to start
- **Regression testing:** run evals on every code/prompt change to catch quality drops early

### Observability & Tracing
- **Traces:** record every LLM call — input, output, latency, tokens, cost — for debugging and analytics
- **Spans:** in agentic systems, each agent step is a span inside the trace
- **Prompt versioning:** track which prompt version produced which output — essential for A/B testing
- **Langfuse:** open-source observability stack — traces, prompt management, dashboards — the default choice
- **LangSmith:** tight LangChain integration — good if already in the LangChain ecosystem

### Production Serving
- **vLLM:** production-grade server for open-source models; uses PagedAttention for high throughput
  - PagedAttention: allocates KV cache in non-contiguous pages → eliminates fragmentation → more concurrent requests
  - Continuous batching: dynamically adds new requests to in-flight batches → GPU utilization stays high
- **LiteLLM:** unified API proxy over 100+ models — swap providers without changing client code
- **Quantization in serving:** INT8 for quality-sensitive tasks; INT4 (GGUF) for demos and local use
- **Caching:** semantic cache (GPTCache) — cache LLM responses for similar queries; big cost win
- **Cost optimization:** prompt caching (Anthropic) + model routing (cheap model first, escalate) + batching

### Safety & Guardrails
- **Prompt injection:** attacker injects instructions via user content to override system prompt — defense: input sanitization + output validation
- **PII detection:** use `presidio` to redact before sending to LLM APIs
- **Output filtering:** NeMo Guardrails or custom regex/classifier for content moderation
- **OWASP LLM Top 10:** the standard security checklist for LLM applications — know it

## The One Resource

**[Langfuse docs](https://langfuse.com/docs)** — tracing quickstart + prompt management section  
Best observability tool for the price (free self-hosted). Learn it deeply.

**For serving:** [vLLM documentation](https://docs.vllm.ai/en/latest/) — quickstart + architecture overview

## Must-Read Papers

- [Judging LLM-as-a-Judge](https://arxiv.org/abs/2306.05685) — how to use LLMs as evaluators; biases to watch for
- [PagedAttention / vLLM](https://arxiv.org/abs/2309.06180) — read abstract + section 2

## Key Libraries

| Library | Use |
|---------|-----|
| `ragas` | RAG evaluation (faithfulness, relevancy) |
| `langfuse` | Tracing + observability + prompt mgmt |
| `promptfoo` | Automated LLM testing / regression suite |
| `vllm` | Production LLM serving |
| `litellm` | Unified API proxy |
| `presidio` | PII detection + redaction |
| `fastapi` | API serving layer |

## Projects

**Eval harness on P2 (RAG system)** — week 15:  
- RAGAS metrics on 50 Q&A pairs
- LLM-as-judge scoring pipeline
- Langfuse tracing dashboard
- Eval script that runs on every commit

**Production deployment** — weeks 16–17:  
- Dockerize P2, deploy to Modal or HF Spaces
- Serve P4 fine-tuned model with vLLM

## Interview Questions

1. How does LLM-as-judge work? What are its failure modes?
2. What RAGAS metrics would you use to evaluate a RAG system? What do they measure?
3. Explain PagedAttention. Why does it increase throughput?
4. How do you detect a quality regression in an LLM system after a prompt change?
5. What is continuous batching and why does it matter for GPU utilization?
6. How would you reduce LLM API costs by 50% in production?
7. What is prompt injection and how do you defend against it?
8. How would you design an eval pipeline for a chatbot that catches regressions automatically?
