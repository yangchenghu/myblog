# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Hugo-based personal technical blog focused on iOS/Android/React Native/Kotlin Multiplatform/DevOps content. The blog uses the PaperMod theme and is deployed to GitHub Pages with custom domain support.

## Development Commands

### Local Development
```bash
# Start development server with drafts
hugo server -D

# Start with drafts and future posts
hugo server -DF

# Build for production
hugo --minify

# Build with cleanup
hugo --minify --gc
```

### Content Management
```bash
# Create new post
hugo new posts/post-title.md

# List drafts
hugo list drafts

# List all posts
hugo list all
```

## Architecture

### Key Directories
- `content/posts/` - Blog posts in Markdown with front matter
- `static/` - Static assets (images, CSS, CNAME file)
- `layouts/` - Custom Hugo templates
- `archetypes/` - Content templates for new posts
- `themes/PaperMod/` - PaperMod theme (git submodule)

### Configuration
- `hugo.toml` - Main Hugo configuration with SEO settings, theme parameters, and build options
- `.github/workflows/deploy.yml` - GitHub Actions for automatic deployment to GitHub Pages

### Content Structure
Posts use TOML front matter with these key fields:
- `title`, `date`, `description`, `tags`, `categories`, `draft`
- `cover.image` and `cover.alt` for featured images
- Posts are organized in `content/posts/` with hierarchical categories

### SEO Features
- Automatic sitemap.xml generation
- Meta descriptions and Open Graph tags
- JSON-LD structured data
- Canonical URLs
- Robots.txt
- Bread crumbs and table of contents

### Theme Customization
The blog uses PaperMod theme with these customizations:
- Light/dark mode support
- Reading time display
- Share buttons
- Post navigation links
- Table of contents

## Deployment

The blog is automatically deployed to GitHub Pages via GitHub Actions when pushing to the main branch. The deployment uses Hugo Extended version 0.135.0 and builds with minification.

## Content Creation Workflow

1. Create new post: `hugo new posts/title.md`
2. Edit content and set `draft: false` when ready
3. Preview locally: `hugo server -D`
4. Commit and push to trigger deployment

## Custom Domain

The blog uses custom domain `blog.chenghu.me` with:
- CNAME file in `static/`
- DNS configuration for subdomain
- HTTPS enabled through GitHub Pages