---
name: "Expand one question into several queries"
description: "a single wording is unlikely to hit every relevant chunk."
---

# Expand one question into several queries

## Inputs

a base retriever and a chat model. Import path in the recording is `langchain_classic` (`MultiQueryRetriever`). He warns those classic imports may be deprecated by the end of 2026 and that retrievers were moving toward LangGraph.

## Steps

1. Enable logging so the generated queries print.
2. `MultiQueryRetriever.from_llm` with the vector-store retriever and the LLM.
3. `invoke` the original question. The demo question about tools for AI applications produced three rewrites and three embedding calls, then unique documents.

## Output

a deduplicated document set from several phrasings.

## Failure modes

extra embedding and chat cost. Exact class path is version-sensitive. Named in the same lecture, without a separate procedure: self-query and a caption that sounds like "hypersarch" (unclear; do not treat as a specified algorithm).
