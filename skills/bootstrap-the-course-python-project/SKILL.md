---
name: "Bootstrap the course Python project"
description: "starting the local environment the course codes against."
---

# Bootstrap the course Python project

## Inputs

OpenAI API key and an Anthropic API key, saved once and copied immediately.

## Steps

1. Create the OpenAI secret under account settings, default project. Create the second provider key from that vendor's API-keys page. The spoken URL is unclear in the captions (`platform.claw.com`).
2. If `uv` is missing, install it (Mac: the curl installer the instructor already had; Windows: look up the installer). Then `uv init`, `uv venv`, and activate (`.venv/bin/activate` on Mac; the Windows activate script is under the venv `Scripts` directory).
3. `uv add` LangChain, LangChain core, LangGraph, the OpenAI integration, the Anthropic integration, and python-dotenv. Add `langchain-community` when loaders or splitters are needed. PDF loading also needs `uv add pypdf`.
4. Create the env file and store both keys. Load it with dotenv before any client call.
5. Verify imports. Package versions in this course are read with `importlib.metadata` (`version`), not a LangChain version attribute that failed for the instructor. Call `ChatOpenAI` with a mini model (`gpt-4o-mini` is what he aimed at) via `invoke`, not `predict`. Repeat a one-word check with `ChatAnthropic`.

## Output

printed LangChain core and LangGraph versions (both described as just over 1.0 at record time) and a successful completion from each provider.

## Failure modes

missing key, wrong interpreter, or a removed import path. Versions will differ later.
