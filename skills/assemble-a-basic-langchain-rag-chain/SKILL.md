---
name: "Assemble a basic LangChain RAG chain"
description: "first end-to-end chain after chunks exist."
---

# Assemble a basic LangChain RAG chain

## Inputs

documents, embeddings, a chat model, a prompt.

## Steps

1. Split, then build the vector store from documents with a persist directory.
2. `vectorstore.as_retriever` with similarity search and a small `k` (demo: 2).
3. Chat prompt: answer only from context, be concise, say "I don't know" otherwise. Include context and question variables.
4. Format retrieved docs into one string.
5. LCEL pipe: a dict of `context` (retriever piped into the formatter) and `question` (`RunnablePassthrough`), then the prompt, the LLM, then a string output parser.
6. `chain.invoke` per question.

## Output

a string answer per question.

## Failure modes

same as the grounding skill. Temperature in the demo was set low for determinism; the spoken value is "two", which is unclear as a temperature (likely 0.2). Do not invent the literal.
