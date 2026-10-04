---
name: "Attach sources to retrieved chunks"
description: "when users must verify an answer."
---

# Attach sources to retrieved chunks

## Inputs

retrieved documents that already have metadata such as source file and page content.

## Steps

1. Format each chunk with a source tag (the course calls this formatting docs with sources).
2. Pass that formatted context into the grounded prompt.
3. Ask the answer to include which sources it used.

## Output

answer plus citations the user can check.

## Failure modes

not stated beyond loss of trust if sources are omitted.
