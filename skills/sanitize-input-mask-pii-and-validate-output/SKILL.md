---
name: "Sanitize input, mask PII, and validate output"
description: "every user string before a model call, and every model string before the client."
---

# Sanitize input, mask PII, and validate output

## Inputs

raw user text; model text.

## Steps

1. Input sanitizer: compile reject patterns for common prompt-injection phrases (instructions to ignore prior directions, role-play jailbreaks, and requests to reveal the hidden prompt). `check` returns whether the text is safe and, if not, why. `clean` strips delimiter runs attackers use to close a prompt section.
2. PII detector: regex for email, phone, SSN, and credit card. `detect` lists types. `mask` replaces them with markers such as email-redacted.
3. Output validator: run the PII detector on the model text and block harmful patterns. Return cleaned text plus warnings. An email in the output is masked; harmful instructions are blocked.
4. One security-pipeline class holds all three. Order on the way in: injection check, clean, mask PII, then the model. On the way out: validate before the client. Decorate with `@traceable`.

## Output

allow with a cleaned string, or block with a reason. The model never sees a blocked payload or raw PII.

## Failure modes

he says this is not bulletproof against a determined attacker; it catches common attacks quickly and with no model call. Regex can miss creative PII.
