# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a personal blog built with Jekyll and hosted on GitHub Pages. It uses the [Beautiful Jekyll](https://github.com/daattali/beautiful-jekyll) remote theme (v5.0.0) and focuses on technical content related to software architecture, event-driven systems, and AI integration.

## Key Commands

### Local Development
```bash
# Install dependencies (first-time setup)
bundle install

# Run the site locally with drafts included
bundle exec jekyll serve --drafts

# Run the site in production mode (without drafts)
bundle exec jekyll serve
```

**Important**: Changes to `_config.yml` require restarting the Jekyll server to take effect.

### Working with Posts
```bash
# Posts are stored in _posts/ with naming format: YYYY-MM-DD-title.md
# Drafts are stored in _drafts/ (no date prefix needed)

# Create new posts using jekyll-compose (if available)
bundle exec jekyll post "Post Title"
bundle exec jekyll draft "Draft Title"
```

## Site Architecture

### Directory Structure
- `_posts/` - Published blog posts (must follow `YYYY-MM-DD-title.md` naming)
- `_drafts/` - Draft posts (excluded from production builds unless `--drafts` flag is used)
- `_includes/` - Custom includes (e.g., `mermaid-script.html` for diagram rendering)
- `_layouts/` - Custom layout overrides (currently empty, uses theme defaults)
- `assets/img/` - Images for posts and site assets
- `assets/css/custom-styles.css` - Custom CSS overrides for the Beautiful Jekyll theme
- `_config.yml` - Jekyll configuration and site settings

### Configuration (_config.yml)
- Uses Beautiful Jekyll remote theme version 5.0.0
- Custom navigation links defined in `navbar-links`
- Comments enabled via Disqus (`www-shawnewallace-com`)
- Google Analytics tracking via gtag (`G-E7MLGF56Q5`)
- Timezone: `America/New_York`
- Permalink format: `/:year-:month-:day-:title/`
- Pagination: 5 posts per page
- Custom container max-width: 1600px (via custom-styles.css)

### Post Front Matter Template
All posts require the following front matter:
```yaml
---
layout: post
title: "Your Post Title"
subtitle: "Optional subtitle"
author: Shawn Wallace
date: YYYY-MM-DD HH:MM:SS -0400
tags: [tag1, tag2, tag3]
comments: true
thumbnail-img: /assets/img/image-name.jpg  # optional
---
```

### Custom Features

#### Mermaid Diagrams
Posts that include Mermaid diagrams need to include the mermaid-script.html in their front matter:
```yaml
---
layout: post
# ... other front matter ...
---

{% include mermaid-script.html %}
```

The script converts fenced code blocks with `language-mermaid` class into rendered diagrams using Mermaid.js from CDN.

#### Custom Styling
Custom styles in `assets/css/custom-styles.css` include:
- Extended container max-width (1600px) for better content display on large screens
- Responsive figure styles (`.post-figure`, `.figure-left`, `.figure-right`) for floated images in posts
- Custom styles referenced in `_config.yml` via `site-css` array

## Deployment

The site deploys automatically via GitHub Actions when changes are pushed to the master branch. The deployment status badge is visible in the README.

## Theme Customization

This site uses the Beautiful Jekyll remote theme. To override theme defaults:
- Place custom includes in `_includes/`
- Place custom layouts in `_layouts/`
- Add custom CSS in `assets/css/` and reference in `_config.yml` under `site-css`

Theme colors are customized in `_config.yml` (navbar, page, text, links, footer colors).

## Content Focus

The blog covers:
- Event-driven Architecture (EDA) patterns and best practices
- Software architecture and system design
- AI/ML integration in enterprise systems
- Technical leadership and career development

Posts often include technical diagrams (using Mermaid), code examples, and architecture patterns.
