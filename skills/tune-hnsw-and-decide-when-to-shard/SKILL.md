---
name: "Tune HNSW and decide when to shard"
description: "queries slow down or accuracy drops as the index grows into the hundreds of thousands or millions. He says Pinecone, pgvector, Chroma, and Qdrant use HNSW or something similar."
---

# Tune HNSW and decide when to shard

## Inputs

index build parameters `M` and `ef_construction`; query parameter `ef_search`.

## Steps

1. `M` is connections per node. Low `M` about 8 to 16: smaller index, faster builds, lower accuracy. Default he cites is 16. High `M` about 32 to 64: larger index, slower builds, higher accuracy.
2. `ef_search` is the candidate-list size. Low about 32 to 64: faster, less accurate. Default band about 64 to 128. High about 200 to 500: slower, more accurate.
3. You cannot maximize accuracy, speed, and small memory together. His starting points: prototype `M=16`, `ef_search=40`; production `M=16`, `ef_search=100`; high accuracy `M=32`, `ef_search=200`.
4. pgvector sketch he shows: HNSW index on the embedding with cosine ops, `m=16`, `ef_construction=64`; at query time set `hnsw.ef_search` to 100. Chroma: collection metadata `hnsw:M` set to 16. Pinecone: he says you do not set these; you control `top_k`.
5. If queries exceed about 100 ms, add RAM or shard. If inserts spike, scale writes separately. If memory errors, bigger instance or shard. If accuracy drops, raise `ef_search` or shard.
6. Try vertical scaling first while under about 5 to 10 million vectors. Shard (horizontal) past about 10 million. Most apps do not need sharding.
7. Host choice he gives: under 1 million vectors, a single pgvector is enough; if there is no DevOps team, use Pinecone; if cost is the priority and you can operate it, self-host.

## Output

an index configuration and a scale decision.

## Failure modes

raising `M` and `ef_search` together spends memory and latency; lowering either spends accuracy.
