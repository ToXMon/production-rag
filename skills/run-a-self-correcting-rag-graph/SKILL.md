---
name: "Run a self-correcting RAG graph"
description: "complex questions that may need a rewrite, high-stakes or user-facing apps, mixed document types (legal, guides, instructions). He says a simple prototype does not need it."
---

# Run a self-correcting RAG graph

## Inputs

a Chroma store, a chat model, a max retry count (demo: 2).

## Steps

1. State dict: query, rewritten query, documents, generation, relevance score, retry count, max retries, and the vector store.
2. Nodes: retrieve (`as_retriever` then `invoke`), grade (an LLM scores each document and averages; drop zeros), rewrite (an LLM rewrites the query and increments retries), generate, and a fallback that says it could not find relevant information.
3. `StateGraph` entry is retrieve, then an edge to grade. Conditional edge from grade: good relevance goes to generate; low relevance with retries left goes to rewrite; no documents or retries exhausted goes to fallback. Rewrite edges back to retrieve. Generate and fallback edge to end.
4. Invoke with retry count 0. Cap retries so a miss cannot loop forever.

## Output

a generated answer, or the fallback string after the cap.

## Demo he walks

an install question about LangGraph grades about 0.67, keeps 2 of 3 documents, and generates. A question about making pizza grades 0, rewrites twice, then falls back because the corpus has no such content.

## Failure modes

each retry spends embedding and chat tokens. Traditional one-shot RAG cannot do this loop. LangGraph is what he uses because the flow is cyclic.
