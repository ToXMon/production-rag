---
name: "Log structure, metrics, and an instrumented LLM call"
description: "any production LLM process. Monitoring wraps the system and does not change answers."
---

# Log structure, metrics, and an instrumented LLM call

## Inputs

each call's latency, token counts, error flag, and cache flag.

## Steps

1. Structured logs: a JSON object with timestamp, level, message, module, function, plus extra fields. He names Datadog, Elasticsearch, and CloudWatch as consumers. Plain text cannot answer "latency over 1 second" or "errors from this user" at 10,000 requests an hour.
2. Metrics counters: request total, errors, latency sum and latency count (do not average the averages), input tokens, output tokens, cache hits, cache misses. Record a request, then summarize average latency, error rate, and cache hit rate.
3. Instrumented wrapper: `@traceable` invoke that logs those fields and sends the trace to LangSmith. JSON logs and LangSmith traces are separate systems.

## Output

one JSON line per call and a summary dict. Demo summary: 3 requests, 0 errors, input tokens 14, output tokens 876, cache hit rate 0.

## Failure modes

not stated beyond flying blind. The three questions he wants the pillars to answer: is it working, is it fast, is it expensive or breaking.
