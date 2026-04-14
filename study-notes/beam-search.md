# Beam Search

## The Problem with Greedy Decoding

Greedy decoding picks the single highest-probability token at each step. It's locally optimal but globally suboptimal — an early choice can close off better long-term sequences.

```
"The cat sat on the ___"

Greedy picks "mat" (prob 0.4) → commits to a mediocre continuation
"roof" (prob 0.35) might lead to a much higher joint-probability sequence
```

---

## How Beam Search Works

Keep the top-k partial sequences (**beams**) alive simultaneously. At each step, expand every beam across the full vocabulary, score all candidates, and keep only the top-k.

**beam width = 3 example:**

```
Start: [""]

Step 1 — expand, keep top 3:
  Beam 1: "The"   score = log(0.4)
  Beam 2: "A"     score = log(0.3)
  Beam 3: "Once"  score = log(0.2)

Step 2 — expand all 3, get 3×vocab candidates, keep top 3:
  Beam 1: "The cat"   score = log(0.4) + log(0.6)
  Beam 2: "The dog"   score = log(0.4) + log(0.3)
  Beam 3: "A cat"     score = log(0.3) + log(0.5)
```

Scores are **summed log-probabilities** (log of joint probability) — avoids floating-point underflow from multiplying many small numbers.

---

## Connection to `torch.gather`

At each step, surviving beams may come from different parent beams. `gather` is used to pull the correct history (past key/value states) forward:

```python
# logits: (beam_width, vocab_size)
log_probs = F.log_softmax(logits, dim=-1)

# beam_indices: which parent beam each surviving candidate came from
# Retrieve the right KV cache entries for the next step
past_keys = torch.gather(past_keys, dim=0, index=beam_indices)
```

`topk` picks the candidates, `gather` reorders history to match.

---

## Key Hyperparameter: Beam Width

| Width | Behavior |
|-------|----------|
| 1 | Equivalent to greedy decoding |
| 4–10 | Typical for translation / summarization |
| Large | Higher quality, but O(beam_width × vocab_size) compute per step |

---

## Failure Modes

**Length bias** — longer sequences accumulate more (negative) log-probs, so short outputs win unfairly.  
Fix: divide score by sequence length (length normalization).

**Repetition** — repeated tokens are often high-probability, causing loops like "the the the...".  
Fix: n-gram blocking, repetition penalty.

**Diversity collapse** — all beams converge to near-identical outputs.  
Fix: diverse beam search adds a dissimilarity penalty across beams.

---

## When to Use (and Not Use)

**Good fit:** translation, summarization, constrained code generation — tasks with a more objectively correct output. Beam search maximizes joint probability, which works well here.

**Poor fit:** open-ended generation (chat, creative writing). Maximizing probability produces bland, safe text. Prefer sampling (top-p, temperature) instead.
