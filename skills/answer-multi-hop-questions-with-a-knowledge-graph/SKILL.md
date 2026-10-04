---
name: "Answer multi-hop questions with a knowledge graph"
description: "the answer connects facts that never appear in one chunk (who works in the same department as the CEO's assistant). Not for simple fact lookup, corpora under about 100 documents, real-time indexing, or tight index budgets."
---

# Answer multi-hop questions with a knowledge graph

## Inputs

documents that state relationships; a graph library or Microsoft GraphRAG.

## Steps he actually codes with NetworkX

1. Build a directed graph. Add entity nodes (person, role, organization, department) and relationship edges (CEO of, works in, assistant to).
2. Traverse in hops: find the CEO, then their assistant, then that person's department, then others in the department.
3. Optionally extract entities and relationships with a chat model prompted on the source paragraph, instead of hand-building nodes.

## Steps he specifies for the Microsoft-style pipeline but does not code

index by LLM extraction, build the graph, community detection, community summaries, then at query time identify entities and traverse (local search) or answer from community summaries (global search). Install and run are named as install GraphRAG, point it at the document root, then query. CLI flags are not spoken. A LangGraph plus Neo4j option is named; steps not specified (the code is in the course repo, not read aloud).

## Output

an answer plus the path. In the demo that is Sarah Johnson, the executive department, and the other people in that department.

## Failure modes

standard vector search can retrieve a department mention and still miss the person who was never in the query. Graph indexing is slower and more expensive; he says skip it when that cost is not justified.
