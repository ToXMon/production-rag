---
name: "Compress chunks before the prompt"
description: "long mixed documents where only a paragraph answers the query, and token cost at generation matters more than an extra model call."
---

# Compress chunks before the prompt

## Inputs

a base retriever, a chat model, a query.

## Steps

1. Build `LLMChainExtractor` from the LLM.
2. Wrap the base retriever in `ContextualCompressionRetriever` with that compressor.
3. Compare `invoke` with and without compression on a noisy document.

## Output

shorter excerpts. On the noisy demo he reports lengths dropping from about 1,700 and 1,500 characters to a couple of hundred, roughly an 82 to 87 percent reduction, and about 85 percent fewer tokens in the final prompt.

## Failure modes

extra completion calls at retrieval time. On already-clean chunks the compression is invisible. Skip it when documents are short and entirely relevant.
