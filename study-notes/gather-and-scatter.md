# Gather and Scatter

## `torch.gather` — Read from Indexed Positions

For each position in `index`, go to that position along `dim` in `source` and pull the element out.

**Output shape always matches `index` exactly.**

```python
values = torch.tensor([
    [10., 20., 30., 40.],
    [50., 60., 70., 80.],
    [90., 100., 110., 120.],
])  # (3, 4)

indices = torch.tensor([[2], [0], [3]])  # (3, 1)

gathered = torch.gather(values, dim=1, index=indices)
# [[30.], [50.], [120.]]
```

`dim=1` means index numbers refer to columns — each row picks a different column.

**The mental model:**
```python
# equivalent loop:
output[i][j] = values[i][index[i][j]]   # dim=1
```

**Why not just slice?** `values[:, 2]` picks the same column for every row. `gather` lets each row pick a *different* column.

**Common uses:** beam search (retrieve history for surviving beams), attention (index value vectors), top-k selection follow-up lookups.

---

## `torch.scatter_add_` — Write (Accumulate) into Indexed Positions

The inverse of gather — instead of reading from indexed positions, it adds source values *into* indexed positions.

```python
group_sums = torch.zeros(3, 2)          # (num_groups, embed_dim)
embeddings = torch.tensor([             # (5, 2) — 5 tokens
    [1.0, 0.0],  # group 0
    [2.0, 0.0],  # group 0
    [0.0, 3.0],  # group 1
    [0.0, 1.0],  # group 1
    [5.0, 5.0],  # group 2
])
ids_expanded = torch.tensor([           # (5, 2) — same shape as embeddings
    [0, 0], [0, 0], [1, 1], [1, 1], [2, 2]
])

group_sums.scatter_add_(0, ids_expanded, embeddings)
# group_sums = [[3.0, 0.0],   ← token 0 + token 1
#               [0.0, 4.0],   ← token 2 + token 3
#               [5.0, 5.0]]   ← token 4
```

`dim=0` means the index refers to which **row** to write into.

**The mental model:**
```python
# equivalent loop:
self[index[i][j]][j] += source[i][j]   # dim=0
```

**Why `ids_expanded` must match `embeddings` shape:** every element of the source needs its own destination index. A 1D group id `[0, 0, 1, 1, 2]` must be expanded to `(5, 2)` so each of the 10 values has an explicit target row.

**The trailing `_`:** in-place operation — modifies `group_sums` directly.

---

## Gather vs Scatter: The Duality

```
gather:        output[i][j] = source[i][index[i][j]]   ← read from indexed location
scatter_add_:  self[index[i][j]][j] += source[i][j]    ← write into indexed location
```

| | gather | scatter_add_ |
|---|---|---|
| Direction | many positions → output | source → many positions |
| Operation | select | accumulate |
| Output shape | matches `index` | matches `self` (destination) |
| Analogy | look up | group by + sum |

**Used together in:**
- **Attention**: scatter to aggregate by group, gather to retrieve per-query results
- **Graph neural networks**: scatter neighbor features into node aggregations
- **Beam search**: gather KV-cache rows to match surviving beam order
