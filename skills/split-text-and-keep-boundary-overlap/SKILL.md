---
name: "Split text and keep boundary overlap"
description: "implementing the recursive default, and when proving overlap."
---

# Split text and keep boundary overlap

## Inputs

raw text or Documents; chunk size; overlap; separator list.

## Steps

1. Build `RecursiveCharacterTextSplitter` (the hands-on example uses chunk size 500 and overlap 50, separators including blank lines, newlines, and an empty string). The basic-RAG notebook caption says chunk size "5500" and overlap 50; treat 5500 as unclear, not as a second recommendation.
2. Call `split_text` for a string and `split_documents` for Documents.
3. To see overlap, run the same splitter with overlap 0 and with overlap 20 (demo chunk size 50) and compare the end of chunk 1 with the start of chunk 2.

## Output

chunks whose boundaries repeat a small span of text.

## Failure modes

no overlap can orphan the solution from the problem (API key expires in chunk 1, refresh step in chunk 2). He calls overlap cheap insurance against missed retrievals.
