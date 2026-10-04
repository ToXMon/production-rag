# Tool catalog

One entry per tool from the pack Tools section. Grouping is for navigation. Roles and "mentioned only" marks are copied from the pack.

## Frameworks

- LangChain: framework for loaders, splitters, retrievers, prompts, and LCEL chains. Core version just over 1.0 at recording.
- LangChain core: version import target via `importlib.metadata`.
- LangGraph: stateful graphs for the production agent and the agentic RAG loop. Version just over 1.0 at recording. Also named as the future home of retrievers that had moved into `langchain_classic`.
- TextLoader: plain-text documents.
- PyPDFLoader and pypdf: default PDF loader. The package must be installed separately.
- PyMuPDF loader: faster PDF loader with better metadata, for volume.
- Unstructured PDF loader and Unstructured loader: complex layouts, tables, mixed formats; slower.
- DirectoryLoader: a directory, a glob, and a loader class.
- Web base loader: one or many URLs.
- Document: page content and metadata.
- RecursiveCharacterTextSplitter: default hierarchical splitter. `split_text` versus `split_documents`.
- CharacterTextSplitter and TokenTextSplitter: imported in the splitter file. The hands-on walk-through uses the recursive splitter; the other two are named by the import.
- Markdown header text splitter: markdown chunks by headers. Spoken as an MD splitter.
- Code splitter and the Language enum: split code on language constructs. Chunk size can follow functions. The exact class name is not spoken cleanly.
- SemanticChunker in langchain-experimental: meaning-based splits. Demo breakpoint is the 90th percentile.
- BM25, BM25Retriever, and rank-bm25: keyword retriever. Must be rebuilt on insert.
- EnsembleRetriever: LangChain fusion retriever he says was removed. He reimplemented weighted reciprocal rank fusion.
- Reciprocal rank fusion: the fusion method. No separate library.
- RunnablePassthrough and RunnableParallel: LCEL. Parallel is imported; the chain shown uses a dict plus passthrough.
- ChatPromptTemplate: grounded prompt with context and question.
- String output parser: chain output as a string.
- ParentDocumentRetriever plus an in-memory doc store: search the child, return the parent.
- ContextualCompressionRetriever and LLMChainExtractor: drop irrelevant sentences. A later import path included langchain_classic.
- MultiQueryRetriever: an LLM rewrites one query into several. langchain_classic in this recording.
- CacheBackedEmbeddings and LocalFileStore: disk cache for embeddings, via langchain_classic here. Deprecation called out for December 2026.
- Pydantic BaseSettings and BaseModel: settings and API contracts. lru_cache wraps get_settings.
- FastAPI: HTTP app, lifespan, POST /chat, health, metrics, cache stats, and /docs.
- uvicorn: ASGI server, port 8000 locally, PORT on Render.
- SlowAPI: per-IP rate limit. Returns 429 when exceeded.

## Models

- OpenAI API: chat and embeddings. Keys from the account dashboard.
- Anthropic API: second provider and ChatAnthropic. The key-creation URL in the captions is unclear.
- ChatOpenAI: chat wrapper. Demo model family is gpt-4o-mini. A later "GPT 5.4 nano" caption is unclear and is not a verified model id.
- ChatAnthropic / Claude: second chat check.
- OpenAI embeddings API and text-embedding-3-small: 1536-dimension demo model. text-embedding-3-large is the larger model; the spoken dimension is unclear.
- Gemini embeddings: 768 dimensions, described as free.
- BGE small: 384-dimension embedding model.
- Jina embeddings (v2 named for late chunking): native late chunking. Spoken import is JinaEmbeddings.
- ColPali: vision embedding of page images. The model id in the captions is unclear.
- PaliGemma: named as the Google vision-language model in that stack. Captions say "pali jamma".
- GPT-4, Claude, and later vision-capable chat models: read retrieved page images. The exact vision model id is not fixed.

## Vector stores

- Chroma and chromadb: local vector store. Client, get-or-create collection, upsert, and query with query texts and n_results. Also from_documents and as_retriever.
- Pinecone: managed index, autotuned HNSW, top_k, serverless versus pods. No manual M or ef.
- Qdrant: named as another HNSW store. Mentioned only.
- FAISS: appeared as a metadata example of a vector database. Mentioned only.
- pgvector: Postgres extension for embeddings. HNSW index with m, ef_construction, and hnsw.ef_search.
- PostgreSQL: the database pgvector attaches to. Port 5432 in the Supabase string.
- HNSW: index type controlled by M and ef_search.

## Hosting

- Supabase: hosted Postgres he recommends, with a free tier, Pro at $25, direct URI versus poolers, and row-level security.
- Neon: serverless Postgres that can scale to zero. Hosting option.
- AWS RDS: enterprise Postgres hosting option, with the price bands above.
- Docker, Dockerfile, Docker Compose, and Docker Desktop: image build, non-root user, healthcheck, and docker compose up --build.
- Render and render.yaml: host, free plan, auto deploy, dashboard secrets.
- Git and GitHub: the repo Render deploys from.
- Redis: shared cache across instances. Named. Client steps are not specified.

## Observability

- LangSmith (smith.langchain.com): tracing, token and latency views, tags, metadata. Tracing env vars must be the LANGCHAIN names.
- `@traceable`: decorator that records a function or route.
- Datadog, Elasticsearch, and CloudWatch: JSON log sinks.
- Prometheus: production metrics backend. Named as the replacement for in-process counters. Client steps are not specified.
- ELK stack: named with Datadog and CloudWatch as a log aggregator. Mentioned only.

## Other

- uv: project init, virtualenv, and package add.
- python-dotenv: load the env file.
- NumPy: L2 norm and the from-scratch cosine demo.
- MD5: demo hash for the vector-search cache and the first answer-cache sketch.
- SHA-256: hash for the production response-cache key.
- pytest and httpx: unit tests. httpx is named because the FastAPI test client needs it.
- NetworkX (DiGraph): teaching graph for multi-hop hops.
- Microsoft GraphRAG: the production GraphRAG he recommends. The spoken procedure is install it, point it at the documents, and query.
- Neo4j: named with LangGraph for a custom graph store. Steps not specified.
- PDF-to-image conversion: required for the ColPali path. The library name is not spoken.
- importlib.metadata: read installed package versions after a LangChain version attribute failed.
