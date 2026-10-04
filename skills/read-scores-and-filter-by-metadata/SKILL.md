---
name: "Read scores and filter by metadata"
description: "after a LangChain vector-store search, and when metadata can drop irrelevant hits."
---

# Read scores and filter by metadata

## Inputs

query, `k`, and an optional metadata dict.

## Steps

1. Build the store from documents, embeddings, and a persist directory. Call `similarity_search_with_score(query, k)`.
2. Treat the returned numbers as distances unless you know that store returns similarity. Closer to 0 is the better match. A farther score such as the demo's about 1.34 was the least relevant.
3. If you need a similarity-style score, he gives `1 / (1 + distance)`.
4. For filtering, pass a dict such as topic equals `database` into `similarity_search` along with `k` (demo used 5). Hits that fail the metadata check are dropped.

## Output

ranked documents, optionally restricted by metadata.

## Failure modes

reading a distance as "higher is better".
