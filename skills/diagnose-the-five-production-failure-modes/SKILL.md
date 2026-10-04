---
name: "Diagnose the five production failure modes"
description: "a demo works on about 10 documents and breaks around 10,000, or answers go wrong in production."
---

# Diagnose the five production failure modes

## Inputs

the query, the chunks that were stored, the chunks retrieved, and the prompt that was sent.

## Steps

1. Bad chunking: splits fall mid-thought, so retrieval returns partial context. Fix with the chunking skill.
2. Embedding mismatch: user wording and document wording differ (example: "how do I cancel" versus "termination policy") or the query has no semantics (codes, acronyms). Fix with hybrid search, not a bigger chat model.
3. Retrieval noise: many hits, few relevant, and the LLM gets confused. He points at hybrid search and, separately, truncation and token budgeting.
4. Context overflow: the prompt is so long the model ignores or truncates part of it. Fix with token budgeting and compression.
5. Hallucination: the answer is in the context and the model still invents. Fix with the grounding prompt; he still treats this as its own failure mode.

## Output

one primary failure mode to fix before tuning generation.

## Failure modes

not stated as a meta-failure. He also says about 90% of RAG systems fail in production for these same reasons.
