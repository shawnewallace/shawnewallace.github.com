# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a personal blog built with Jekyll and hosted on GitHub Pages. It uses the [Beautiful Jekyll](https://github.com/daattali/beautiful-jekyll) remote theme (v5.0.0) and focuses on technical content related to software architecture, event-driven systems, and AI integration.

## Key Commands

```bash
# Install dependencies (first-time setup)
bundle install

# Run the site locally with drafts included
bundle exec jekyll serve --drafts

# Run without drafts (production mode)
bundle exec jekyll serve

# Create a new published post
bundle exec jekyll post "Post Title"

# Create a new draft
bundle exec jekyll draft "Draft Title"
```

**Important**: Changes to `_config.yml` require restarting the Jekyll server.

## Site Architecture

### Directory Structure
- `_posts/` — Published posts (`YYYY-MM-DD-title.md` naming required)
- `_drafts/` — Draft posts (no date prefix; excluded from production builds)
- `_includes/mermaid-script.html` — Client-side Mermaid.js diagram renderer
- `_layouts/` — Custom layout overrides (currently empty; uses theme defaults)
- `_data/interesting_links.yml` — Sidebar links widget (up to 3 entries with `title` and `url`)
- `assets/img/` — Post images and site assets
- `assets/css/custom-styles.css` — Theme overrides (1600px max-width, `.post-figure`/`.figure-left`/`.figure-right` float helpers)
- `_config.yml` — Jekyll configuration, theme settings, and color scheme

### Configuration Notes
- Remote theme: `daattali/beautiful-jekyll@5.0.0` (Gemfile pins `~> 4.1` for local dev only)
- `_config.yml` defaults set `comments: true` and `social-share: true` for all posts — no need to repeat these in front matter unless overriding
- Permalink format: `/:year-:month-:day-:title/`
- Pagination: 5 posts per page at `/posts/page:num/`

### Post Front Matter Template
```yaml
---
layout: post
title: "Your Post Title"
subtitle: "Optional subtitle"
date: YYYY-MM-DD HH:MM:SS -0400
categories: [Category One, Category Two]
tags: [tag1, tag2, tag3]
description: "SEO/excerpt description"
thumbnail-img: /assets/img/image-name.png
thumbnail-dimensions: "width: 600px; max-width: 100%; height: auto;"
---
```

`thumbnail-dimensions` is optional and only needed to constrain oversized images.

### Mermaid Diagrams

To render Mermaid diagrams in a post, add the include in the post **body** (after the front matter `---`):

```markdown
---
layout: post
title: "..."
---

{% include mermaid-script.html %}

```mermaid
graph TD
  A --> B
```
```

The script converts fenced ` ```mermaid ` blocks into rendered diagrams via Mermaid.js from CDN.

## Deployment

Deploys automatically via GitHub Actions on push to `master`. No manual steps required.
