# Evaluation and tracing

What does the course state about debugging, traces, metrics, and LangSmith?

- LLM debugging is hard because outputs are non-deterministic, errors cascade, failures are silent, and extra loops multiply token spend (about 02:22:19).
- Observability means inspecting the path, not only the final answer. He splits it into traces (what happened), metrics (tokens, latency, cost, errors), and evals (correctness, relevance, human feedback, regressions) (about 02:22:19).
- Add tracing before the outage. A sample line he gives managers: about 12 cents per report, about 45 seconds, quality score about 85 percent (about 02:25:41).
- LangSmith is described as framework-agnostic for tracing, evaluating, and deploying agents, and it is the tool he uses because it can trace a LangChain or LangGraph app from environment variables (about 02:29:03).
- Production visibility has three pillars: structured logging (what happened), metrics (how much), and an instrumented LLM wrapper around every call. Order he wants: security, then cost control, then error handling, with monitoring outside all of them (about 04:05:13).
- Eight metric fields he lists are enough to see health: requests, errors, latency sum, latency count, input tokens, output tokens, cache hits, cache misses (about 04:08:34).
