# CLAUDE.md — bump-site

Context for Claude instances working in this repo. Read first: **this repo is not the live site.**

## What this is

Mirror of the static marketing pages for `bumpnow.app`. The actual live site is served by the [bump-server](https://github.com/breadman69420/bump-server) Go app from its `static/` directory on Fly.io. This repo exists only so the pages are browsable on GitHub as standalone HTML.

## Critical thing that will bite you

**Drift between this repo and `bump-server/static/` is a silent footgun.** Changes made here are invisible to users — only `bump-server/static/` is served on the wire. If you are asked to "edit the privacy policy" or "fix the landing page," the correct action is:

1. Edit `../bump-server/static/<page>/index.html` (source of truth)
2. Copy to `./<page>/index.html` in this repo (mirror)
3. Commit and push both repos
4. Run `fly deploy --remote-only` from `../bump-server` (this is what makes the change live)

Editing only this repo will appear to work — the file on GitHub will show the new content — but `bumpnow.app` will keep serving the stale version until the server is deployed. Verify with `curl -s https://bumpnow.app/<path> | grep <new content>` after any change.

## Structure

```
index.html             — landing page
privacy/index.html     — privacy policy (anchored #data-deletion section)
safety/index.html      — child safety standards (CSAE policy)
```

No build step. No dependencies. Plus Jakarta Sans from Google Fonts CDN. Inline `<style>` blocks in each page.

## Style conventions

- Dark theme, pure black background
- Body text: `#c5c5c5` minimum (13:1 contrast on `#000`, clears WCAG AA comfortably)
- Never use `#555` or dimmer for body text — verified readable on LCDs, sunlight, and dimmed displays as of April 5 2026
- Lowercase-styled headings to match the app's voice
- Interactive elements (links, buttons) must pass AA at 4.5:1 minimum

## Companion repos

- **bump-server**: `../bump-server` — source of truth and the thing that actually serves this site
- **bump**: `../bump` — Android client
- Umbrella dir: `/Users/ttalvac/Apps/bump/`
