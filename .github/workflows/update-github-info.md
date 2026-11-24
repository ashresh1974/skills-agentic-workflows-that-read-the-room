---
name: update-github-info
description: Review GitHub news and update Mona's GitHub information page
intent: Keep Mona's GitHub information page current with practical, source-backed official news.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
strict: true
network:
  allowed:
    - github.blog
    - github.com
engine:
  id: copilot
  copilot-sdk: true
  model: claude-sonnet-4.5
tools:
  cli-proxy: false
  edit:
  web-fetch:
  bash: false
safe-outputs:
  create-pull-request:
    allowed-files:
      - site/content/github-info.md
    title-prefix: "[github-info] "
---

# Update GitHub Info

Review Mona's editorial guidance and the latest official GitHub news, then propose a focused update to `site/content/github-info.md`.

## Required sources

1. Read `notes/mona-notes.md` and follow its editorial rules.
2. Fetch `https://github.blog/latest/`.
3. Fetch `https://github.blog/changelog/`.

## Task

- Compare the fetched Blog and Changelog information with the current content in `site/content/github-info.md`.
- Add or revise only practical, concise, source-backed information that helps developers learn GitHub faster.
- Mention the source for every item that comes from the GitHub Blog or GitHub Changelog.
- Preserve Mona's existing editorial angle and avoid unsupported claims.
- Make no other repository changes.

## Pull request

When the page has a meaningful update:

- Use `create-pull-request` to open a pull request for Mona to review.
- Change only `site/content/github-info.md`.
- Summarize the reviewed news, the changes made, and the source links in the pull request body.

If the sources do not provide a meaningful or sufficiently evidenced update, call `noop` with a brief reason and do not open a pull request.
