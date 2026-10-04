---
name: "Load raw files into LangChain Documents"
description: "before chunking, whenever context comes from files or URLs."
---

# Load raw files into LangChain Documents

## Inputs

a path, a directory plus glob, or one or more URLs.

## Steps

1. Pick a loader: `TextLoader` for plain text; `PyPDFLoader` to start (fast, basic metadata, simple PDFs); PyMuPDF loader when speed, metadata, and volume matter; Unstructured PDF loader for tables and complex layouts (slower, richer metadata); `DirectoryLoader` with a path, glob, and loader class; web loader for one URL or a list of URLs; Unstructured loader for mixed complex formats.
2. Instantiate the loader with the source. Call `.load()`.
3. Read `page_content` and `metadata` (source, page, producer, and similar fields the loader adds).

## Output

a list of Document objects.

## Failure modes

`pypdf` not installed (`PyPDFLoader` import fails until `uv add pypdf`). Recommendation stated: start with PyPDFLoader and switch later for the use case.
