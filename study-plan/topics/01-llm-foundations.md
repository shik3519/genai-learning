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

**Alternative/companion — Sebastian Raschka, [Build a Large Language Model From Scratch](https://sebastianraschka.com/blog/) (book)**  
If you want a written, code-first alternative to Karpathy's video (or want both), this covers the same from-scratch implementation ground in more depth, chapter by chapter.

**[The Smol Training Playbook](https://huggingface.co/spaces/HuggingFaceTB/smol-training-playbook) — HuggingFace (Aug 2026)**  
The real, messy story of training SmolLM3 (3B params, 11T tokens) — architecture choices, data decisions, and debugging a run they had to restart after burning 1T tokens. This is the judgment layer Karpathy's video doesn't cover: not "how attention works" but "why we made this specific architecture/data/hyperparameter call, and what broke." Read it as an ongoing companion through Phase 1, not a one-sitting resource. (There's also [The Ultra-Scale Playbook](https://huggingface.co/spaces/nanotron/ultrascale-playbook) on distributed training/GPU parallelism — optional only, since that leans into pretraining-infra depth that's deliberately out of scope for this plan.)

**Nathan Lambert — [Interconnects newsletter](https://www.interconnects.ai/)**  
Ongoing coverage of post-training research. For the implementation-depth material (RLHF, DPO, GRPO, RLVR), see [Topic 6](06-post-training-rl.md) — this week's alignment content is the conceptual primer only.

**Supplement:** [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) — Jay Alammar  
Best visual explanation of attention that exists.

**Stay-current (optional, ongoing):** [Stanford CS25: Transformers United](https://www.youtube.com/playlist?list=PLoROMvodv4rNiJRchCzutFw5ItR_Z27CM) (V6, livestreamed through 2026)  
Guest-lectured seminar tracking where transformer research is heading right now — not core curriculum, but worth skimming recent lecture titles during the paper's topic-survey milestone (weeks 1–8) for novelty ideas.

## Must-Read Papers

- [Attention Is All You Need](https://arxiv.org/abs/1706.03762) (2017) — the original transformer paper
- [InstructGPT](https://arxiv.org/abs/2203.02155) — how RLHF works in practice
- [Chinchilla Scaling Laws](https://arxiv.org/abs/2203.15556) — skim intro + conclusion

## Project

**nanoGPT from scratch** — see [week-by-week.md](../week-by-week.md) weeks 1–5 (Phase 1, primary track).

## Interview Questions

1. Walk me through the attention mechanism. What are Q, K, and V?
2. Why does multi-head attention work better than single-head?
3. What is the role of the residual stream in a transformer?
4. What is BPE tokenization and what are its tradeoffs?
5. Explain the difference between RLHF and DPO. Why do people prefer DPO?
6. What are scaling laws? How do they inform model training decisions?
7. What is the KV cache and when does it become a bottleneck?
8. How does temperature affect text generation? What happens at temperature 0?
