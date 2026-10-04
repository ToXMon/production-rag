---
name: "Add hybrid BM25 plus vector search"
description: "production queries that include SKUs, acronyms (WCAG example), error codes (the intended example is a connection-refused code; captions say \"econ refuse\"), or exact names. Skip it for simple Q&A, creative chat, or a throwaway prototype."
---

# Add hybrid BM25 plus vector search

## Inputs

the same documents for both retrievers; a weight pair; `k`.

## Steps

1. Vector retriever: `as_retriever`, top 3 in the demo. Good at synonyms and natural questions; bad at exact codes.
2. BM25 retriever: `BM25Retriever.from_documents`. No embedding argument. Install `rank-bm25`. Good at exact and rare terms; bad at synonyms.
3. Fuse with weighted reciprocal rank fusion. LangChain's `EnsembleRetriever` was gone from the SDK in the recording, so he inlined the same algorithm. Start weights at 50/50. Shift toward the vector retriever (example 0.3 BM25 / 0.7 vector) for semantic queries, or toward BM25 (0.7 / 0.3) for codes and ids.
4. On every `add_documents`, rebuild the BM25 retriever from the full document set. BM25 does not take incremental updates.
5. He recommends retrieving about 4 documents and letting RRF sort them. Budget an extra about 20 to 50 ms versus one search.

## Output

one ranked list. A document that is only rank 1 in BM25 can still lose to a document that is rank 3 in both.

## Failure modes

stale BM25 index after inserts; assuming the fused list is a simple concatenation.
