---
name: "Embed with an embedding model, not a chat model"
description: "indexing and querying."
---

# Embed with an embedding model, not a chat model

## Inputs

text or a list of strings; one embedding model name.

## Steps

1. Do not call chat completions for vectors. Call the embeddings API (`embeddings.create` in the OpenAI client example) with `text-embedding-3-small` or another embedding model. Input is text; output is a vector.
2. For one string use `embed_query`. For many strings use `embed_documents`.
3. Use that same model and version for indexing and for query embedding. If you switch models, vectors are not comparable and search fails.
4. Optional check: vector length (1536 for `text-embedding-3-small` in the demo) and L2 norm. He says OpenAI embeddings are normalized to about 1.0 so longer documents do not get larger vectors only because they are longer. If the norm is not 1, that model did not normalize.
5. A from-scratch ranker he shows: embed documents and the query, compute cosine similarity, sort.

## Output

vectors stored with the original text, or a ranked list.

## Failure modes

embedding the query with a different model than the index; blaming the chat model when the retrieved chunks are already wrong. He says about 90% of RAG failures are retrieval failures, not generation failures, and to test retrieval before blaming the LLM.
