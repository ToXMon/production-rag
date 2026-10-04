---
name: "Create a Chroma collection and query it"
description: "local vector store for development. He later says Chroma is the choice under about 100k vectors."
---

# Create a Chroma collection and query it

## Inputs

Python venv, the Chroma package, documents with ids and text.

## Steps

1. `python3 -m venv` (name in the demo is `venv`), activate, `pip install chromadb` (he says to copy the install line from the Chroma getting-started docs). Point the IDE at that interpreter.
2. `import chromadb` and construct a client. Create or get a collection with `get_or_create_collection` (demo name `test_collection`) so reruns do not depend on a fresh name.
3. Upsert rather than `add`, so reruns do not duplicate rows. Pass `ids` and `documents` (a list). The first error in the demo was passing the wrong field name; the argument must be `documents`.
4. `collection.query` with `query_texts` and `n_results`.

## Output

ids, documents, and distances. In that demo, distance 0 was the exact "hello world" match; nearer to 0 is more similar.

## Failure modes

using `add` in a loop duplicates data; wrong keyword arguments.
