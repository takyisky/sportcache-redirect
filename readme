# sportcache-redirect

A minimal Render Static Site used exclusively to redirect legacy domain traffic to the live SportCache platform.

## What this does

Redirects all traffic from:
`https://www.athleticstiming.publicvm.com`

To:
`https://athletics.sportcache.com`

## How it works

The redirect is configured natively via Render's **Redirects/Rewrites** dashboard (not a `_redirects` file). Rule:
- Source: `/*`
- Destination: `https://athletics.sportcache.com/:splat`
- Type: Redirect 301

## Why this exists

`athleticstiming.publicvm.com` was the original domain used for the Ghana Athletics / African Athletics Championship results platform before the migration to `sportcache.com`. The domain was flagged as malware due to the publicvm.com platform's reputation. This redirect ensures any old links (external championship websites, shared links, etc.) still land on the correct platform.

## Infrastructure

- **Host:** Render (Static Site, free tier)
- **DNS:** publicvm.com dashboard — CNAME `www.athleticstiming` → `sportcache-redirect.onrender.com`
- **Repo:** Only needs to exist for Render to have something to deploy. The redirect rule lives in Render's dashboard, not in this repo.
