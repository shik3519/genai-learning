# Topic 1: LLM Foundations & Architecture

## Core Concepts

- **Transformer architecture:** self-attention, multi-head attention, MLP layers, residual stream
- **Attention mechanism:** Q/K/V matrices — what they represent and why dot-product attention works
- **Positional encoding:** why order matters and how it's injected
- **Tokenization:** BPE — how text becomes integers; vocabulary size tradeoffs
- **Autoregressive generation:** next-token prediction, temperature, top-p, top-k sampling
- **Context window & KV cache:** what limits context length; how KV cache speeds up inference
- **Pre-training vs fine-tuning:** self-supervised next-token prediction vs supervised adaptation
- **RLHF & DPO:** how models are aligned to human preferences; why DPO replaced PPO for most tasks
- **Scaling laws:** bigger model + more data = predictable improvement (Chinchilla)
- **Model families:** GPT (decoder-only) vs BERT (encoder-only) vs T5 (encoder-decoder); MoE

## The Two Resources

**Andrej Karpathy — [Let's Build GPT](https://youtu.be/kCc8FmEb1nY) (YouTube, 2hr)**  
Best resource for transformer architecture + implementation. Watch actively — pause, implement, re-watch.

**Nathan Lambert — [YouTube channel](https://www.youtube.com/@natolambert) + [Interconnects newsletter](https://www.interconnects.ai/)**  
Best resource for post-training: RLHF, DPO, reward modeling, preference learning, alignment. Clearer than any paper on why the post-training pipeline works the way it does.

**Supplement:** [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) — Jay Alammar  
Best visual explanation of attention that exists.

## Must-Read Papers

- [Attention Is All You Need](https://arxiv.org/abs/1706.03762) (2017) — the original transformer paper
- [InstructGPT](https://arxiv.org/abs/2203.02155) — how RLHF works in practice
- [Chinchilla Scaling Laws](https://arxiv.org/abs/2203.15556) — skim intro + conclusion

## Project

**nanoGPT from scratch** — see [week-by-week.md](../week-by-week.md) weeks 1–2.

## Interview Questions

1. Walk me through the attention mechanism. What are Q, K, and V?
2. Why does multi-head attention work better than single-head?
3. What is the role of the residual stream in a transformer?
4. What is BPE tokenization and what are its tradeoffs?
5. Explain the difference between RLHF and DPO. Why do people prefer DPO?
6. What are scaling laws? How do they inform model training decisions?
7. What is the KV cache and when does it become a bottleneck?
8. How does temperature affect text generation? What happens at temperature 0?
