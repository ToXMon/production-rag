---
name: "Test the pure logic, then containerize"
description: "before deploy. Security and cache tests should not call a model or the network."
---

# Test the pure logic, then containerize

## Inputs

the security and cache modules; a Dockerfile; Docker Desktop.

## Steps

1. Pytest the sanitizer (benign questions versus injection strings), the PII detector (email, phone, SSN, card versus a plain greeting), and the output validator. Separate tests for cache miss, store, hit, case-insensitive hit, and expiry.
2. `uv run pytest` on the security test file with verbose output, and the cache file. He reports 20 tests, all passing, under 3 seconds.
3. Testing pyramid he states: fast unit tests at the bottom, integration tests with a mocked agent in the middle, real model tests only in staging. The mocked-agent layer is named; steps for that layer are not specified beyond the pyramid.
4. Dockerfile with no extension: copy dependency files before application code so installs stay cached; create a non-root user and switch to it; give that user the app directory if the build hits permission denied; healthcheck the health endpoint every 30 seconds and mark unhealthy after 3 failures.
5. Compose file: build the service, map port 8000, pass the env file. `docker compose up --build`. Open `/health` and `/docs` (Swagger).

## Output

a container that serves the same API.

## Failure modes

running the container as root; copying code before dependencies and rebuilding the install every time; healthcheck failing because the path is not `/health`.
