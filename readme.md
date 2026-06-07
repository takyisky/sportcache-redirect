# sportcache-redirect

A minimal Render Static Site used exclusively to redirect legacy domain traffic to the live SportCache athletics platform.

## What this does

Redirects all traffic from:
`https://www.athleticstiming.publicvm.com/*`

To:
`https://athletics.sportcache.com/*`

Deep paths and query strings are preserved (e.g. `/result/african-athletics-championship-accra-2026?day=2` carries over correctly).

## How it works

The redirect is configured natively via Render's **Redirects/Rewrites** dashboard — NOT a `_redirects` file (that's a Netlify convention and is ignored by Render).

Rule:
- Source: `/*`
- Destination: `https://athletics.sportcache.com/*`
- Action: Redirect (301)

Note: Render uses `*` in the destination to apply the captured path, NOT `:splat`. Using `:splat` will pass the literal string through and break the redirect.

## Why this exists

`athleticstiming.publicvm.com` was the original domain for the Ghana Athletics / African Athletics Championship results platform before the migration to `sportcache.com`. Some external websites still link to the old URL, so this redirect ensures those legacy links land on the correct platform.

## Known limitations

- Only `www.athleticstiming.publicvm.com` redirects. The bare apex (`athleticstiming.publicvm.com`) does NOT — it never verified on Render since the publicvm apex isn't controllable. Live championship links use `www`, so this is covered.
- 301 is a permanent redirect, so browsers cache it aggressively. Test changes in incognito.

## Infrastructure

- **Host:** Render (Static Site, free tier)
- **DNS:** publicvm.com dashboard — CNAME `www.athleticstiming` → `sportcache-redirect.onrender.com`
- **Repo:** Only exists so Render has something to deploy. Files inside do nothing — the redirect rule lives entirely in Render's dashboard.

## Teardown (when no longer needed)

1. Delete the static site in Render.
2. Remove the `www.athleticstiming` CNAME in the publicvm dashboard.
3. Repo can be kept or deleted.
