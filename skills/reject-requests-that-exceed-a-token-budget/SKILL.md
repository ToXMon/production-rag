---
name: "Reject requests that exceed a token budget"
description: "user-controlled or unpredictable input, and when you need per-user or per-endpoint chargeback and abuse limits."
---

# Reject requests that exceed a token budget

## Inputs

raw user text, a max token count, running totals.

## Steps

1. Track input tokens, output tokens, and request count.
2. Estimate before the call. His guardrail is word count times 1.3. He says rough is enough for a bouncer, not for accounting.
3. If the estimate exceeds the budget, raise and do not call the model (demo budget 100 rejected an estimate of 133). Default max he shows on the class is 4,000.
4. Otherwise invoke, then record usage.
5. Log stats per user, per hour, and per endpoint.

## Output

either a normal completion plus updated counters, or a budget error and zero model spend.

## Failure modes

the estimate is not a real tokenizer count. One pasted contract can be on the order of 50,000+ input tokens and about 2,000 output tokens, which he compares to about 100 normal requests.
