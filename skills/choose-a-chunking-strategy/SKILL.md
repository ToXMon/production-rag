---
name: "Choose a chunking strategy"
description: "before embedding. The instructor treats chunking as architecture, not a preprocessing detail."
---

# Choose a chunking strategy

## Inputs

document type, whether you are prototyping, and whether quality is critical.

## Steps

1. Do not use fixed-size chunking in production. He allows it only for quick prototypes, fast processing, or hard size constraints. It cuts mid-word and mid-thought.
2. Default to recursive splitting: paragraphs, then newlines, then sentences, then clauses, then words, then characters as the last resort. LangChain's recursive splitter is the framework default he cites.
3. If prototyping must be quick, or documents are simple and structured, stay on recursive. If quality is critical, or topics shift without clear structure, use semantic chunking.
4. Reference table he gives: general documents, recursive, chunk size 500 to 1,000; technical and legal documents, semantic; code, a code splitter with chunk size at function boundaries; markdown, a markdown header splitter on headers.
5. Start with recursive plus overlap, measure retrieval, and upgrade to semantic only if quality is not enough. He calls this an 80/20 rule: recursive with good overlap gets most of the way; semantic gets the rest and costs more.
6. Semantic procedure, named with steps: embed each sentence, compare adjacent embeddings, split where similarity drops.
7. Late chunking is named as embed-the-full-document-then-split, needing a model such as Jina embeddings v2. He says semantic is the practical best for now and late chunking is the direction to watch. A later lecture gives the comparison procedure.

## Output

a chosen splitter and size/overlap.

## Failure modes

too-small chunks lose context and add retrieval noise; too-large chunks dilute the embedding and waste token budget. Same corpus, model, database, and query can return different answers if only the chunking changes. Sweet spot he states: usually about 200 to 1,000 tokens.
