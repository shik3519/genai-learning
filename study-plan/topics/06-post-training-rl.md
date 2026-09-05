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

## The Resources

**Nathan Lambert — [YouTube channel](https://www.youtube.com/@natolambert) + [Interconnects newsletter](https://www.interconnects.ai/)**
Best ongoing coverage of post-training research — RLHF, DPO, reward modeling, and the reasoning-RL wave (GRPO and successors).

**[HuggingFace TRL docs](https://huggingface.co/docs/trl)** — reference implementations for PPO, DPO, and GRPO trainers. Use these to sanity-check your from-scratch implementations, not as a substitute for writing them.

## Must-Read Papers

- [InstructGPT](https://arxiv.org/abs/2203.02155) — the RLHF pipeline in practice
- [PPO](https://arxiv.org/abs/1707.06347) — sections 1–3, the clipping mechanism
- [DPO](https://arxiv.org/abs/2305.18290) — sections 3–4, the full derivation
- [DeepSeek-Math / GRPO](https://arxiv.org/abs/2402.03300) — the GRPO objective
- [DeepSeek-R1](https://arxiv.org/abs/2501.12948) — GRPO applied to reasoning at scale

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
