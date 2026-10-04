# Graphs and multi-hop

When does the course say a knowledge graph is required for multi-hop answers?

- Standard RAG fails multi-hop queries because chunks are isolated. GraphRAG extracts entities and relationships, builds a graph, and traverses it. Local search is multi-hop; global search uses community summaries for themes. Microsoft GraphRAG is the implementation he recommends. Skip the graph for simple facts, small corpora (under about 100 documents), real-time indexing, or when indexing cost dominates (about 07:05:03).
