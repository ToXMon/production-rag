---
name: "Prepend document context before embedding"
description: "chunks say \"the company\" or \"they\", titles and headers carry the entity, or documents come from multiple sources. Anthropic's contextual retrieval, late 2024, as he presents it."
---

# Prepend document context before embedding

## Inputs

full document, document title, one chunk, a chat model, then an embedding model.

## Steps

1. For each chunk, prompt the model with the title, the document, and the chunk, and ask for a short context prefix (section and entity).
2. Store and embed the prefix plus the chunk, not the raw chunk.
3. Build a second vector store of the original chunks and compare similarity search with scores on the same questions.

## Output

contextualized chunks. In his Acme demo the contextual store scored better by about 56 percent, 61.4 percent, and 50.6 percent on three questions. He also cites Anthropic: about 49 percent fewer top-20 retrieval failures alone, about 67 percent when combined with reranking.

## Failure modes and costs he states

about 1 to 5 cents per document, once, at index time; extra latency per chunk while indexing; chunks about 20 to 30 percent larger. Benchmarks will not match your corpus; test. Reranking is named as the combination that reaches 67 percent; how to call a reranker is not specified.
