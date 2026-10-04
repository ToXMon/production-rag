# Prompts and grounding

How does the course say a RAG chain must ground the model in retrieved context?

- RAG, as drawn here (about 00:01:48): the query and retrieved document context go into the prompt, then the chat model, then an output parser. The vector store holds embedded, indexed documents. The point is to ground the model and reduce hallucination.
- A basic chain runs context and question in parallel. The question must not be rewritten on that path (`RunnablePassthrough`). Context comes only from the retriever (about 00:01:48).
