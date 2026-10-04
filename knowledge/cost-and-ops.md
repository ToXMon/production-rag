# Cost and ops

What costs, token bills, caches, and savings claims does the course state?

- Token billing is why a single long paste (about 50,000 plus input tokens and about 2,000 output tokens for a 200-page contract) can cost as much as about 100 normal requests. Check the budget before the API call. Word count times 1.3 is a guardrail, not an invoice (about 02:13:55).
- Illustrative monthly costs he charts. At about 500k documents and 10k queries a day: Pinecone serverless about $20 to $30 and zero ops; Pinecone pods, caption unclear ("$7 to $140"), with guaranteed latency; pgvector on RDS about $32 and low ops; self-hosted pgvector about $15 to $20 and medium ops. Graph points he states: at 500k, Pinecone about $30, managed pgvector about $35, self-hosted about $20; at 5 million, about $400, $100, and $75; at 50 million, about $1,500 plus, $400, and $300 (about 03:23:06).
- Cost tactics and claimed savings (about 03:28:03): 1536 to 512 dimensions, about 30 to 60 percent; float32 to int8, about 50 to 75 percent; batching, about 10 to 30 percent; caching repeats, about 10 to 40 percent; right-sizing, about 20 to 50 percent. Do not optimize prematurely.
- Embedding caches exist to avoid paying for the same vectors twice (about 03:52:55). An exact response cache after normalization misses paraphrases; a semantic cache needs vectors and a threshold such as 0.95 (about 04:03:13).
- Identical questions inside the TTL should be one model call. He claims an in-memory TTL cache can cut costs about 30 to 60 percent when repeats are common. Demo TTL is 300 seconds. Use SHA-256 even for cache keys. The shared store he names for many instances is Redis; the metrics store he names is Prometheus (about 04:45:15).
- Long-context models do not make RAG obsolete. He says they get unreliable around 60 to 70 percent of the advertised window. RAG is for large, changing, citation-heavy, cost-sensitive corpora. The pattern he wants is RAG and long context together (about 06:06:19).
