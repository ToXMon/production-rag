---
name: "Ground the model on retrieved context only"
description: "any RAG prompt, before blaming the retriever or the model."
---

# Ground the model on retrieved context only

## Inputs

retrieved context string, user question.

## Steps

1. Pass the question through unchanged (`RunnablePassthrough` in the LangChain example).
2. Put both context and question in the prompt.
3. Instruct the model to answer based only on the context.
4. Instruct it to say it does not know, or that it does not have information, when the context does not contain the answer.

## Output

an answer grounded in the chunks, or an explicit "I don't know".

## Failure modes

without that instruction the model answers from its own weights (the quantum-computing example) and can sound coherent while hallucinating. Prompting alone does not prove the answer is in the documents; also return sources.
