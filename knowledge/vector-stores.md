# Vector stores

What does the course state about embeddings, scores, HNSW, and hosted stores?

- Chat models take text and return text. Embedding models take text and return vectors. The same vendor can ship both. They are not interchangeable (about 00:48:13).
- `text-embedding-3-small` dimension in the demo: 1536. More dimensions hold more features and cost more storage and slower search. Gemini embeddings: 768, and he says they are free. BGE small: 384, fastest and least nuance. Sweet spot he states for most cases: 768 to 1536 (about 00:51:42). `text-embedding-3-large` is described only as larger; the caption number "3,72" is unclear, so a specific large dimension is not taken from this transcript.
- Chroma's role in the lecture: store document embeddings and run similarity search for an app that then calls an LLM. The pattern is not Chroma-specific (about 01:01:06).
- In the raw Chroma demo, distance 0 is an exact match and larger distances are worse (about 01:14:30). Some stores return similarity instead. Convert with 1 divided by (1 plus distance) if you need a similarity-style score (about 01:17:50).
- Metadata filters run with the vector search. Demo: topic database, k=5, drops non-matching topics (about 01:21:12).
- OpenAI embedding vectors in the demo have dimension 1536 and norm about 1.0. Normalization stops longer texts from dominating only because they are longer. `embed_query` is one string; `embed_documents` is a list (about 01:46:57).
- Most vector databases he lists use HNSW (hierarchical navigable small world graphs). Two knobs: M and ef_search. Pick two of accuracy, speed, and memory (about 03:13:01).
- Query latency around 100 ms or more suggests the index does not fit in memory. Vertical scale example: 8 GB RAM and 100k vectors at about 50 ms versus 32 GB and the same 100k vectors at about 10 ms (about 03:19:43).
- Managed Pinecone: sharding is automatic, ops burden low, control limited, expensive at scale. Self-hosted pgvector: you shard, ops are significant, full control, cheaper at scale (about 03:19:43).
- Hosting prices as of the recording (about 03:33:18): Supabase is the one he recommends; free tier 500 MB with pgvector; Pro $25 a month and about 8 GB. The team price in the captions ("$5.99") is unclear. Neon: serverless, free 512 MB, Pro about $19, can scale to zero. AWS RDS: small about $30, mid about $60, for teams already on AWS or GCP. The course can stay on Supabase's free tier.
- Supabase free tier details he reads (about 03:36:02): unlimited API requests, 50,000 monthly active users, 500 MB database, 5 GB egress, 5 GB cached egress, 1 GB file storage. Direct connection for long-lived apps; transaction pooler for brief serverless connections; port 5432.
- LangChain created the pg embedding and pg collection tables. Unrestricted data-API access means row-level security is off. Turn it on (about 03:49:33).
