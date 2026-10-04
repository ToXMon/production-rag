---
name: "Simulate or run late chunking when pronouns matter"
description: "references such as \"he\" or \"the company\" must survive the split. He also lists parent-child retrieval as the practical alternative."
---

# Simulate or run late chunking when pronouns matter

## Inputs

a document; either a late-chunking embedding model or a simulation that prepends context.

## Steps

1. Early chunking, for contrast: split with `RecursiveCharacterTextSplitter`, embed each chunk alone. In the Steve Jobs demo, later chunks contain "he" and not the name, so a query about Steve Jobs matches poorly.
2. True late chunking, as specified: embed the whole document first, then split the token embeddings by position, so each slice still carries document context. He says this needs a model that supports it natively and names Jina embeddings. Claimed gain: about 10 to 12 percent retrieval accuracy, and elsewhere "research shows about 10 to 20 percent".
3. His runnable demo is not true late chunking. It prepends a context sentence and re-embeds. He says so. The printed improvement on that simulation is about 0.2 percent. Do not quote 0.2 percent as the late-chunking result.
4. Comparison table he gives versus traditional chunking: overlap about 3 to 5 percent; contextual retrieval about 15 to 20 percent and about 1 cent per document; late chunking about 10 to 12 percent but you must find a specialized model; parent-child quality is excellent at the cost of extra vectors; combining approaches about 25 to 30 percent.

## Output

chunk vectors that still resolve pronouns, or an explicit decision to use parent-child instead.

## Failure modes

using a normal embedding API on already-split text and calling it late chunking.
