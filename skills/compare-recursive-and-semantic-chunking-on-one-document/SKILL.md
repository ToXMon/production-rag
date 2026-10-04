---
name: "Compare recursive and semantic chunking on one document"
description: "before adopting semantic chunking as the default."
---

# Compare recursive and semantic chunking on one document

## Inputs

one document with known topics; both splitters; the same embedding model and queries.

## Steps

1. Install LangChain, LangChain OpenAI, Chroma, and `langchain-experimental` (semantic chunker lived there).
2. Recursive splitter: demo chunk size 400 and overlap 50, separators for blank lines, newlines, and sentence punctuation. `split_text`.
3. `SemanticChunker` with the embeddings, breakpoint type `percentile`, threshold amount 90.
4. Build two Chroma collections and run the same queries with `k=1`.
5. His later helper, `smart_chunker`, tries semantic first and falls back to recursive, then checks chunk size and errors. He still says to prefer semantic as primary for most corpora.

## Output

a side-by-side of which query hit which chunk.

## Failure modes

on a well-headed document, semantic chunking merged rate limiting with error handling and lost to recursive. He says semantic chunking is for unstructured text where topic shifts are not marked by headers. `langchain-experimental` APIs can move.
