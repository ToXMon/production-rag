---
name: "Cache embedding calls and repeated answers"
description: "the same text is embedded twice, or the same question is asked again."
---

# Cache embedding calls and repeated answers

## Inputs

an embedding model or a chat model; a store; for answers, a TTL or a similarity threshold.

## Steps

1. Embedding cache: `CacheBackedEmbeddings.from_bytes_store` (import path he landed on: `langchain_classic` storage `LocalFileStore` and classic embeddings cache) with the underlying embeddings, a namespace, and a local directory. First `embed_documents` hits the API; the second returns the cached vectors. He says this classic path is deprecated by December 2026 and the concept remains.
2. Exact answer cache: normalize case and whitespace, hash (MD5 in the semantic-cache sketch; SHA-256 in the later API cache), store the response. "What is Python?" and "what is python?" share a key. "Tell me about Python" does not.
3. For real semantic cache he says to embed the query, search prior queries, and return on similarity above a threshold. Example he gives: 0.95. The class in the video is only the exact-match starting point.
4. Wrapper flow: on hit, return without a model call; on miss, call, store, return. Demo stats: 2 hits, 3 misses, 40 percent hit rate. He says 30 to 50 percent is typical in production for repeated support questions.

## Output

identical vectors or a reused answer, plus hit/miss counters.

## Failure modes

exact hash misses paraphrases. In-memory caches do not share across instances (later skill: move to Redis).
