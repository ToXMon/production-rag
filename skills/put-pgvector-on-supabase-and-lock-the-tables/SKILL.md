---
name: "Put pgvector on Supabase and lock the tables"
description: "moving the same LangChain store from local disk to hosted Postgres."
---

# Put pgvector on Supabase and lock the tables

## Inputs

a Supabase project, the database password, the connection URI, region.

## Steps

1. Create an organization and project. Generate the database password and save it. Pick a region. He uses the free tier for the course.
2. Copy the project URL, the publishable key, and the direct connection URI. He prefers the direct connection for long-lived app connections. Transaction pooler is what he describes for short serverless connections. Session pooler is only an alternative to direct. Port he states: 5432. User and database in the demo string: `postgres`.
3. Enable the `vector` extension in the dashboard (or in SQL).
4. Put the URI in the Supabase database URL env var with the password substituted and the brackets removed. If the password is lost, reset it under database settings.
5. LangChain `PGVector` with the embedding model, collection name (demos: `production_docs` and `production_documents`), JSONB metadata enabled, and the connection string. Add a test document, similarity-search it, then delete it. Tables show up as LangChain pg embedding and pg collection.
6. Enable row-level security on those tables. He says the data API otherwise leaves them unrestricted.

## Output

a cloud collection you can add to and query like the local one.

## Failure modes

forgotten password; RLS left off; using the pooler mode that does not match the app's connection lifetime. Connection-pooling details are named and then skipped ("you can look into" them).
