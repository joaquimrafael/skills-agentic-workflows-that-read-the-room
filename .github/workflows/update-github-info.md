---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read

tools:
  edit:
  web-fetch:

network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com

safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    reviewers: [mona]
    draft: true
    max: 1
---

# Update GitHub Info

Read `notes/mona-notes.md` and the current contents of `site/content/github-info.md` before researching or editing.

Use web-fetch to read these sources:

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Identify recent, relevant updates that help developers learn GitHub faster. Keep summaries short and practical, avoid duplicating information already in `site/content/github-info.md`, and include the original source link (GitHub Blog, Changelog, or Awesome Copilot workflows) for every new item. Do not infer details that are not supported by the sources.

Update only `site/content/github-info.md`. If there are no useful new updates, make no changes and do not open a pull request. Otherwise, propose the change with the configured `create-pull-request` safe output as a draft pull request for Mona to review; do not write directly to the default branch. In the pull request description, summarize the additions and include the source links.