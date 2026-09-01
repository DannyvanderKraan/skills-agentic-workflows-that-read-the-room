---
name: update-github-info

on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read

engine: copilot

tools:
  edit:
  web-fetch:

network:
  allowed:
    - defaults
    - github.blog
    - github.com
    - awesome-copilot.github.com

safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    labels: [automation, github-info]
---

# Update GitHub Info

Keep the GitHub Info site content fresh with the latest news from GitHub Blog and
the GitHub Changelog, following Mona's editorial preferences.

## Instructions

1. Read [notes/mona-notes.md](../../notes/mona-notes.md) to understand Mona's
   editorial preferences for the GitHub Info website.
2. Fetch the latest posts from `https://github.blog/latest/`.
3. Fetch the latest entries from `https://github.blog/changelog/`.
4. Fetch the latest workflows from
  `https://awesome-copilot.github.com/workflows/`.
5. Review the current content in
   [site/content/github-info.md](../../site/content/github-info.md).
6. Update `site/content/github-info.md` with a short, practical summary of
  noteworthy recent stories from the GitHub Blog, GitHub Changelog, and
  Awesome Copilot workflows, following Mona's notes:
   - Keep summaries short and practical.
   - Prefer updates that help developers learn GitHub faster.
   - Mention the source whenever a change comes from the GitHub Blog or
    GitHub Changelog or Awesome Copilot workflows.
   - Do not remove existing sections unless the information is outdated or
     superseded by a newer story.
7. Open a pull request with the updated file so Mona can review the changes
   before they go live. Do not write directly to the `main` branch.

## Notes

- Only modify `site/content/github-info.md`. Do not change other files.
- If none of `https://github.blog/latest/`, `https://github.blog/changelog/`,
  or `https://awesome-copilot.github.com/workflows/` returns new information
  worth adding, skip opening a pull request.
