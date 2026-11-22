---
name: update-github-info
description: Keep Mona's GitHub information page current and propose updates through a pull request.
intent: Review trusted GitHub Blog sources daily and propose concise, sourced updates to Mona's GitHub information page.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
  copilot-requests: write
strict: true
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - github.blog
    - github.com
tools:
  edit: true
  web-fetch: {}
safe-outputs:
  create-pull-request:
    title-prefix: "[Mona] "
    allowed-files:
      - "site/content/github-info.md"
    draft: false
    if-no-changes: "ignore"
---

# Update GitHub Info

Review the repository's editorial guidance and current GitHub news, then propose only a focused update to Mona's GitHub information page.

1. Read `notes/mona-notes.md` and use its editorial rules.
2. Read `site/content/github-info.md` to understand the current page.
3. Use web fetch to read:
   - https://github.blog/latest/
   - https://github.blog/changelog/
4. Compare the fetched news with the current page. Identify only accurate, practical updates that help developers learn GitHub faster.
5. Keep summaries short, concise, and in Mona's editorial voice. Mention the GitHub Blog or GitHub Changelog source for any new information.
6. Update only `site/content/github-info.md`. Preserve its existing structure unless a clear new section or theme is justified.
7. Use `create-pull-request` to open a pull request for Mona to review. Set a concise title and explain which sources informed the change. Do not write directly to `main`.

Call `noop` with a brief reason when no material update is found, the sources are unavailable or insufficient, or the proposed change would duplicate existing content.
