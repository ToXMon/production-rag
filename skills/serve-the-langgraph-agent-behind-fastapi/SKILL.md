---
name: "Serve the LangGraph agent behind FastAPI"
description: "turning the security, cache, metrics, and agent modules into one HTTP API."
---

# Serve the LangGraph agent behind FastAPI

## Inputs

env file (OpenAI key, Anthropic key, LangChain tracing key, project name, app env, log level, rate limit, cache TTL, max retries). Demo values: rate limit 20 per minute, cache TTL 300 seconds, max retries 3, message length 1 to 10,000.

## Steps

1. `uv init` in a new directory. `uv add` LangChain, the Anthropic and OpenAI integrations, LangGraph, LangSmith, FastAPI, uvicorn, SlowAPI, Pydantic settings, and python-dotenv. Dev: pytest and httpx.
2. Package layout: `app/` with `config.py`, `models.py`, `security.py`, `cache.py`, `monitoring.py`, `agent.py`, `main.py`; `tests/` for security, cache, and API. Commit `.env.example`, never `.env`.
3. Settings: a Pydantic `BaseSettings` class, env file, extra fields ignored, and `get_settings` wrapped in `lru_cache`. A missing API key must crash at startup.
4. Models: chat request (message, thread id), chat response (response, thread id, model used, cached, processing milliseconds, timestamp, and later security notes), health response, metrics response, error response.
5. Response cache: lowercase the query, SHA-256 the key, expire after TTL. He says swap this for Redis when more than one instance must share it.
6. Agent state: messages with an add-messages reducer, error, retry count, model used. Graph nodes: process with the primary `ChatOpenAI` (pass the API key from settings), fallback node with a second model, error node that returns a polite message instead of a 500. Conditional edges after process and after fallback. `invoke` is `@traceable` and returns response, model used, and error.
7. FastAPI lifespan creates the security pipeline, cache, metrics, and agent, and logs a summary on shutdown. SlowAPI limiter keys off client IP at the configured rate; over the limit returns 429.
8. `POST /chat` order: security check, cache lookup, agent invoke on miss, output validation, cache store, record metrics, return the chat response. Also expose health, metrics, and cache stats. Mark the chat route `@traceable`.
9. Run `uv run uvicorn app.main:app --reload --port 8000`. Check `GET /health` (agent, security, and cache all true). Repeat a question and expect cached true. A message that includes an email should be answered without echoing the email and should note that PII was masked. An injection string should be blocked before any model call. Hammering past 20 requests in a minute should flip from 200 to 429.

## Output

a local JSON API whose traces appear under the LangSmith project.

## Failure modes

LangSmith env names must be the LangChain names (see the tracing skill). Primary and fallback were the same model in the demo; he says production should use a different fallback model. In-memory cache is per process.
