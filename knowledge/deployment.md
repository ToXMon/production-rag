# Deployment

What does the course state about the production API, Docker, tests, and Render?

- The production API adds, on top of tracing and logging: input sanitization, PII detection and masking, retries, response cache, rate limiting, health checks, and Docker (about 04:16:47). Request path: rate limit, security middleware, cache, model with fallback and retry, output check, metrics. Build each module alone, then wire FastAPI (about 04:20:12).
- The agent graph has three nodes: primary model, fallback model, graceful error. Users should not see an internal server error. Messages use an add-messages reducer that appends and drops duplicates (about 04:55:23).
- POST /chat is the only large route. Health, metrics, and cache stats are smaller. Health is what a Docker healthcheck hits. Swagger is /docs (about 05:05:37).
- Security and cache unit tests do not need keys or a model. He reports 20 tests passed in under 3 seconds (about 05:27:59).
- Dockerfile rules he emphasizes: dependency layer before code, non-root user, healthcheck every 30 seconds, unhealthy after 3 failures (about 05:31:26).
- Pre-deploy checklist he ticks (about 05:41:33): injection blocking, PII masked on input and output, rate limit, Pydantic body validation, non-root container, secrets only in the environment, model fallback, retries with exponential backoff (named here; the backoff parameters are not specified), health endpoint, no stack traces to clients, response cache and cache stats, token-budget awareness, LangSmith on every request, JSON logs, metrics endpoint, Docker plus Compose, an env example file, and tests passing. Ready to deploy is not the same as deployed.
- Render's free plan is for learning. Paid plans stay on. Auto deploy follows a git push to main. Secrets are set in the dashboard, not in render.yaml (about 05:43:07).
- Free Render services sleep after 15 minutes; cold start is about 30 to 60 seconds. He cites about 750 hours of runtime a month. A stateless API plus an in-memory cache scales horizontally only after the cache moves to Redis (about 06:00:32).
