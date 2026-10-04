# Agent index

How to choose a file:

- If the task is a procedure, open `skills/<slug>/SKILL.md`.
- If the task is a constraint or fact, open `knowledge/`.
- If the task names a library or service, open `tools/catalog.md`.
- If the task needs the speaker's words, open `resources/transcript/`.

## Skills

| Slug | When to use | Path |
| --- | --- | --- |
| `ground-the-model-on-retrieved-context-only` | any RAG prompt, before blaming the retriever or the model. | `skills/ground-the-model-on-retrieved-context-only/SKILL.md` |
| `attach-sources-to-retrieved-chunks` | when users must verify an answer. | `skills/attach-sources-to-retrieved-chunks/SKILL.md` |
| `bootstrap-the-course-python-project` | starting the local environment the course codes against. | `skills/bootstrap-the-course-python-project/SKILL.md` |
| `load-raw-files-into-langchain-documents` | before chunking, whenever context comes from files or URLs. | `skills/load-raw-files-into-langchain-documents/SKILL.md` |
| `choose-a-chunking-strategy` | before embedding. The instructor treats chunking as architecture, not a preprocessing detail. | `skills/choose-a-chunking-strategy/SKILL.md` |
| `split-text-and-keep-boundary-overlap` | implementing the recursive default, and when proving overlap. | `skills/split-text-and-keep-boundary-overlap/SKILL.md` |
| `embed-with-an-embedding-model-not-a-chat-model` | indexing and querying. | `skills/embed-with-an-embedding-model-not-a-chat-model/SKILL.md` |
| `create-a-chroma-collection-and-query-it` | local vector store for development. He later says Chroma is the choice under about 100k vectors. | `skills/create-a-chroma-collection-and-query-it/SKILL.md` |
| `read-scores-and-filter-by-metadata` | after a LangChain vector-store search, and when metadata can drop irrelevant hits. | `skills/read-scores-and-filter-by-metadata/SKILL.md` |
| `assemble-a-basic-langchain-rag-chain` | first end-to-end chain after chunks exist. | `skills/assemble-a-basic-langchain-rag-chain/SKILL.md` |
| `diagnose-the-five-production-failure-modes` | a demo works on about 10 documents and breaks around 10,000, or answers go wrong in production. | `skills/diagnose-the-five-production-failure-modes/SKILL.md` |
| `add-hybrid-bm25-plus-vector-search` | production queries that include SKUs, acronyms (WCAG example), error codes (the intended example is a connection-refused code; captions say "econ refuse"), or exact names. Skip it for simple Q&A, creative chat, or a throwaway prototype. | `skills/add-hybrid-bm25-plus-vector-search/SKILL.md` |
| `reject-requests-that-exceed-a-token-budget` | user-controlled or unpredictable input, and when you need per-user or per-endpoint chargeback and abuse limits. | `skills/reject-requests-that-exceed-a-token-budget/SKILL.md` |
| `trace-runs-in-langsmith` | before production, not after the first bad answer. Multi-step agents have no stack trace for a wrong answer. | `skills/trace-runs-in-langsmith/SKILL.md` |
| `compare-recursive-and-semantic-chunking-on-one-document` | before adopting semantic chunking as the default. | `skills/compare-recursive-and-semantic-chunking-on-one-document/SKILL.md` |
| `retrieve-small-return-the-parent` | when small chunks search well but the model needs the surrounding section. | `skills/retrieve-small-return-the-parent/SKILL.md` |
| `compress-chunks-before-the-prompt` | long mixed documents where only a paragraph answers the query, and token cost at generation matters more than an extra model call. | `skills/compress-chunks-before-the-prompt/SKILL.md` |
| `expand-one-question-into-several-queries` | a single wording is unlikely to hit every relevant chunk. | `skills/expand-one-question-into-several-queries/SKILL.md` |
| `tune-hnsw-and-decide-when-to-shard` | queries slow down or accuracy drops as the index grows into the hundreds of thousands or millions. He says Pinecone, pgvector, Chroma, and Qdrant use HNSW or something similar. | `skills/tune-hnsw-and-decide-when-to-shard/SKILL.md` |
| `cut-vector-search-cost-without-a-new-vendor` | after a workload exists, not before the first prototype. He says start managed, and self-host when the bill matters. | `skills/cut-vector-search-cost-without-a-new-vendor/SKILL.md` |
| `choose-a-vector-host-by-scale` | picking Chroma versus Pinecone versus pgvector. | `skills/choose-a-vector-host-by-scale/SKILL.md` |
| `put-pgvector-on-supabase-and-lock-the-tables` | moving the same LangChain store from local disk to hosted Postgres. | `skills/put-pgvector-on-supabase-and-lock-the-tables/SKILL.md` |
| `cache-embedding-calls-and-repeated-answers` | the same text is embedded twice, or the same question is asked again. | `skills/cache-embedding-calls-and-repeated-answers/SKILL.md` |
| `log-structure-metrics-and-an-instrumented-llm-call` | any production LLM process. Monitoring wraps the system and does not change answers. | `skills/log-structure-metrics-and-an-instrumented-llm-call/SKILL.md` |
| `sanitize-input-mask-pii-and-validate-output` | every user string before a model call, and every model string before the client. | `skills/sanitize-input-mask-pii-and-validate-output/SKILL.md` |
| `serve-the-langgraph-agent-behind-fastapi` | turning the security, cache, metrics, and agent modules into one HTTP API. | `skills/serve-the-langgraph-agent-behind-fastapi/SKILL.md` |
| `test-the-pure-logic-then-containerize` | before deploy. Security and cache tests should not call a model or the network. | `skills/test-the-pure-logic-then-containerize/SKILL.md` |
| `deploy-the-api-on-render` | the service should be reachable on a public URL. | `skills/deploy-the-api-on-render/SKILL.md` |
| `choose-rag-or-long-context-or-both` | deciding whether to stuff documents into a long window. | `skills/choose-rag-or-long-context-or-both/SKILL.md` |
| `prepend-document-context-before-embedding` | chunks say "the company" or "they", titles and headers carry the entity, or documents come from multiple sources. Anthropic's contextual retrieval, late 2024, as he presents it. | `skills/prepend-document-context-before-embedding/SKILL.md` |
| `simulate-or-run-late-chunking-when-pronouns-matter` | references such as "he" or "the company" must survive the split. He also lists parent-child retrieval as the practical alternative. | `skills/simulate-or-run-late-chunking-when-pronouns-matter/SKILL.md` |
| `run-a-self-correcting-rag-graph` | complex questions that may need a rewrite, high-stakes or user-facing apps, mixed document types (legal, guides, instructions). He says a simple prototype does not need it. | `skills/run-a-self-correcting-rag-graph/SKILL.md` |
| `answer-multi-hop-questions-with-a-knowledge-graph` | the answer connects facts that never appear in one chunk (who works in the same department as the CEO's assistant). Not for simple fact lookup, corpora under about 100 documents, real-time indexing, or tight index budgets. | `skills/answer-multi-hop-questions-with-a-knowledge-graph/SKILL.md` |
| `embed-page-images-when-layout-is-the-content` | financial reports, technical docs, papers with figures or formulas, contracts, medical records, or anything where tables and charts must survive. Do not use it for plain prose, simple CSV, real-time paths, or cost-sensitive paths. | `skills/embed-page-images-when-layout-is-the-content/SKILL.md` |

## Knowledge

| File | Question |
| --- | --- |
| `knowledge/chunking.md` | What chunking choices, sizes, overlap, and split types does the course state? |
| `knowledge/retrieval.md` | What retrieval failures, search methods, and later retrieval patterns does the course state? |
| `knowledge/prompts-and-grounding.md` | How does the course say a RAG chain must ground the model in retrieved context? |
| `knowledge/vector-stores.md` | What does the course state about embeddings, scores, HNSW, and hosted stores? |
| `knowledge/cost-and-ops.md` | What costs, token bills, caches, and savings claims does the course state? |
| `knowledge/evaluation-and-tracing.md` | What does the course state about debugging, traces, metrics, and LangSmith? |
| `knowledge/security.md` | What input, PII, output, and rate-limit controls does the course state? |
| `knowledge/deployment.md` | What does the course state about the production API, Docker, tests, and Render? |
| `knowledge/graphs-and-multihop.md` | When does the course say a knowledge graph is required for multi-hop answers? |
