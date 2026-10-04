---
name: "Deploy the API on Render"
description: "the service should be reachable on a public URL."
---

# Deploy the API on Render

## Inputs

a Git repo, a Render account connected to GitHub, secrets only in the dashboard.

## Steps

1. Add `render.yaml`: type web, Python runtime, a region (demo Oregon), plan free, build command that installs `uv` then syncs deps, start command `uvicorn` bound to Render's `PORT`, health check path `/health`, auto deploy true. Mark secrets so the blueprint does not sync them (`sync: false`). The file must not contain real secrets.
2. Gitignore env files. Commit and push. Do not commit `.env`.
3. New Web Service from the GitHub repo. He selects Docker in one pass and Python 3 in another; follow the blueprint you actually wrote. Import env vars from a local env file in the dashboard rather than typing secrets into git.
4. Deploy. `GET /health` on the public URL, then exercise docs, cache, PII masking, and a blocked injection (demo status 400 with a security-filter detail).
5. A commit to main redeploys. He bumps a version string from 1.0 to 1.1 and confirms `/health` after the new deploy.

## Output

a public base URL.

## Failure modes

free tier spins down after 15 minutes of inactivity; the next request cold-starts for about 30 to 60 seconds. Free runtime he cites is about 750 hours per month. Horizontal scale requires replacing the in-memory cache with Redis so instances share it. He says Prometheus replaces the in-process counters and a load balancer sits in front, but the request-path pattern stays the same. Custom domain and clicking to scale instances are named; click-path steps are not specified.
