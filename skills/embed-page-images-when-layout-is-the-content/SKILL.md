---
name: "Embed page images when layout is the content"
description: "financial reports, technical docs, papers with figures or formulas, contracts, medical records, or anything where tables and charts must survive. Do not use it for plain prose, simple CSV, real-time paths, or cost-sensitive paths."
---

# Embed page images when layout is the content

## Inputs

PDFs rendered as images; a ColPali-style vision embedding model; a vector store that can hold those embeddings; a vision-capable chat model for the answer.

## Steps

1. Do not extract text first. Render each page to an image, embed the image, and store the vector.
2. Embed the query with the same model. Retrieve page images. Send those images to a vision model (he names GPT-4, Claude, and later generations) to answer from what it sees.
3. He says ColPali is a vision-language model using contextual late interaction, and he ties it to PaliGemma (captions say "pali jamma"). The initialization string in the captions is "vori kali v1 d2", which is unclear. Do not guess the model id; check current ColPali docs.
4. Keep a text-RAG fallback for plain documents.

## Output

an answer grounded in the page image, including table structure and visual marks that text extraction dropped.

## Failure modes and cost

he says multimodal is on the order of 10 times text RAG; text query about 1 cent with a GPT-4-class model versus about 10 cents multimodal; embedding cost per page is higher and may need a GPU or a cloud GPU. PDF-to-image conversion is required. Not every vector database accepts these embeddings. Exact per-page prices were on screen and are not in the captions.
