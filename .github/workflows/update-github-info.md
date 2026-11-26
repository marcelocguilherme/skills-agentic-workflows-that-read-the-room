---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - github.com
    - github.blog
tools:
  web-fetch:
  edit: true
safe-outputs:
  create-pull-request:
    title-prefix: "[chore] "
    body-footer: "Updated by [{workflow_name}]({run_url})"
    labels: [automation]
    reviewers: [mona]
    draft: true
    allowed-files:
      - "site/content/github-info.md"
    base-branch: "main"
---

## Instructions

You are an AI assistant helping to keep the site's GitHub information up-to-date.

### Gather Information

1. Read `notes/mona-notes.md` to understand context and formatting preferences
2. Web fetch the latest from https://github.blog/latest/
3. Web fetch the latest from https://github.blog/changelog/
4. Review the current content at `site/content/github-info.md`

### Update and Propose

If there are substantive updates to make:
- Update `site/content/github-info.md` with:
  - Latest GitHub Blog highlights
  - Recent changelog entries
  - Insights from Mona's notes
  - Consistent formatting and structure
- Include a summary in your create_pull_request output explaining what changed
- The PR will be assigned to `mona` for review

If the information is current, use `noop` with a brief note that no updates are needed.
