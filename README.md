# Quick Start: Using & Reusing Delivery Workflows

## 1. Add a Workflow from a Template
1. In your repository, go to **Actions → New workflow**.
2. Select the **Delivery** template you want (for example, “Delivery Lint Template”).
3. Commit the auto-generated file. That’s it - no extra configuration required unless you want to customize triggers or steps.

## 2. Call a Reusable Workflow
If you prefer referencing a shared workflow directly, create a `.github/workflows/your-workflow(name that you prefer).yml` in your repo and add following, below will be example usage (code) and main reusable workflow that we calling lives here - https://github.com/humalytix/delivery-core/blob/main/.github/workflows/release-notify.yml.

```
name: Release Notify

on:
  release:
    types: [published]

permissions:
  contents: read
  actions: read
  pull-requests: read

jobs:
  call-release-notify:
    uses: humalytix/delivery-core/.github/workflows/release-notify.yml@main
    with:
      release_tag: ${{ github.event.release.tag_name }}
    secrets:
      GH_APP_ID: ${{ secrets.GH_APP_ID }}
      GH_APP_PRIVATE_KEY: ${{ secrets.GH_APP_PRIVATE_KEY }}
      GH_APP_INSTALLATION_ID: ${{ secrets.GH_APP_INSTALLATION_ID }}
      SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK_URL }}
```
