---
name: "Cut vector-search cost without a new vendor"
description: "after a workload exists, not before the first prototype. He says start managed, and self-host when the bill matters."
---

# Cut vector-search cost without a new vendor

## Inputs

current dimension, query rate, repeat rate, instance size.

## Steps

1. Reduce dimensions. Example: `text-embedding-3-small` from 1536 to 512 via the embeddings `dimensions` argument. He claims about 30 to 60 percent savings at low effort. Re-embed; mixed dimensions are not comparable.
2. Quantize float32 to int8 or binary. He claims about 50 to 75 percent savings, medium effort.
3. Batch queries instead of one HTTP call each. He claims about 10 to 30 percent where the SDK supports it.
4. Cache repeated searches: hash the query (demo uses MD5) and skip the similarity call on a hit. If 20 percent of queries repeat, he says you save about 20 percent of that compute. Overall cache savings he cites: about 10 to 40 percent.
5. Start on a small instance, measure, and scale only at a real limit. Review monthly. He claims about 20 to 50 percent versus over-provisioning.

## Output

a lower bill at the same retrieval approach.

## Failure modes

premature optimization. Dimension cuts and quantization are quality tradeoffs he does not quantify beyond "keeping quality" for int8.
