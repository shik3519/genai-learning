# Topic 4: Fine-Tuning & Model Adaptation

## Core Concepts

### When to Fine-Tune
- **Fine-tune when:** consistent format/style, domain vocabulary, task that can't be prompted reliably
- **Don't fine-tune when:** RAG or prompting would work — fine-tuning is more expensive and slower to iterate
- **Full SFT vs LoRA:** full fine-tuning updates all parameters (expensive); LoRA freezes base and trains small adapters

### LoRA & QLoRA
- **LoRA mechanics:** decompose weight update ΔW into two small matrices A·B (rank r ≪ d); only A and B are trained
- **Why it works:** most useful weight updates live in a low-dimensional subspace
- **QLoRA:** quantize the frozen base model to 4-bit (NF4) to save GPU memory; train adapters in 16-bit
- **Practical outcome:** fine-tune a 7B model on a single 24GB GPU (e.g. RTX 3090/4090)
- **DPO vs SFT:** SFT teaches the model what to say; DPO teaches it what to prefer — better for alignment tasks

### Dataset Preparation
- **Instruction tuning format:** `{"instruction": ..., "input": ..., "output": ...}` (Alpaca format)
- **Data quality > quantity:** LIMA showed 1000 high-quality examples beats 50k noisy ones
- **Train/eval split:** always hold out 10–15% for evaluation; never leak into training

### Evaluation
- **Before/after benchmark:** pick 20–50 task-specific prompts; score base vs fine-tuned side by side
- **Perplexity:** lower = model assigns higher probability to correct answers (but can be gamed)
- **Task-specific metrics:** accuracy, ROUGE, or LLM-as-judge depending on the task

### Inference Optimization
- **Quantization:** INT8 (small quality loss) → INT4 (noticeable on small models) — use for serving
- **GGUF format:** `llama.cpp` format for CPU inference; good for demos and local testing
- **vLLM:** production serving with PagedAttention — see [05-eval-production.md](05-eval-production.md)

## The One Resource

**[HuggingFace PEFT docs — LoRA quickstart](https://huggingface.co/docs/peft/quicktour)**  
The authoritative hands-on guide. Covers LoRA, QLoRA, and merging adapters.

**Course:** [DeepLearning.AI: Finetuning Large Language Models](https://www.deeplearning.ai/short-courses/finetuning-large-language-models/) (free, 4hr)

## Must-Read Papers

- [LoRA](https://arxiv.org/abs/2106.09685) — read intro + section 2 (the math is accessible)
- [QLoRA](https://arxiv.org/abs/2305.14314) — read intro + section 3 (the 4-bit trick)
- [LIMA](https://arxiv.org/abs/2305.11206) — short paper proving data quality > quantity

## Key Libraries

| Library | Use |
|---------|-----|
| `peft` | LoRA/QLoRA — HuggingFace standard |
| `bitsandbytes` | 4-bit/8-bit quantization |
| `axolotl` | Config-driven fine-tuning wrapper |
| `trl` | SFT trainer, DPO trainer |
| `wandb` | Experiment tracking |
| `llama.cpp` | Local GGUF inference |

## Project

**P4 — LoRA Fine-Tuned Model + Benchmark** — see [week-by-week.md](../week-by-week.md) weeks 13–14.  
Push the adapter to HuggingFace Hub with a model card. The before/after benchmark is the portfolio piece.

## Interview Questions

1. Explain LoRA mathematically. Why does low-rank decomposition work?
2. What is QLoRA and what problem does it solve?
3. When would you fine-tune instead of using RAG or better prompting?
4. What is instruction tuning? How does the Alpaca format work?
5. How do you prevent catastrophic forgetting when fine-tuning?
6. What is DPO and how is it different from RLHF/PPO?
7. How do you evaluate whether a fine-tuned model is actually better?
8. What is the tradeoff between INT4 and INT8 quantization?
