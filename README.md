# bump-site

Marketing site for the [bump](https://github.com/breadman69420/bump) Android app.

> **⚠️ This repo is a mirror, not the live site.** The live site at `bumpnow.app` is served by the [bump-server](https://github.com/breadman69420/bump-server) Go app from its `static/` directory. This repo exists for standalone browsing and is kept in sync manually. **Source of truth is `bump-server/static/`.** If the two diverge, the server repo wins.

## Pages

| Path | Purpose |
|---|---|
| `/` | Landing page |
| `/privacy` | Privacy policy (with anchored `#data-deletion` section for Play Console) |
| `/safety` | Child safety standards (Play Console CSAE policy) |

## Stack

Static HTML with inline CSS. No build step, no framework, no dependencies. Plus Jakarta Sans from Google Fonts. Dark theme, WCAG AA contrast throughout.

## Editing

Edits should happen in `bump-server/static/` first, then be mirrored here:

```sh
cp ../bump-server/static/index.html        ./index.html
cp ../bump-server/static/privacy/index.html ./privacy/index.html
cp ../bump-server/static/safety/index.html  ./safety/index.html
git add . && git commit -m "Mirror from bump-server@<sha>" && git push
```

Then redeploy the server so the live site picks up the change:

```sh
cd ../bump-server && fly deploy --remote-only
```

## Companion repos

- **[bump](https://github.com/breadman69420/bump)** — Android client
- **[bump-server](https://github.com/breadman69420/bump-server)** — Go backend, source of truth for this site
