---
name: "Trace runs in LangSmith"
description: "before production, not after the first bad answer. Multi-step agents have no stack trace for a wrong answer."
---

# Trace runs in LangSmith

## Inputs

a LangSmith account (smith.langchain.com; GitHub, email, or Google; he says no credit card), a personal API key, and a project name.

## Steps

1. Put the key in the env file. He first tried LangSmith-named variables and then found the client required `LANGCHAIN_API_KEY` and `LANGCHAIN_PROJECT` even though the product is LangSmith. Tracing is toggled with the tracing env var; he also sets it in process with `os.environ`.
2. `uv add` the LangSmith package.
3. Decorate functions with `@traceable`. Pass a name, tags, and metadata (demo: user id, request name).
4. Run the function and open the project. Expect inputs, outputs, token breakdown, latency, status, and tags. Refresh if a run looks empty.

## Output

a trace per run. Two env vars are what he says are enough to trace existing LangGraph graphs.

## Failure modes

wrong env var names produce no traces. Non-determinism means you cannot debug by re-asking. Cascading errors: a bad search poisons later analysis. Silent failures return a confident wrong answer with no exception. A loop that runs 10 times instead of 2 can burn about 5x the expected tokens.
