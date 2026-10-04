---
name: "Choose RAG or long context, or both"
description: "deciding whether to stuff documents into a long window."
---

# Choose RAG or long context, or both

## Inputs

corpus size, query volume, whether the task needs the whole document at once, whether citations and updates matter.

## Steps

1. Use long context when the corpus is small. He gives two thresholds: under about 100k tokens in the overview, and under 50,000 tokens in the decision script. Also when query volume is low (under about 100 a day), the task needs the entire document, documents change so often that embedding overhead is wasted, or you are optimizing for simplicity rather than cost.
2. Use RAG when the corpus is large (he says greater than about 100k), query volume is high (hundreds a day), users ask specific questions, cost or latency matters, you need citations, or documents are relatively stable.
3. Hybrid he names: RAG retrieves candidate chunks, then those chunks are loaded into the window for a deeper answer. Steps beyond that sentence are not specified.

## Output

a routing choice.

## Failure modes

judging cost on a tiny demo. His slide says RAG is over 1,200 times cheaper, about 1 second versus about 45 seconds, and long context about 10 cents a query, with long context unreliable around 60 to 70 percent of a claimed 1 million token window (Gemini is the example, including a 10 million token claim). His script on 100k tokens with a mini model prints a different bill: long context about 25 to 26 cents a query, RAG far cheaper, and at 10,000 queries a day long context a bit over $2,500 a day versus RAG a bit over $100 a day, which he sums as about $73,500 saved per month. Treat the slide and the script as two statements, not one reconciled number. Some latency figures in the script captions are unclear.
