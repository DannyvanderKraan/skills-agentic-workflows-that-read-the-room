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
2. Use the `web-fetch` tool to fetch `https://github.blog/latest/` for the
   latest posts.
3. Use the `web-fetch` tool to fetch `https://github.blog/changelog/` for the
   latest changelog entries.
4. Use the `web-fetch` tool to fetch
   `https://awesome-copilot.github.com/workflows/` for the latest workflows.
5. If one of those sources cannot be fetched, continue with the remaining
   sources and still open the pull request.
6. Review the current content in
   [site/content/github-info.md](../../site/content/github-info.md).
7. Update `site/content/github-info.md` with a short, practical summary of
  noteworthy recent stories from the GitHub Blog, GitHub Changelog, and
  Awesome Copilot workflows, following Mona's notes:
   - Keep summaries short and practical.
   - Prefer updates that help developers learn GitHub faster.
   - Mention the source whenever a change comes from the GitHub Blog or
    GitHub Changelog or Awesome Copilot workflows.
   - Do not remove existing sections unless the information is outdated or
     superseded by a newer story.
8. Open a pull request with the updated file so Mona can review the changes
   before they go live. Do not write directly to the `main` branch.

## Notes

- Only modify `site/content/github-info.md`. Do not change other files.
- Network access:
  - `web-fetch` is the only tool with outbound network access.
  - `curl`, `wget`, and any other shell or bash command for network access are
    blocked by the egress firewall and must never be used.
  - A blocked shell network command is not a missing tool and must not be
    reported via `missing_tool`. Use `web-fetch` instead.
- Skip opening a pull request only when every source fails to fetch, or when
  none of `https://github.blog/latest/`, `https://github.blog/changelog/`,
  or `https://awesome-copilot.github.com/workflows/` returns new information
  worth adding.
