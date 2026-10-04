---
name: "Retrieve small, return the parent"
description: "when small chunks search well but the model needs the surrounding section."
---

# Retrieve small, return the parent

## Inputs

a long document; a parent splitter and a child splitter.

## Steps

1. Parent `RecursiveCharacterTextSplitter` chunk size 800; child chunk size 200; both with overlap (sizes as stated).
2. In-memory doc store plus a Chroma collection (demo name `parent_child_demo`).
3. Construct `ParentDocumentRetriever` with the vector store, doc store, child splitter, and parent splitter. Add documents.
4. Compare a normal search hit (demo child about 173 characters) with the parent returned to the model (demo about 675 characters).

## Output

a focused match plus the larger parent text.

## Failure modes

small chunks alone fragment context; large chunks alone dilute embeddings. Parent-child costs extra storage (stated in the later comparison).
