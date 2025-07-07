[![pages-build-deployment](https://github.com/shawnewallace/shawnewallace.github.com/actions/workflows/pages/pages-build-deployment/badge.svg)](https://github.com/shawnewallace/shawnewallace.github.com/actions/workflows/pages/pages-build-deployment)

# Shawn Wallace's Personal Blog

This is the repository for my personal blog, hosted via GitHub Pages. The site is built with Jekyll using the [Beautiful Jekyll](https://github.com/daattali/beautiful-jekyll) theme.

## Site Structure

- `_posts/` - Published blog posts
- `_drafts/` - Draft posts (not published on the site unless using `--drafts` flag)
- `assets/` - Images, CSS, and other site assets
- `_config.yml` - Site configuration
- `index.html` - Main landing page
- `about.md`, `now.md`, `resume.md` - Static content pages

## Local Development

### Prerequisites

- Ruby and Bundler installed
- Jekyll dependencies installed via `bundle install`

### Running Locally

To run the site locally with draft posts included:

```bash
bundle exec jekyll serve --drafts
```

To run without drafts (production mode):

```bash
bundle exec jekyll serve
```

### Creating New Posts

Posts should be named using the format: `YYYY-MM-DD-title.md`

All posts should include proper front matter:

```markdown
---
layout: post
title: "Your Post Title"
subtitle: "Optional subtitle"
date: YYYY-MM-DD HH:MM:SS -0400
categories: [Category1, Category2]
tags: [tag1, tag2, tag3]
comments: true
---
```

## Deployment

The site is automatically built and deployed via GitHub Actions whenever changes are pushed to the main branch.