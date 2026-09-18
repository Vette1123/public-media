# public-media

Rendered marketing images, **public on purpose**, for every project that posts with
[postkit](https://github.com/Vette1123/postkit).

## Why this repo is public

Instagram and Threads do not accept image bytes. They accept a URL and fetch it from Meta's
own servers, so an image has to be publicly reachable before a post can be created at all.
Every hosted alternative (S3, R2, a CDN) wants a card on file; `raw.githubusercontent.com`
serves a public repo for free, forever, with the right content type.

So this is the one deliberately public piece of otherwise private projects. Each app's own
repo stays where it is.

## What goes in here

Only images that are **already public or about to be** — the canvases that go out on a Page,
a feed or a profile the same day.

Never:

- screenshots of unreleased features, staging data, or anything under embargo
- anything with a real person's transactions, name, email or phone in it
- keys, tokens, `.env` anything, or exports of a real account

If an image would be a problem on the front page of the app's Instagram, it does not belong
here, because that is exactly where it is going.

## Layout

```
<project>/<pack>/<canvas>-<hash>.jpg
```

- **`<project>`** — one folder per repo: `masareef/`, `rafiq/`, whatever comes next.
- **`<pack>`** — the release or campaign the image belongs to, so a folder is a whole post.
- **`<hash>`** — the first 12 hex of the file's SHA-1. Names are content-addressed, so the
  same bytes upload once and are reused, and a re-rendered canvas can never quietly serve
  the old picture from a cached URL.

postkit writes all of this. Nothing here is meant to be arranged by hand.

## Adding a project

Nothing to create. Point the project's `postkit.config.json` at this repo:

```json
"media": { "host": "github", "repo": "Vette1123/public-media", "branch": "main" }
```

The prefix defaults to the project name, so the folder appears on the first post.

## Deleting

Safe to delete a whole pack folder once the posts referencing it are gone. A live
Instagram or Threads post keeps serving Meta's own copy of the image, not this URL — Meta
fetches once, at publish time.
