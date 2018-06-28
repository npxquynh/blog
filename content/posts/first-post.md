---
title: "Hugo theme does not work with GitHub Project Pages"
date: 2018-06-29T01:29:59+02:00
draft: false
---

;TLDR

Read the document of deployment for GitHub Project Pages again

### My setup

1. Setup a simple site with Hugo with [_Quick Start_ tutorial](https://gohugo.io/getting-started/quick-start/)
2. Use _Project Pages_ on GitHub to host this blog at `<USERNAME>.github.io/<PROJECT_NAME>` . The [GitHub page documentation](https://help.github.com/articles/user-organization-and-project-pages/#user--organization-pages) explains the differences between the two. The main reason I chose _Project Pages_ over _User Pages_ is because only _master_ branch can be used for publishing.
3. Follow the [Deployment of Project Pages From Your `gh-pages` branch](https://gohugo.io/hosting-and-deployment/hosting-on-github/#deployment-of-project-pages-from-your-gh-pages-branch)

### Problem

The theme doesn't work when I tried it on GitHub

### Solution

The [Deployment of GitHub Project Pages documentation](https://gohugo.io/hosting-and-deployment/hosting-on-github/#github-project-pages) mentioned it right in the beginning. But somehow I skipped through it. So I write the first post to remind myself to read more carefully next time.

> Make sure your `baseURL` key-value in your [site configuration](https://gohugo.io/getting-started/configuration/) reflects the full URL of your GitHub pages repository if you’re using the default GH Pages URL (e.g., `<USERNAME>.github.io/<PROJECT>/`) and not a custom domain.

