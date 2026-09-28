---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read

model: gpt-4.1

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

Update only `site/content/github-info.md`, making at least one small, practical, relevant improvement supported by the configured sources whenever they provide valid information. Read the existing content first and do not duplicate it. Never invent facts or links. After editing, verify that `site/content/github-info.md` changed and that no other content file was modified. Then always use the `create_pull_request` safe output to open exactly one draft pull request containing the change, even if the update is small. Base it on the repository's default branch, give it a clear title, and include a concise summary and source links in the description. Do not use `noop` if a valid update can be made. If the sources provide no valid information for a non-duplicated improvement, make no content change and use `noop`.