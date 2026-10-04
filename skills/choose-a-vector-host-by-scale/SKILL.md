---
name: "Choose a vector host by scale"
description: "picking Chroma versus Pinecone versus pgvector."
---

# Choose a vector host by scale

## Inputs

vector count and whether you will operate the database.

## Steps (his decision table, stated as rules of thumb)

1. Under about 100k vectors: Chroma, local, free.
2. About 10k to 1 million: Pinecone serverless, low cost, no ops.
3. About 1 million to 10 million: managed pgvector.
4. Above about 10 million: self-hosted pgvector.

## Output

a hosting choice, revisited when the count crosses a band.

## Failure modes

choosing Pinecone at small scale without planning the 50-million-vector price gap he charts. The bands overlap on purpose in his talk; they are not a single strict function.
