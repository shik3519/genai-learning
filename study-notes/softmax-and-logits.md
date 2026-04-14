# Softmax and Logits

## Logits

Raw, unnormalized scores output by a model's final layer — before any probability conversion. They can be any real number (positive, negative, large, small).

```python
logits = [2.0, 1.0, 0.1]  # raw scores for 3 classes
```

The name comes from **log-odds** (logistic regression), but in modern deep learning it loosely means "pre-activation scores."

---

## Softmax

A function that converts logits into a **probability distribution** (values between 0–1 that sum to 1).

$$\text{softmax}(x_i) = \frac{e^{x_i}}{\sum_j e^{x_j}}$$

```python
import numpy as np

logits = [2.0, 1.0, 0.1]
exp = np.exp(logits)           # [7.39, 2.72, 1.11]
probs = exp / exp.sum()        # [0.659, 0.242, 0.099]
# sums to 1.0 ✓
```

**Key properties:**
- Larger logit → larger probability (order preserved)
- Exponentiation **amplifies differences** — the largest logit dominates
- Temperature scaling: divide logits by `T` before softmax
  - `T < 1` → sharper/more confident distribution
  - `T > 1` → flatter/more uniform distribution (used in sampling)

---

## In LLMs specifically

At each generation step:
1. Model outputs **logits** — one score per token in vocabulary (~50k tokens)
2. **Softmax** converts them to probabilities
3. A token is **sampled** from that distribution (or argmax for greedy decoding)

```
logits (vocab_size,) → softmax → probabilities → sample → next token
```

This is why `temperature` affects "creativity" — it reshapes the probability distribution before sampling.

---

## Numerically Stable Softmax

Standard softmax is $\frac{e^{x_i}}{\sum_j e^{x_j}}$. The problem: `exp()` of large logits overflows to `inf`.

```python
torch.exp(torch.tensor(1000.0))  # → inf
```

### The Stability Trick

Subtract the row maximum before exponentiating. Mathematically identical, numerically safe:

$$\frac{e^{x_i - c}}{\sum_j e^{x_j - c}} = \frac{e^{x_i} \cdot e^{-c}}{\sum_j e^{x_j} \cdot e^{-c}} = \frac{e^{x_i}}{\sum_j e^{x_j}}$$

The $e^{-c}$ cancels out — the result is the same, but now the largest value in each row always exponentiates to $e^0 = 1$ instead of $e^{1000}$.

### Line by Line

```python
logits = torch.randn(2, 5)           # (2, 5) — 2 rows, 5 logits each

max_vals = logits.max(dim=-1,        # find max per row → (2,)
           keepdim=True).values      # keepdim=True keeps shape as (2, 1)
                                     # so it can broadcast against (2, 5)

stable_exp = torch.exp(logits        # (2, 5) - (2, 1) broadcasts to (2, 5)
                       - max_vals)   # largest value per row → exp(0) = 1

softmax = stable_exp /               # (2, 5) / (2, 1) → (2, 5)
  stable_exp.sum(dim=-1,             # sum across columns per row → (2,)
                 keepdim=True)       # keepdim=True → (2, 1) for broadcast
```

**Why `keepdim=True` matters:** without it, `max` and `sum` return shape `(2,)`. Subtracting/dividing `(2, 5)` by `(2,)` would fail or broadcast wrong. Keeping the dimension as `(2, 1)` lets it broadcast cleanly across all 5 columns.
