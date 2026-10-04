# Security

What input, PII, output, and rate-limit controls does the course state?

- Pydantic settings fail at startup if the API key is missing. Chat messages are rejected under length 1 or over 10,000 before any model call (about 04:26:52).
- Regex filters and PII masks are a fast first layer, not a proof against a creative attacker. PII types in the detector: email, phone, SSN, credit card (about 04:35:09).
- Rate-limit demo: 20 requests a minute allowed; request 21 and after return HTTP 429 (about 05:15:43).
