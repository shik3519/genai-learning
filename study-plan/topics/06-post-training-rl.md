# Topic 6: Post-Training & RL — PPO, DPO, GRPO from Scratch

## Core Concepts

### The Post-Training Pipeline
- **Pretrain → SFT → Reward Model → RL (or DPO)**: SFT teaches the model what to say; RL/DPO teaches it what to prefer.
- **Why post-training at all:** pretraining optimizes next-token prediction, not "be a helpful assistant" — post-training closes that gap.

### Reward Modeling
- **Preference data:** pairs of (chosen, rejected) completions for the same prompt.
- **Reward model architecture:** base LM + scalar head, trained to score chosen > rejected (Bradley-Terry style loss).
- **Failure modes:** reward hacking — the policy exploits quirks in the reward model rather than genuinely improving.

### PPO (Proximal Policy Optimization)
- **The objective:** clipped surrogate objective — prevents the policy from moving too far from the reference model in one update.
- **Why clipping matters:** unconstrained policy gradient updates on a reward model's noisy signal are unstable; clipping bounds the step size implicitly.
- **The RLHF loop:** generate completions with the current policy → score with the reward model → compute advantage (often via a value network / GAE) → PPO update → repeat.
- **Practical pain points:** needs a value network (extra model to train), sensitive to hyperparameters, compute-heavy relative to DPO.

### DPO (Direct Preference Optimization)
- **The core trick:** derive a closed-form relationship between the optimal RLHF policy and the reward model, which lets you optimize preferences directly on the policy — no separate reward model, no RL loop.
- **The loss:** a binary cross-entropy-style loss over (chosen, rejected) pairs, referencing log-probabilities under the current policy vs. a frozen reference policy.
- **Why it's simpler:** one training loop, no reward model, no value network, no PPO instability — and it works about as well in practice for most alignment tasks.
- **Where PPO still wins:** when the "preference" isn't static pairwise data but something you can only score by executing an action (agentic tasks, verifiable rewards like code passing tests or math being correct) — DPO needs paired preference data, PPO/GRPO don't.

### GRPO (Group Relative Policy Optimization)
- **What it drops:** the value network. Instead of a learned baseline, GRPO samples a *group* of completions per prompt and uses the group's mean reward as the baseline — advantage is just (reward − group mean).
- **Why it matters for reasoning:** popularized by DeepSeek-R1/DeepSeek-Math for tasks with verifiable rewards (math correctness, code passing tests) where you can cheaply sample many completions and score them exactly, without a learned reward model at all.
- **Tradeoff:** needs multiple samples per prompt (more inference cost per step), but removes an entire network (the value function) and its instability.
- **RLVR (RL with Verifiable Rewards):** the umbrella term (from Lambert's Tülu 3 work) for this whole family — reward comes from programmatic verification (did the code pass? is the math answer right?) instead of a learned reward model.

### The post-GRPO landscape (awareness level, not full implementation)
GRPO successors are proliferating fast as of 2025–2026 — **DAPO, GSPO, GFPO, CISPO** each tweak stability/efficiency of the same core idea (group-relative advantage, no value network). Know that this family exists and roughly what problem each addresses (mostly: training stability at scale, or reducing variance/cost per update) — implementing all of them isn't necessary, but not knowing they exist would be a gap in an interview or in the paper's related-work section.

### Inference-time scaling / reasoning effort control
A distinct but connected 2025–2026 focus area: once a model is post-trained for reasoning (via RLVR/GRPO), how much it "thinks" at inference time becomes a lever of its own — test-time compute scaling, budget forcing, and explicit low/medium/high reasoning-effort modes. Worth knowing conceptually even though the implementation focus this phase is post-training, not serving — it connects directly to Phase 5's vLLM/serving work (reasoning effort is a cost/latency knob in production).

## The Resources

**[rlhfbook.com](https://rlhfbook.com/) — Nathan Lambert's RLHF & Post-Training book + free course**
The primary spine resource for this phase. Free online book (also published by Manning, July 2026) covering instruction tuning, reward modeling, rejection sampling, PPO, direct alignment algorithms (DPO family), GRPO, RLVR/reasoning, and on-policy distillation — plus a companion video course (finished as of August 2026). Use this as the main text; it's more current and complete than piecing the topic together from individual papers.

**Sebastian Raschka — [Build a Reasoning Model From Scratch](https://sebastianraschka.com/) (book, June 2026)**
Hands-on implementation companion for the GRPO/reasoning week — picks up where his "Build a Large Language Model From Scratch" leaves off. Also see his **Ahead of AI** blog posts "Categories of Inference-Time Scaling for Improved LLM Reasoning" and "How LLMs Learn Low-, Medium-, and High-Effort Reasoning Modes" for the inference-time-scaling concepts above.

**Nathan Lambert — [Interconnects newsletter](https://www.interconnects.ai/)**
Best ongoing coverage of post-training research as it evolves — check here for anything newer than the book by the time you reach this phase.

**[HuggingFace TRL docs](https://huggingface.co/docs/trl)** — reference implementations for PPO, DPO, and GRPO trainers. Use these to sanity-check your from-scratch implementations, not as a substitute for writing them.

## Must-Read Papers

- [InstructGPT](https://arxiv.org/abs/2203.02155) — the RLHF pipeline in practice
- [PPO](https://arxiv.org/abs/1707.06347) — sections 1–3, the clipping mechanism
- [DPO](https://arxiv.org/abs/2305.18290) — sections 3–4, the full derivation
- [DeepSeek-Math / GRPO](https://arxiv.org/abs/2402.03300) — the GRPO objective
- [DeepSeek-R1](https://arxiv.org/abs/2501.12948) — GRPO applied to reasoning at scale
- [Rank-K: Test-Time Reasoning for Listwise Reranking](https://arxiv.org/pdf/2505.14432) (2025) — reasoning RL applied directly to reranking; a close precedent for the hybrid RL+retrieval paper angle, worth reading during the topic-survey milestone

## Project

Implement PPO, DPO, and GRPO from scratch on a small LM and benchmark them against each other on the same task — see [week-by-week.md](../week-by-week.md) weeks 7–9 (Phase 2). This is the leading candidate for the technical core of the KDD paper — see [`tracks/research-paper.md`](../tracks/research-paper.md).

## Interview Questions

1. Walk through the RLHF pipeline end to end. What does each stage do?
2. Derive PPO's clipped surrogate objective. Why does clipping stabilize training?
3. Derive DPO from the RLHF objective. What assumption lets you skip the reward model?
4. When would you still reach for PPO/GRPO over DPO?
5. What does GRPO remove compared to PPO, and why does that matter for reasoning tasks with verifiable rewards?
6. What is reward hacking and how do you detect/mitigate it?
7. How would you evaluate whether post-training actually improved the model, beyond the reward model's own score?
8. What is RLVR, and how does it differ from classic RLHF? Name a GRPO successor (DAPO/GSPO/GFPO/CISPO) and what problem it addresses.
9. What is inference-time/test-time compute scaling? How does it interact with what the model learned during post-training?
